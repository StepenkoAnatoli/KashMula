# 0003. Runtime: one DBOS worker, one Postgres database, agents under DBOSDurability

- Date: 2026-10-04
- Status: proposed

## Context

The stack is fixed: Python 3.11 or later, DBOS Transact, Pydantic AI and Postgres, pinned to
`dbos==3.2.0`, `pydantic-ai[dbos]==2.54.0` and `apify==4.0.2` (U-38). How the stack is arranged
is open. These facts bear on it:

- Queue concurrency limits count per process, while rate limits are global (E-229).
- SQLite cannot serve an application on several servers. Postgres is recommended for
  production (E-224).
- The corpus does not say which process recovers a pending workflow after a crash
  (U-40 residual).
- DBOS keeps its tables in schema `dbos` by default and migrates them itself (E-223). An
  application's data may use its own URL (E-224).
- Attribute filters and listen/notify are Postgres features (E-231, E-223). The `reset_dbos`
  fixture makes fast SQLite tests possible (E-232; U-43).
- Under Pydantic AI, `DBOSAgent` is deprecated and removed in v3. New code adds
  `DBOSDurability` and calls `agent.run()` in its own workflow (E-237). The capability's import
  path and `StepConfig` fields are not captured (U-46).
- This container runs Python 3.11.15 and offers 3.14 only as a release candidate download
  (`uv python list`, 2026-10-04).

## Decision

1. **Process model.**
   - Exactly one worker process calls `DBOS.launch()`. It hosts the schedules, every workflow,
     the agents, the stop watcher and, from phase 4, the Operate API.
   - The operator CLI never launches DBOS. It writes application rows over SQL and reads
     workflow state through `DBOSClient` (E-51 capture, E-52 capture).
2. **Storage.**
   - One Postgres database: DBOS's system tables in schema `dbos`, application tables in
     `public`, reached through SQLAlchemy Core, which comes with dbos (E-223).
   - Migrations are numbered plain-SQL files written in a subset SQLite also accepts. They are
     applied before `DBOS.launch()`, one transaction each, with checksums. They are
     forward-only.
3. **Tests.**
   - A SQLite lane through `reset_dbos` for workflows.
   - A PostgreSQL 16 lane for notifications, the stop sweep, races, migrations and
     crash-injection recovery.
4. **Agents.**
   - Every agent is built before launch with a unique name and
     `capabilities=[DBOSDurability()]`, and is run by our own `@DBOS.workflow`.
   - If the U-46 day-one check fails, each whole `agent.run()` goes inside one `@DBOS.step`
     (E-226).
   - `DBOSAgent` is never used.
5. **Toolchain.**
   - Images are pinned to Python 3.11.
   - CI has one leg, Linux with Python 3.11, with a PostgreSQL 16 service from phase 2. This
     container reproduces it.

## Alternatives rejected and why

- **Separate API and worker processes, or several workers for availability.** Each would launch
  DBOS. Recovery ownership becomes ambiguous (U-40 residual), per-process limits multiply
  (E-229), and in-process locks stop being real locks.
- **A CLI that launches DBOS to send messages.** That is a second executor, with the same
  problem.
- **A separate application database.** It gives two restore points that can drift apart, for
  no gain at this size.
- **Alembic.** The project needs no branches or downgrades, and Alembic is not in the evidence.
- **SQLite-only tests.** They miss listen/notify, attribute filters and real recovery (E-223,
  E-231).
- **Postgres-only tests.** They make every workflow test slow for no extra coverage.
- **`DBOSAgent`.** Deprecated and removed in v3 (E-237).
- **A Python 3.11 to 3.14 CI matrix**, as U-38 suggests. A matrix suits a published library,
  not pinned images. Python 3.14 is not runnable here except as a release candidate, so that leg
  would hold every merge under the lead-orchestrator rule.

## Consequences

- There is no high availability. A Machine outage pauses gates, health checks and Scout, while
  customers' runs on Apify continue.
- Per-channel locks in the policy guard are valid only while the one-process rule holds. A
  second process needs a new ADR.
- Two inferences must be proven by tests: that the app tables can share the DBOS database, and
  that DBOS management calls work from a plain thread.
- Deploys drain first (spec section 20), because recovery across application versions is not
  in the corpus.
- Python 3.12 to 3.14 are untested, which is acceptable while images pin 3.11.

## Evidence

E-51 (capture), E-52 (capture), E-220, E-221, E-222, E-223, E-224, E-225, E-226, E-229, E-231,
E-232, E-237, E-238; U-38, U-39, U-40, U-41, U-43, U-45, U-46.
