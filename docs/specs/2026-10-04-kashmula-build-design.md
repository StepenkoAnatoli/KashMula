# KashMula build design

How KashMula goes from the phase-1 decision (`docs/PLAN.md`) to a running C1 business: a
small portfolio of pay-per-event Actors on Apify Store, watched and kept within budget by a
durable runtime. Every external fact cites an evidence row (`E-nn`) or an unknown (`U-nn`)
in `research/`. "E-nn capture" means the fact is on that row's cached page under
`research/raw/` but not yet quoted in its Finding cell; phase 1 adds the quote anchors
(section 22). Internal references point at files in this repository, at the operator's own
repositories with the commit read, or at the merged Moonzila Operate-mode specification
(`moonaliza` repository, `docs/specification/operate-mode.md`), called "the Operate spec"
below.

## 1. Status

Proposed, 2026-10-04. Merging the phase-0 pull request approves this design, ADRs 0001 to
0011 in `docs/adr/`, and the phase changes it asks of `docs/BUILD.md` (section 22). A later
phase that would change this design stops and says so first (`docs/BUILD.md`, "How a phase
runs").

The design is the winner of three drafted approaches, judged on three lenses (section 6):
**Approach 3, the smallest loop that earns** (Actor first, one process, one database), with
the safety mechanisms of Approach 1 and the human-time mechanisms of Approach 2 grafted in.

Two decisions here change documents that were written before it. ADR-0001 swaps
`docs/BUILD.md` phases 1 and 2, so the first Actor is built and published before the runtime.
ADR-0002 replaces the first-wave agent table of `docs/PLAN.md` section 4 with one model agent
(Scout) plus deterministic workflows, and defers the Builder, Support and Finance agents with
named return triggers. The operator approves both by merging.

## 2. Goal and success criteria

**Goal.** Earn the first verified Apify payout from 3 to 5 reliable pay-per-event Actors
(PLAN section 1), with as little operator time as the platforms legally allow, inside the
budget, without a policy strike.

**Success criteria**, from PLAN section 5 ("Done, as defined in the contract"):

1. **30 days unattended without a policy strike.** A policy strike is any enforcement action
   against one of the operator's accounts or Actors (for example a notice set on an Actor by
   Apify's quality checks, E-254, or an Anthropic throttle, suspension or termination, E-40) or
   any external write that the policy layer would have denied. A guard
   that refuses an action is the system working, not a strike.
2. **Every remaining human step is listed and takes under one hour a week.** The list is the
   table in section 16.3. Each touch is journaled with its kind, and `kashmula status` shows
   touches and estimated minutes per week, so the criterion is measured rather than assumed.
3. **Every cost is metered against the budget.** Model spend is in the ledger with
   reservations (section 12); platform and hosting costs are entered as dated lines or read
   from the platform once the API is collected; the month's total is shown against the
   200-1,000 USD ceiling.
4. **Real revenue verified by the payout within 90 days, or a clear report of why not.**
   Apify generates the invoice on the 11th, approves it automatically on the 14th and pays on
   days 21 to 25 (E-04 capture), once the balance reaches USD 20 for PayPal or USD 100 for
   other methods (E-05). A payout counts as verified when the operator records it with
   `kashmula payout record`.

## 3. Scope and non-goals

**In scope.** The C1 first wave: the Actor template and Actors 1 to 5; the runtime (one DBOS
worker on Postgres) with its policy layer, budgets, stop signals, approval gates, kill
switch, journal and operator CLI; the Scout agent; deterministic release, health, ledger and
digest workflows; the HTTPS API that Moonzila's Operate mode consumes; deployment to one
Fly.io Machine. The design covers `docs/BUILD.md` phases 1 to 4 in detail and maps phases 5
and 6.

**Non-goals.**

- C6 (print-on-demand) and C2/C8 (alert feed). They are phases 7 and 8 and get their own
  designs on this skeleton.
- Model-generated code running on the runtime host. There is no runtime Builder in the first
  wave (ADR-0002).
- Support and Finance agents, a model router, a tracing backend, queues of our own, and
  publishing or pricing through the Apify API. Each is on the cut list with a return trigger
  (ADR-0002, section 16).
- Any customer-facing message sent by the runtime.
- High availability. One Machine runs the control plane; customers' runs on Apify do not
  depend on it (section 7).
- Monnzila's side of Operate mode. This spec defines only the runtime's half of the contract.

## 4. Fixed constraints

These are settled and not reopened here.

- The operator is an Israeli tax resident with no US status. No Stripe account of any kind
  (U-01; PLAN section 2).
- Budget: 200 to 1,000 USD a month before revenue.
- No YouTube Shorts.
- As little human time as the platforms legally allow, with the human gates of PLAN
  section 7.
- First product: C1 pay-per-event Actors on Apify Store (PLAN section 1).
- Runtime: Python 3.11 or later with DBOS Transact, Pydantic AI and Postgres (PLAN section 4),
  pinned to `dbos==3.2.0`, `pydantic-ai[dbos]==2.54.0` and `apify==4.0.2`, no pre-releases
  (U-38).
- GitHub only for source, tests and image builds, never to run the business (E-48).
- Every external fact cites an evidence row or an unknown. External content is data, never
  instructions. Secrets never enter the repository.
- The operator does the first Store publish and the first price in Console (BRIEF build-stack
  decision; U-51).

## 5. Observed, inferred and assumed

**Observed** (read in the corpus or in this repository):

- DBOS recovers a workflow from its last completed step; a step may run more than once until
  it completes; a repeated start under the same workflow ID returns the existing run (E-225).
- SQLite cannot serve an application on several servers, and Postgres is recommended for
  production (E-224); filtering workflows by attribute needs Postgres (E-231).
- Cancelling a workflow interrupts it at its next step and removes it from its queue (E-228,
  E-231). Schedules can be paused and resumed at runtime (E-52), and re-applying a schedule
  keeps its paused status (E-228 capture).
- Apify describes the first Store publish only as a Console flow, and its CLI has no publish
  or price command (E-253, E-255; U-51).
- The synthetic `apify-default-dataset-item` event charges every default-dataset item with no
  code (E-245); local test mode logs explicit charge calls (E-244).
- Apify tests every Store Actor daily with its prefill input; three failed days label it under
  maintenance (E-256).
- A new Actor waited a week for its first run, with single-digit weekly runs in months 1 and 2
  (E-14); the quality score rewards a track record (E-92).
- A provider spend limit answers HTTP 429 (tier cap) or HTTP 400 (self-set limit), and retries
  fail until access resumes (E-43).
- DROPSCRAP's `search-light-signals` is JavaScript (repository read at `f200c11`); the Agent
  repository has no licence file (read at `8932fe0`).
- This container runs Python 3.11.15, uv 0.8.17, PostgreSQL 16.14 and Docker, with ruff, mypy
  and pytest installed; uv offers Python 3.14 only as a release candidate download
  (`AGENTS.md` Orchestrator facts; `uv python list`, 2026-10-04).

**Inferred** (reasoned from the observed facts; each has a test or a check):

- With exactly one process calling `DBOS.launch()`, that process recovers every pending
  workflow (from U-40's residual and E-229). A PostgreSQL recovery test observes it.
- Application tables can share the DBOS database in a different schema (E-223, E-224). The
  PostgreSQL lane proves it.
- DBOS management calls (`cancel_workflows`, `pause_schedule`, `list_workflows`) work from a
  plain thread of the worker. A day-one check proves it.
- A forked workflow gets a new ID (E-231), so a key that must survive forks cannot contain
  the workflow ID.
- Customers' runs of a published Actor execute on Apify without our runtime (E-06, E-256), so
  a runtime outage pauses monitoring and gates, not sales.
- Every month the first publish slips moves the first possible payout back by about a month
  (E-04 capture, E-14).

**Assumed** (not in the evidence; each can be rejected):

- Niche 1 is a keyless government source of the kind DROPSCRAP already reads, such as the
  Federal Register API (E-203) or CBP CSMS (E-70). Their reuse terms are not captured (U-24),
  so phase 1 collects them before a short list is offered.
- First-wave running cost is 10 to 25 USD a month excluding Postgres hosting: a 1 GB Machine at
  $6.70 (E-49), the Apify Creator plan at $1 with $500 of bonus usage for own tests (E-13), and
  a weekly Scout run on a small model (E-42 prices, the limits in section 16).
- Numeric settings: internal spend caps at 80% of the provider limits; a 3,600-second gate wake
  timeout; `max_recovery_attempts=5` for workflows with external writes; 30-second adapter
  timeouts; a 30-day niche-gate deadline; a 120-second wait for a stop confirmation.
- The operator's time stays under one hour a week with 3 to 5 Actors. The status board measures
  it (section 16.3).
- ruff and mypy are the lint and type tools, pinned in `uv.lock` in phase 1.

## 6. Approaches considered

Three approaches were drafted and scored 0 to 10 by three independent judges.

| Approach | Operator fit | Correctness and safety | Buildability and traceability | Total |
|---|---|---|---|---|
| 1. Fenced durable control plane (reliability first) | 5 | **8** | 5.5 | 18.5 |
| 2. Least human time (policy-bounded autonomy, batched gates) | 7 | 5 | 6 | 18 |
| 3. Smallest loop that earns (Actor first, one process, one database) | **8** | 7 | **8** | **23** |

**Approach 1** put a row-lock write fence, a three-class write taxonomy with provider
read-back, a hash-chained journal, crash-injection recovery tests and a mutation manifest
into phase 1, and kept all six agents by phase 4. It was the safest design and the slowest to
the first dollar. The first publish waited for phase 3, behind the heaviest phase 1. Its STOP
held a Postgres row lock across an HTTP call, which the corpus does not describe.

**Approach 2** budgeted human time explicitly (a touch table, a weekly digest of one-line
cards, a paste-ready Console card) and shipped repairs that change no README, schema or price
without a human gate. Those unattended repairs conflict with the Operate spec ("Nothing lands
on the bot without the same reviewed edit"). They would run model-generated code without a
sandbox on the host that holds every credential.

**Approach 3** builds and publishes Actor 1 first, runs one worker on one database, and keeps
one model agent (Scout). The Builder, Support and Finance agents are cut until data asks for
them, and Actors 2 to 5 arrive as reviewed pull requests from a coding agent.

**Why Approach 3 wins.** It has the highest total and wins two of the three lenses. Its loss
on safety is one point, to Approach 1, and the judges named the Approach 1 mechanisms that
close the gap. All of them are grafted:

- write-intent rows keyed by business key and step, never by workflow ID;
- a worst-case budget reservation that stays counted if a crash leaves it unsettled;
- a STOP that waits for in-flight writes before it reports STOPPED;
- PAUSE, drain, deploy, RESUME, with versioned workflow names;
- a guard-to-test manifest;
- JSON-shaped workflow inputs and outputs;
- an import-boundary test.

From Approach 2 the design takes:

- the human-touch table with measured minutes;
- the weekly digest of one-line, digest-bound cards;
- the paste-ready Console card closed by `kashmula actor confirm-published`;
- the month in the price-change key;
- one Anthropic Workspace per agent;
- the U-46 fallback decided in advance;
- the Operate models frozen early and mirrored in `docs/contracts/operate-api.md`.

**Overridden.** Approach 3's custom per-item charging event is replaced by the synthetic
dataset-item event (ADR-0010). Two judges found the custom event's manual Console deletion
to be a human-error path onto a customer's bill.

**The strongest argument against the winner.** Actor 1 runs on the Store through phases 2
and 3 with no runtime watching it. Until the runtime is deployed in phase 4, a broken source
is caught only by Apify's daily test, which notifies after three failed days (E-256), or by the
operator, and a broken Actor costs quality score (E-92). Cutting the Builder also makes each
of Actors 2 to 5 a pull request the operator reviews, which does not scale past five Actors.
The design accepts both: the first is bounded by a repair fast path (section 15.9), the second
by the first wave's size (PLAN section 1) and a return trigger for the Builder (ADR-0002).

## 7. Architecture

### 7.1 Components

- **Apify is the data plane.** Customers' runs of a published Actor execute on Apify, billed
  through the platform (E-06). Apify's daily test watches every Store Actor (E-256).
- **The worker is the control plane.** One Python process, the only one that calls
  `DBOS.launch()`. It hosts the schedules, every workflow, the Scout agent, the stop watcher
  thread and, from phase 4, the Operate API.
- **The operator CLI (`kashmula`).** It never launches DBOS. It writes application rows over
  SQL and reads workflow state through `DBOSClient` and its `list_workflows` (E-51 capture,
  E-52 capture). For manual inspection the operator can also use the `dbos workflow` CLI
  (E-231), whose `dbos-config.yaml` names the database only through `${VAR}` (E-223).
- **Postgres, one database.** DBOS's system tables in schema `dbos` (the default, E-223) and
  the application tables in schema `public`.
- **The effects gateway.** The only code that imports network clients. Every external write is
  one DBOS step that runs the policy guard first (section 11).
- **Adapters.** Apify (pushing a source version, starting a run, reading a run and its
  dataset) and Anthropic (an `AsyncAnthropic` client with `max_retries=0`, passed as
  `anthropic_client=`, E-235, E-237).
- **Actors.** Self-contained Python projects under `actors/<slug>/`. They import nothing from
  `kashmula` (section 8).

### 7.2 Process model

There is one process because three facts point there. Queue concurrency limits count per
process while rate limits are global (E-229). SQLite cannot serve several processes
(E-224). The corpus does not say which process recovers a pending workflow (U-40 residual).
With a single executor, recovery has one owner and every in-process lock is a real lock.

Startup order:

1. Apply application migrations (section 9).
2. Read the control state.
3. Build every agent and register every workflow (E-237, E-238).
4. Call `DBOS.launch()`. Recovery of pending workflows starts here (E-225).
5. Declare the static schedules with `DBOS.apply_schedules`, which keeps an existing
   schedule's paused status (E-228 capture).
6. If the control state is not RUNNING, pause the schedules and run the stop sweep
   (section 14).
7. Start the stop watcher.

### 7.3 Picture

```
 operator ──> kashmula CLI ──SQL──┐            (phase 4) Moonzila Operate ──HTTPS──┐
                                  v                                                v
 ┌──────────────── worker: the only process that calls DBOS.launch() ─────────────────────┐
 │ startup: migrations > control > register > launch > apply_schedules > sweep if stopped  │
 │ schedules (UTC): scout weekly · health daily · ledger daily · digest weekly             │
 │ workflows: gate · release · health · ledger · digest · scout (agent.run under DBOS)     │
 │ stop watcher thread (every 5 s)              Operate API v1 (phase 4)                   │
 │                                                                                         │
 │ every external write = one effects step:                                                │
 │   guard(control, breaker, action, rules, rate, budget) -> Permit                        │
 │   -> intent row committed (SENT) -> adapter call (timeout) -> result row                │
 └─────────────┬───────────────────────────────────────┬───────────────────────────────────┘
               v                                       v
     Postgres (one database)                 adapters: apify, anthropic
       schema dbos:   DBOS system tables               │
       schema public: application tables               v
                                             Apify platform (data plane): customers run
                                             the published Actors; the Store tests each
                                             Actor daily (E-256)
```

## 8. Repository layout

```
pyproject.toml, uv.lock          Python 3.11; dbos==3.2.0, pydantic-ai[dbos]==2.54.0,
                                 apify==4.0.2 (U-38); dev: pytest, ruff, mypy
dbos-config.yaml                 system_database_url: ${DBOS_SYSTEM_DATABASE_URL} only (E-223)
config/
  policy.toml                    rules, allowlists, gate deadlines, rate caps
  budgets.toml                   caps, per-agent UsageLimits, fixed monthly cost lines, touch minutes
  prices.toml                    model prices with effective dates (E-42; E-47 shows dated changes)
src/kashmula/
  __main__.py cli.py             kashmula worker | status | gates | approve | reject | digest |
                                 stop | pause | resume | breaker | actor | research | payout |
                                 leads | journal | api
  config.py db.py ids.py journal.py contracts.py (Operate API models)
  migrations/NNNN_name.sql       plain SQL, portable to SQLite and PostgreSQL 16
  policy/   guard.py actions.py rules.py
  effects/  gateway.py permit.py
  adapters/ apify.py anthropic.py          imported only by effects/
  budget/   ledger.py breaker.py prices.py
  control/  state.py watcher.py
  gates/    service.py cards.py
  actors/   registry.py check.py card.py   (phase 1: check and card)
  research/ readiness.py
  workflows/ gate.py release.py health.py ledger.py digest.py
  agents/   scout.py                       (phase 3)
  api/                                     (phase 4)
actors/
  _template/                     the template, itself checked and tested
  <slug>/
    .actor/actor.json input_schema.json output_schema.json dataset_schema.json
           README.md CHANGELOG.md Dockerfile
    requirements.txt             apify==4.0.2 and pinned pydantic (the version uv.lock resolved)
    src/main.py src/source.py src/model.py
    tests/ tests/fixtures/       recorded source responses
qa/oracles/<slug>/               hidden oracle, committed after the build (section 15.5)
tests/
  conftest.py guards.toml        socket guard, model-request block, guard-to-test manifest
  dayone/ unit/ dbos_sqlite/ pg/ recovery/ actors/
docs/contracts/operate-api.md    the frozen Operate contract (phase 2)
docs/actors/<slug>.md            the Actor's Console card and its publish record
.github/workflows/ci.yml         Linux, Python 3.11, PostgreSQL 16 service from phase 2
```

Each Actor has its own root because `apify push` reads `.actor/actor.json` at the Actor's root
(E-247, E-255). Its `actor.json` names every definition file explicitly (`input`, `output`,
`storages.dataset`, `readme`, `changelog`, `dockerfile`), so nothing depends on fallback paths
(E-247). The template is copied, not imported: three to five Actors do not justify a shared
library, and an Actor that imports nothing from the runtime cannot break when the runtime
changes (ADR-0009).

The phase-1 pull request adds `actors` to `codePaths` in `research/kit.json`, so a commit that
touches an Actor stages `docs/ARCHITECTURE.md` (AGENTS.md standing protocol, rule 1). That file
is project configuration, and the operator approves the change by merging. Tests and oracles
are not declared code paths.

## 9. Data model and migrations

DBOS owns and migrates its own tables in schema `dbos` (`run_migrations`, E-223). Their layout
is not in the corpus (U-40 residual), so our code reaches them only through the DBOS API
(`list_workflows`, `list_workflow_steps`, `cancel_workflows`, `resume_workflow`; E-228, E-231,
E-228 capture) and never by SQL.

Application tables live in schema `public` of the same database: one URL, one backup, one
restore point for workflow state and business state together. They use a SQL subset that both
SQLite and PostgreSQL 16 accept, so one set of migrations runs in both test lanes. Times are
UTC ISO-8601 text, money is integer micro-dollars, and JSON is text validated by Pydantic. App
storage uses SQLAlchemy Core. SQLAlchemy and psycopg 3 come with dbos (E-223), so this adds no
dependency; the day-one `uv pip check` confirms it.

| Table | Holds | Once-only key |
|---|---|---|
| `schema_version` | applied migration, file SHA-256, time | version |
| `control` | state (RUNNING, PAUSED, STOPPING, STOPPED), reason, requested_at, requested_by, swept_at | singleton |
| `breaker` | channel, state (CLOSED, OPEN), reason, opened_at, until (null means until the operator resets) | channel |
| `gate` | kind, subject, card JSON (evidence as data), evidence digest, handle, readiness id, deadline, state (PENDING, APPROVED, REJECTED, EXPIRED, SUPERSEDED) | gate ID (business key) |
| `gate_decision` | verdict, evidence digest, note, request id, channel (cli, api), decided_at | gate ID |
| `policy_decision` | action, verdict (allow, deny, needs_gate), rule ids, policy version, key | append-only id |
| `external_write` | channel, action, class (A, B, C), state (SENT, CONFIRMED, FAILED, UNKNOWN), attempts, request and result digests, policy version, workflow id (for reading only) | business key + step |
| `spend` | agent, provider, model, month, reserved and settled micro-dollars, token counts, price row used | business key + step |
| `actor` | slug, Apify name, public and twin Actor ids, published flag and time, event price, last released source digest | slug |
| `release` | slug, source digest, staged run id, verdict, state | release ID |
| `actor_health` | run id, status, item count, charged count, duration, verdict | (slug, date) |
| `research_readiness` | niche, package digest, preflight exit code, commit SHA, registered by | (niche, package digest) |
| `niche_lead` | Scout's typed lead (data), source, week | (week, lead digest) |
| `payout` | month, invoice USD, received ILS, paid date, note | month |
| `stop_report` | mode, requested_at, confirmed_at, cancelled workflow ids, writes in flight at timeout | id |
| `api_token` | SHA-256 of the token, created, revoked (phase 4) | id |
| `journal` | seq, time, origin (cli, api, worker), request id, method, input hash, reply digest, previous hash, hash | seq |

The **journal** records every CLI and API command, every gate decision, every control change,
every breaker change and every external write's final state. Each row's hash covers the
previous row's hash and the row's canonical JSON, so an edited or deleted row breaks the chain.
`kashmula journal verify` walks it (the Agent repository's tamper-evident logging rule, R13,
`docs/core/07-security-compliance.md`, used as an idea). The CLI and the worker both append; a
unique `seq` makes a racing insert fail and retry.

**Migrations** are numbered plain-SQL files in `src/kashmula/migrations/`. The worker applies
them at startup, before `DBOS.launch()`, one transaction each, and records each file's SHA-256.
It refuses to start if an applied file has changed or the database is at a newer version than
the code. Migrations are forward-only; undoing one is a new migration. Alembic is not used:
the project needs no branches or downgrades, and Alembic is not in the evidence.

## 10. Durable execution and idempotency

### 10.1 Configuration and rules

- `DBOSConfig`: `name="kashmula"`, `application_version` set to the git SHA baked into the
  image, `system_database_url` read from the environment and passed explicitly, because the
  corpus does not say DBOS reads it on its own (E-223, E-224; U-39 residual). The defaults for
  `dbos_system_schema` (`dbos`), `use_listen_notify` (fixed once the Postgres system database
  exists) and `run_migrations` are kept (E-223).
- Workflow code is deterministic. Database, network, random and clock calls go in steps
  (E-225, E-226).
- Workflow and step inputs and outputs are JSON-shaped primitives, validated into Pydantic
  models inside the function. DBOS pickles them (E-225) and agents' deps and outputs should stay
  under about 2 MB (E-237). A renamed class therefore cannot break the recovery of a run in
  flight.
- Every workflow has an explicit name with a version suffix, for example `release.v1`. Default
  names are `__qualname__` and must be unique (E-227). A workflow whose step sequence changes
  gets a new name, and deploys drain first (section 20), because changed code replaying an old
  run raises `DBOSStepNondeterminismError` (E-225).
- Expected failures return a terminal value (for example `{"verdict": "source_down"}`). An
  uncaught exception ends a workflow as ERROR and is never recovered (E-225), so ERROR always
  means a bug and raises an alert.
- Workflows that perform external writes use `max_recovery_attempts=5` instead of the default
  100 (E-227), so a crash loop stops early. `MAX_RECOVERY_ATTEMPTS_EXCEEDED` shows on the status
  board, and resuming resets the count (E-227).
- Step retries are off unless stated (E-226). Adapter steps are async with `timeout_seconds`,
  which applies only to async steps (E-226), and their clients carry their own timeouts as well.

### 10.2 Workflow IDs are business keys

Every workflow is started under `SetWorkflowID(key)` with the default `return-existing`
policy, so a repeated start returns the existing run (U-40; E-225, E-228). The keys are built
by `ids.py`: lowercase, parts without colons, digests cut to 12 hex characters.

| Workflow | ID | What makes it once-only |
|---|---|---|
| gate | `gate:<kind>:<subject>:<evidence12>` | one gate per subject and evidence |
| price-change gate | `gate:price:<slug>:<yyyy-mm>` | at most one price change per Actor per month (E-05, E-246) |
| release | `release:<slug>:<source12>` | one release per Actor source digest |
| health | `health:<slug>:<yyyy-mm-dd>` | one check per Actor per UTC day |
| ledger | `ledger:<yyyy-mm-dd>` | one settlement per day |
| digest | `digest:<yyyy>-W<ww>` | one digest per ISO week |
| scout | `scout:<yyyy>-W<ww>` | one Scout run per ISO week |

Lookups use the `workflow_id_prefix` filter of `list_workflows` (E-228 capture), not
attributes, which need a Postgres system database (E-231). The same code therefore runs on
SQLite in tests.

**Schedules.** Static schedules are declared at startup with `DBOS.apply_schedules`, with
`automatic_backfill` left at its default of off (E-228 capture), so an outage never replays a
burst of ticks. DBOS keys each tick by schedule name and time and runs it on exactly one
worker; cron is evaluated in UTC (E-52). A tick's function does one thing: it starts the
business workflow as a child under its business key. A tick, a backfill and a
`trigger_schedule` call (E-52 capture) for the same period therefore collapse into one run. A
day-one check confirms that a child started under `SetWorkflowID` from a scheduled workflow
returns the existing run.

### 10.3 Write intents and write classes

DBOS does not make an external write exactly-once: a step can run again until it completes
(E-225), and the operator's own rule asks for idempotency keys on every external write (E-54,
rule K35). Every external write therefore goes through one effects step (section 11), which
works in this order:

1. Run the guard.
2. Insert an `external_write` row in state SENT, in its own committed transaction.
3. Call the adapter with a timeout.
4. Record CONFIRMED or FAILED with the result digest.

No database transaction ever spans a network call.

The intent key is the **business key plus the step name** (for example
`release:fr-notices:3fa9c1d2e4b5/push_public`), never the workflow ID. `fork_workflow` gives
the copy a new ID (E-231), and a key built from the workflow ID would let a fork repeat a write
that already happened.

Each action in the closed action enum carries a class:

| Class | Meaning | First-wave actions | On re-entry with a SENT row and no result |
|---|---|---|---|
| B, repeat-safe | a repeat leaves the same end state | push an Actor source version (E-255); a field-scoped Actor update (E-254, which changes "only the fields specified") | repeat the call; DBOS step retries allowed, with `should_retry` excluding policy denials, spend signals and 401/403 |
| C, spend-only | a repeat costs money, nothing else | start a staged or health run; model requests | repeat at most once more, bounded by the budget reservation; attempts above one are shown on the status board |
| A, irreversible or customer-visible | a repeat is a visible duplicate | none in the first wave (publishing, prices, visibility and Store replies stay manual) | read the provider back; if the outcome cannot be determined, mark UNKNOWN and open an `unknown_write` gate; never repeat blindly |

The gateway refuses to register a class-A action whose adapter has no read-back method, and a
unit test enforces that. The first class-A action, a Support reply or an API price change,
cannot ship until its read-back endpoint is in the evidence (ADR-0004).

### 10.4 Recovery, proven by a test

A PostgreSQL 16 test runs the worker as a subprocess against a local fake Apify server. A crash
hook calls `os._exit` at a chosen point: before the adapter call, after it, or before the
result is recorded. The test restarts the worker and asserts exactly one CONFIRMED row per
intent key, with the fake server seeing no more calls than the class allows. The hook is inert
unless `KASHMULA_TEST_CRASH_POINT` is set and the database name starts with `kashmula_test_`.
The test observes the one-process recovery behaviour of U-40's residual. It does not turn that
behaviour into evidence, and a DBOS upgrade that changes it shows up as a red test.

## 11. Policy layer

### 11.1 Where the guard runs

`policy.guard(action)` is the **first statement of the same DBOS step** as the write it
permits. A guard in its own step would be checkpointed, and a completed step never runs again
(E-225, E-226), so after a STOP a recovered workflow would replay a stale permit. Inside the
write step, a retried or recovered step checks again.

The guard returns a `Permit`. Adapters accept a write only with a `Permit`, and only `guard`
can construct one. Agents' tools never call the network for writes: they return typed proposals
from the closed action enum. An import-boundary test fails if any module outside `effects/`
imports a network client, or if `agents/` imports `adapters/`. A unit test fails if a `Permit`
can be built outside `guard`. Both are paired with their guards in `tests/guards.toml`.

### 11.2 Order of checks

1. **Control state.** Writes are refused in STOPPING and STOPPED (section 14).
2. **Breaker.** Refused while the channel's breaker is OPEN.
3. **Action allowlist.** The first wave allows `apify.push_version`, `apify.start_run`,
   `apify.read_run` and the model-run admission. There is no pricing, permission, visibility or
   delete action.
4. **Rules** (11.3).
5. **Rate cap** per channel, counted in `external_write` over a window and serialized by an
   in-process lock per channel. The lock is valid because exactly one worker exists (ADR-0003).
   The corpus gives no Apify rate limit, so the caps in `policy.toml` are conservative
   assumptions.
6. **Budget** for spend actions (section 12).
7. **Idempotency.** An existing CONFIRMED intent returns its stored result.

Every decision writes a `policy_decision` row with its rule ids and the policy version. A
denial raises `PolicyDenied`, which no step retries.

**Model calls.** Model requests inside `agent.run()` are steps generated by `DBOSDurability`
(E-237), so the guard cannot sit inside them. They are governed by an admission step before
each run, which checks the control state and the breaker and makes the budget reservation. The
run carries `UsageLimits` (E-233). A cancel interrupts the run at its next model step (E-228).
The provider spend limit is the backstop (E-43).

### 11.3 The rules

| Rule | Enforced where | Evidence |
|---|---|---|
| No niche in mass messaging, engagement, review or SEO manipulation | readiness registration and niche-gate creation | E-09; E-40 (spam, fake reviews); PLAN section 4 |
| No link to or promotion of anything off the platform in the README or description | template checker; release check | E-05 |
| Pay per event only; "pay per event + usage" never switched on; limited permissions; no Standby | template checker (`usesStandbyMode` absent); Console card checklist | E-10, E-246, E-251; E-08 (passing usage costs lowers the quality score) |
| One per-item charging mechanism: the synthetic dataset event; no `Actor.charge(` or `charged_event_name=` in Actor code | template checker | E-245, E-246; ADR-0010 |
| Event price at least the platform cost per result divided by 0.8 | Console card; price-change gate | E-06 |
| Price increases and new paid events at most once a month, effective after 14 days, uncancellable; decreases immediate | `gate:price:<slug>:<yyyy-mm>`; changes made in Console | E-05, E-246 |
| A niche approval needs a readiness record whose preflight exit code is 0 and whose package digest matches the gate's evidence | gate service | Operate spec |
| No account creation; one credential per platform, read at boot; a 401 or 403 opens that platform's breaker and a `credential` gate; no code path loads another credential | config loader; adapters | E-40, E-87 |
| No refund-denying action exists for any agent | action enum | E-86 |
| AI disclosure opens any customer-facing message (none in the first wave; binding when Support returns) | action enum: no messaging action yet | E-40 |
| External content reaches agents only as tool data; Scout has no write tool | agent definition; injection test | U-30; Operate spec ("Evidence shown on a card is data") |

### 11.4 Where the rules live

The rules, allowlists, rate caps and gate deadlines live in `config/policy.toml`. The policy
version is the first 12 hex characters of the SHA-256 of that file's canonical content, and
it is recorded in every decision and journal row. The runtime cannot change its policy: a
change is a pull request the operator merges. That merge is the "changes to the policy itself"
gate of PLAN section 4.

## 12. Budgets and stop signals

**Layer 1: provider limits, set once by the operator.** An Anthropic organization spend limit
below the Start tier's $500 cap, and one Workspace per agent with its own limit (E-43). In the
first wave there is one agent, so one Workspace (`scout`). Another is added only when a second
agent returns. These caps hold even if the local ledger or price table is wrong.

**Layer 2: per-run limits.** Every `agent.run()` carries `UsageLimits` with `request_limit`,
`tool_calls_limit`, `input_tokens_limit`, `output_tokens_limit` and `cost_limit`, from
`config/budgets.toml`. A breach raises `UsageLimitExceeded` (E-233; U-44) and ends the workflow
with the verdict `budget_exhausted`, never retried. `cost_limit` is "not a hard billing
guarantee" (E-233), so it is a guard, not the ceiling.

**Layer 3: the reservation ledger.** Before each run, the admission step reserves the run's
worst case:

> `input_tokens_limit` × input price + `output_tokens_limit` × output price

It uses the `prices.toml` row in effect today (E-42 for Claude prices; prices carry effective
dates because they change, as E-47 shows). The reservation is checked atomically against the
agent's monthly cap, the provider cap and the global cap, each set at 80% of the matching
provider limit (an assumption). The `spend` row is keyed by business key plus step, so a
recovered step cannot reserve twice; the counter lives in Postgres, per workflow, not in a
process global (the DROPSCRAP lesson, `serpapi.py`, read at `f200c11`). After the run a step
settles the actual cost from the run's usage. How a result exposes `RunUsage` is a day-one
check. A reservation that a crash leaves unsettled stays counted at its maximum, so the ledger
never under-counts. Reaching the global cap triggers an automatic STOP with that reason
(section 14).

**Stop signals.** A provider response of HTTP 429 at the tier cap opens the `anthropic` breaker
until 00:00 UTC on the first of the next month. HTTP 400 `invalid_request_error` at a self-set
limit opens it until the operator resets it (E-43). Neither is retried, because retries fail
until access resumes (E-43). Both open a `breaker` gate card whose choices are to raise the
limit in Anthropic Console and run `kashmula breaker reset anthropic`, or to wait.

**Retries.** The Anthropic client is built with `max_retries=0` and passed as
`anthropic_client=`, so the SDK does not retry on its own (E-235, E-237). Model steps get no
`StepConfig`, which means no retries (E-237). A failed Scout run is recorded and the next weekly
tick tries again. The U-44 day-one test records which exception classes a 429, a 500 and a 400
raise, so the breaker classifier matches the right ones (U-44 is KNOWN-UNKNOWN until then).

**Platform and fixed costs.** Own test and health runs come out of the Creator plan's bonus
usage (E-13). Run usage is read from the Apify run API once phase 1 collects it. The Fly.io
Machine (E-49) and Postgres hosting are fixed monthly lines in `budgets.toml`. `kashmula status`
and `GET /v1/status` show month-to-date spend against every cap and against the 200-1,000 USD
budget.

## 13. Operator approval surface and the Operate-mode contract

### 13.1 Gates in the first wave

| Kind | Opened by | Approve means | Unanswered by the deadline |
|---|---|---|---|
| `niche` | readiness registration (section 15.4), once the runtime is deployed; before that, the niche is approved in its pull request | the niche may be built as an Actor pull request | expires; nothing is built |
| `price` | the ledger workflow's price recommendation | the operator makes the change in Console (U-51) and the month's key is spent | expires; the price stays |
| `breaker` | a provider spend signal (section 12) | the operator raised the limit; the breaker closes | the breaker stays open until its `until` time |
| `credential` | a 401 or 403 from a platform | the operator replaced the credential in the environment; the breaker closes | the channel stays closed |
| `unknown_write` | a class-A write with an undeterminable outcome (none in the first wave) | the operator confirms what happened | the write stays UNKNOWN |

No first-wave gate causes an external write by itself. Approving records the decision; the
action it allows is either manual (Console) or a later admitted workflow.

### 13.2 The gate workflow

A gate is a workflow under `gate:<kind>:<subject>:<evidence12>`. Its first step writes the
`gate` row with the card. The `gate` and `gate_decision` rows are the record of truth. A DBOS
message only wakes the workflow. The workflow then loops:

1. A step reads the decision and the clock.
2. If the gate is decided or past its deadline, the workflow records the outcome and returns.
3. Otherwise it waits on `DBOS.recv(topic="wake", timeout_seconds=3600)`, which returns
   `None` on timeout (E-228).

When the deadline passes, the gate becomes EXPIRED and nothing happens. The Operate spec leaves
the meaning of an unanswered gate to the runtime ("for KashMula: nothing is published"), and
the Agent repository's approval rule is default deny on timeout (`docs/core/08-ux-product.md`,
used as an idea). Gate deadlines per kind are in `policy.toml`. New evidence for the same
subject opens a new gate, and the old one becomes SUPERSEDED.

### 13.3 Decisions

`gates.service.decide(gate_id, verdict, evidence_digest, note, request_id, channel)` runs in one
transaction:

1. Check that the gate is PENDING and that the digest matches the gate's current evidence
   digest.
2. Insert the `gate_decision` row (primary key `gate_id`).
3. Set the gate's state.
4. Append the journal row.

Repeating the same decision with the same digest returns the recorded decision, marked as a
repeat. A different digest, a different verdict after a decision, or a decision on an expired
gate is refused. These are the Operate contract's rules: idempotent by gate id and digest, and
a second decision with a different digest refused.

**Waking the gate.** The API path calls
`DBOS.send(<gate workflow id>, "wake", topic="wake", idempotency_key=<request id>)` from plain
Python, which is allowed with an idempotency key (E-228, E-230). The CLI path sends the same
wake through `DBOSClient` if a phase-2 check confirms its send signature. The DBOS Client can
send (E-230), but its signature is not captured. Otherwise the gate picks up the decision at its
next timeout, within an hour. Gate decisions are never time-critical in the first wave.

### 13.4 The weekly digest and one-line cards

`digest:<yyyy>-W<ww>` runs on Monday mornings UTC. It composes one view:

- the pending gates;
- each Actor's health for the week;
- spend against caps;
- Scout's niche leads;
- reminders (the Apify invoice on the 11th, Store issues not yet answered);
- the week's human touches with estimated minutes.

Each gate is one card: what is asked, the recommendation, the evidence digest, the deadline,
and the default ("if unanswered: nothing happens"). Each card has a handle that carries the
digest, for example `k7q2-3fa9c1`, and is answered with one line:

```
kashmula approve k7q2-3fa9c1
kashmula reject  k7q2-3fa9c1 "source terms forbid resale"
```

A handle whose digest part no longer matches the gate's evidence is refused, so a decision is
always bound to what the operator saw. In phases 2 and 3 the digest is read with
`kashmula digest`. From phase 4 it also goes to the alert channel chosen in phase 4's research,
and it is on the status board.

### 13.5 CLI first

The phase-2 CLI covers:

- `status` and `digest`;
- `gates`, `approve` and `reject`;
- `stop`, `pause` and `resume [--workflows]`;
- `breaker reset <channel>`;
- `actor check|card|confirm-published|list`;
- `research register`;
- `payout record`;
- `leads`;
- `journal verify`.

`kashmula worker` starts the worker. The CLI and the phase-4 API call the same functions in
`gates/service.py`, `control/state.py` and the status query, so the two surfaces cannot drift.

### 13.6 Operate API v1 (phase 4)

The contract is the Operate spec's table. The Pydantic models are written in
`src/kashmula/contracts.py` and frozen in phase 2, and they are mirrored in
`docs/contracts/operate-api.md` so Moonzila and KashMula build to one document.

| Method and path | Served by | Notes |
|---|---|---|
| `GET /v1/approvals?state=pending` | pending `gate` rows | each card: id, handle, kind, summary, recommendation, evidence (data), evidence digest, readiness, deadline |
| `POST /v1/approvals/{id}/decision` | `decide()` then the wake | body: verdict, evidence digest, note, request id; a repeat is answered as a repeat; a digest or verdict conflict is refused |
| `GET /v1/status` | the status query | control state and stop reason, spend against every cap, breakers, last run per workflow and agent, Actor health, payout status, human touches per week; cost per 1,000 results and paid users are null with the reason "not collected" until the Apify analytics API is in the evidence |
| `POST /v1/stop` | the stop path (section 14) | body: mode (`stop` or `pause`), reason, request id; returns the confirmed state, or STOPPING with the writes still in flight |
| `GET /v1/proposals?state=pending` | none in the first wave | returns an empty list; first-wave code changes are pull requests on GitHub, the reviewed edit the Operate spec requires |
| `POST /v1/proposals/{id}/decision` | none in the first wave | refuses unknown ids |
| `GET /v1/research/{jobId}` | `research_readiness` | package digest, preflight exit code, commit SHA |

Every call is journaled with the request id, method, input hash and reply, as the Operate spec
asks. The bearer token is created by `kashmula api token create`, shown once and stored only as
a SHA-256 hash. The HTTP framework, TLS and ingress are phase-4 research (section 20).

## 14. Kill switch

Disabling a trigger does not stop a system (E-87). The kill switch is coupled to the loop: a
control state that every admission and every write reads, plus a sweep that pauses the
schedules and cancels the work in flight.

**Modes.**

- **PAUSE** closes admissions and pauses business schedules, and lets running workflows finish,
  including their writes. It is used to drain before a deploy.
- **STOP** is the emergency mode. From the moment it commits, every guard refuses every write.

**STOP, step by step** (`kashmula stop` or `POST /v1/stop`):

1. One transaction sets `control` to STOPPING with the reason and appends the journal row.
   Admissions close at once: each workflow's first step and every guard read the state.
2. The stop watcher, a thread in the worker that wakes every 5 seconds and at startup, pauses
   every business schedule with `DBOS.pause_schedule`. `apply_schedules` keeps that status
   across restarts (E-228 capture).
3. It calls `DBOS.cancel_workflows(ids, cancel_children=True)` on every ENQUEUED, DELAYED and
   PENDING workflow except gate workflows, which only wait and read (E-228 capture). A running
   workflow is interrupted at its next step and a queued one is dequeued (E-228, E-231; U-42).
4. It waits until no `external_write` row is still SENT, that is, until every write that passed
   its guard has a result. Each such write is bounded by its adapter timeout.
5. It repeats the sweep until nothing is left. Late starts meet the admission step.
6. It writes `swept_at`, sets STOPPED, and writes a `stop_report` with the cancelled ids.

The CLI waits up to 120 seconds and then prints either `STOPPED (confirmed <time>)` or
`STOPPING: <n> writes in flight, <m> workflows left`. Nothing reports STOPPED before `swept_at`
is written after the request. If the worker is down, the CLI records the request and says that
no worker has confirmed it; the worker performs the sweep at startup before it starts the
watcher.

**What STOP does not stop.**

- A model request or write already past its guard completes, because cancellation takes effect
  at the next step (E-228). STOP waits for such writes instead of hiding them.
- Customers' runs on Apify continue. Withdrawing a public Actor (`isPublic=false`, E-254) is an
  operator action in Console, not part of STOP.

**RESUME** is operator-only. `kashmula resume` sets RUNNING and resumes the schedules
(`resume_schedule`, E-228 capture). Cancelled workflows stay cancelled, because the cause of
the stop may still be present. `kashmula resume --workflows` also calls `resume_workflow` on
each id in the last stop report, which restarts each from its last completed step (E-228), and
each meets the guard again. Restarting a cancelled business key with a new start would only
return the cancelled run (E-225).

**Automatic stops.** Reaching the global monthly spend cap triggers STOP with that reason.
Provider spend signals and credential rejections open that channel's breaker instead
(section 12). Queue limits are never used to stop anything: there are no queues of our own
(U-41), and limits at zero are not described.

## 15. Actor production, testing and publishing

### 15.1 What an Actor is here

An Actor is deterministic Python that reads a lawful public source within a per-run request
ceiling and pushes typed result items. It makes no model call at run time. That keeps its output
outside the AI-content duties of E-40, keeps its platform cost low (usage is netted from the 80%
share, E-06), and keeps the daily test well inside five minutes (E-256). Python, not
JavaScript: the template, tests and pins are Python (U-38, U-47), and only JavaScript samples
exist for some platform features (E-252).

### 15.2 The template (U-47, U-49, U-50)

- **Lifecycle:** `async def main()` under `asyncio.run(main())`, with the work inside
  `async with Actor:` (E-239, E-240). Unhandled errors exit 91 (E-240).
- **Input:** `await Actor.get_input() or {}`, validated by a Pydantic model with
  `alias_generator=to_camel`. Bad input ends the run with
  `await Actor.fail(status_message=...)` (E-241, E-242). The platform also validates input
  against the schema before a run starts (E-248).
- **Source:** one injectable fetch function built on the standard library, with a request
  ceiling per run, a timeout and per-source failure isolation. This is ported as a design from
  `search-light-signals`, not as code (section 21).
- **Output:** `await Actor.push_data(item)` for result items only. Error items never enter the
  default dataset, because every item there is charged (E-245). Items are deduplicated within a
  run by a stable item id.
- **Charge limit:** the `ChargeResult` from `push_data` is checked for
  `event_charge_limit_reached`, which already accounts for the user's
  `ACTOR_MAX_TOTAL_CHARGE_USD` (E-244, E-245). When it is set, the Actor stops cleanly.
- **Abort:** an `Event.ABORTING` handler flushes and exits; the platform force-stops 30 seconds
  after it sends the event (E-245).
- **Run summary:** the Actor writes items pushed, the summed `charged_count` and whether the
  limit was reached to its default key-value store.
- **Definition files (U-49):**
  - `actor.json` with `actorSpecification` 1, name, version, title and every optional file
    reference (E-247);
  - an input schema with title, `type` object, `schemaVersion` 1 and `properties`, where every
    field has type, title and description, an editor for string, object and array, an `example`,
    and a small `prefill` (E-248);
  - the output schema that Store publishing requires (`actorOutputSchemaVersion` 1, title, and
    properties each with title and template, E-249);
  - a dataset schema with fields and at least one table view (E-250);
  - a README with no external link (E-05) and a CHANGELOG.
- **Permissions (U-50):** default storages only, so limited permissions need no changes
  (E-252). New Actors default to limited permissions (E-251). No `usesStandbyMode` (E-10).
- **Dockerfile:** its base image and contents are not in the corpus. Phase 1 collects the Apify
  Python Actor template and Dockerfile pages with Research-Kit before writing it.

### 15.3 Charging (U-48)

Each Actor has one per-item charging mechanism, the synthetic `apify-default-dataset-item`
event. It is on by default, charges every default-dataset item, and needs no charging code
(E-245). A custom event would need the synthetic event deleted in Console (E-246). Whether both
would charge one push is unknown (U-48 residual), so a missed deletion could bill a customer
twice. The template checker fails on `Actor.charge(` and `charged_event_name=`.

Local test mode logs explicit charge calls (E-244), and the synthetic event makes none, so the
local guard tests **what is charged**: the default dataset holds only valid, deduplicated
result items, and the prefill input yields a non-empty dataset. What
`ACTOR_TEST_PAY_PER_EVENT=true` logs for the synthetic event is recorded by a day-one check and
kept as a pinned observation, not used as the guard.

The revenue path is proven on the platform. The first run after the operator sets up
monetization must show a summed `charged_count` equal to the items pushed in the run summary
(E-245: `push_data` returns a `ChargeResult` under the synthetic event). That run is a private
run if Console allows monetization before publishing, and otherwise the first health run after
publishing. A mismatch blocks further releases and raises an alert.

### 15.4 How each Actor is produced

- **Actor 1 (phase 1, no runtime yet).**
  1. The phase opens with a Research-Kit package for a short list of niches, including each
     source's terms of use (U-24 is open for the Federal Register and CSMS). A source whose
     terms are not captured as allowing commercial use does not enter the short list.
  2. The operator approves one niche in the pull request.
  3. A builder sub-agent fills the template from the approved niche and recorded source
     responses, under the `lead-orchestrator` skill.
- **Actors 2 to 5 (after phase 1's merge, whenever the operator asks for one).** Each is one
  pull request on its own branch, never mixed into a phase pull request, from a coding-agent
  session the operator starts, built from the template.
  1. The first commit is the niche's Research-Kit package at preflight PASS, drawing on
     Scout's leads.
  2. Before phase 4, the session asks for the niche approval in the pull request. From phase 4
     it registers the readiness record (`kashmula research register`, which records the package
     digest, the preflight exit code and the commit) and the runtime opens a `niche` gate.
  3. The Actor is built only after the approval.
- **Repairs** are pull requests in the same way. There is no runtime Builder (ADR-0002).

The runtime never collects research. AGENTS.md reserves collection for the collector machine,
and the runtime is a builder-role host.

### 15.5 Tests and the hidden oracle

Local tests:

- Each test sets `SmartApifyStorageClient(local_storage_client=MemoryStorageClient())` in the
  service locator before entering the Actor context (E-243). Nothing is written to disk.
- Input comes from patching `Actor.get_input` with an `AsyncMock`. The first Actor test
  confirms this works (U-47 residual).
- Source responses are recorded once from the live source within the request ceiling and
  replayed with the network blocked.
- The assertions check:
  - items validate against the dataset schema's fields;
  - no error items and no duplicates;
  - the prefill input read from `input_schema.json` yields a non-empty dataset in well under
    five minutes (E-256);
  - bad input ends the run as failed through `Actor.fail` (E-242);
  - the request ceiling holds;
  - the charge-limit branch exits cleanly, with `push_data` substituted at the SDK boundary.

**The hidden oracle** follows WindowRunner's pattern (Apache-2.0, ported as a pattern, read at
`b50ff36`):

1. Before the build, a separate sub-agent writes `check.py` from the niche spec and the
   recorded responses.
2. The lead holds it outside the builder's worktree.
3. A build passes only if the oracle exits 0 and the Actor run finishes successfully.
4. After the build the oracle is committed under `qa/oracles/<slug>/` as a regression test.

**The template checker** (`kashmula actor check actors/<slug>`) enforces:

- E-247's required fields;
- E-248's schema rules, including the 500 kB limit and no `patternKey` or `patternValue`;
- E-249's output schema and E-250's views;
- no `usesStandbyMode` (E-10);
- no external link in the README (E-05);
- one charging mechanism (ADR-0010);
- a title, a prefill input and a CHANGELOG.

The checker runs on `actors/_template` too.

### 15.6 Staging and the first publish: what stays manual, and why

The push and the private runs need the operator's Apify token. They run from the development
environment with `APIFY_TOKEN` set for that session only, never in the repository and never in
CI, by the agent at the operator's request or by the operator. `apify push` creates or updates
the Actor named in `actor.json` and builds it (E-255).

Staging a new Actor means at least two private runs with the prefill input, at least 24 hours
apart, one of them with permissions forced to limited (`forcePermissionLevel`, E-252). Each
must finish SUCCEEDED with a non-empty default dataset within five minutes, the criteria of
Apify's daily test (E-256).

Then the operator publishes and prices in Console, in one sitting.

| Step | Manual because | Evidence |
|---|---|---|
| Identity verification and payout method | KYC needs a person and an ID photo | E-04, E-05 |
| First Store publish | publishing is described only as a Console flow with required sections; the CLI has no publish command; API error codes such as `store-terms-not-accepted` point to Console-only prerequisites | U-51; E-253, E-255, E-254 |
| Monetization and first price | needs billing and payout details first; events and prices are set in Console | U-48, U-51; E-246 |
| Permission level check | shown only in Console | U-50; E-251 |
| README review | generated content published externally needs human review; the operator also reviewed it in the pull request | E-40 |
| Price changes | Console until a call on a throwaway private Actor with no paying users shows `pricingInfos` works without Console prerequisites | U-51; E-254, E-246 |

In the same sitting the operator sees what the definition files of U-49 produce: the input form
built from the input schema (E-248), the sample output, and the Output tab built from the output
schema (E-249).

### 15.7 The Console card

`kashmula actor card actors/<slug>` writes `docs/actors/<slug>.md`, a paste-ready checklist:

- title, categories, description and the README to check;
- sample output and the output schema;
- permission level: limited;
- source files hidden (the default, E-253);
- monetization: pay per event, keeping `apify-default-dataset-item` as the per-result and
  primary event (E-246), adding no custom per-item event, and leaving "pass platform usage costs
  to users" off (E-10, E-246, E-08);
- the recommended event price with the floor computation: measured compute units per result
  times $0.20, the Bronze-tier unit cost and the highest (E-06), divided by 0.8 (E-06);
- the `apify-actor-start` choice, which covers the first 5 seconds of compute (E-08).

The operator closes the sitting with
`kashmula actor confirm-published <slug> --actor-id <id> --price <usd>`, which records the
`actor` row and a journal row. Before phase 2 creates the registry, the confirmation is recorded
in the card file and loaded into the registry by the phase-2 pull request. The operator also
records the hours until the Actor appears in Store search, which answers U-33 for this account.

An Actor that meets these rules (pay per event, no "+ usage", limited permissions, no Standby,
operator KYC done) becomes available to agentic buyers automatically (E-10).

### 15.8 Releases after the first publish (phase 3)

A merged change to `actors/<slug>/` reaches Apify through `release:<slug>:<source12>`, started
by the worker when the deployed image carries a source digest the registry has not released:

1. Push the source to a private twin Actor. The twin is a copy of the Actor directory whose
   `actor.json` name carries a `-staging` suffix, which `apify push` creates or updates (E-255);
   a non-public Actor is visible only to its owner (E-254).
2. Start a staged run with the prefill input and permissions forced to limited (E-252).
3. Check SUCCEEDED, a non-empty dataset, no error items, the run time, and the run summary.
4. Push to the public Actor.
5. Record the release.

A failed check refuses the release. The Apify endpoints for starting a run, reading its status
and dataset, and the CLI's installation are not in the corpus; phase 1 collects the run and
dataset pages and phase 3 collects the rest before coding the adapter.

A release does not wait 48 hours. A repair must beat the three-day clock of E-256, and the daily
health check below plays the role PLAN section 4 gave the 48-hour stage (ADR-0011).

### 15.9 Daily health and the repair fast path

From phase 3 (live in phase 4), `health:<slug>:<date>` runs each published Actor once a day
with its prefill input and checks Apify's criteria: SUCCEEDED, a non-empty default dataset,
within five minutes (E-256). It also checks the run summary. The first failure raises an alert
and a repair item in the digest and on the status board, two days before Apify's "under
maintenance" label.

A repair pull request that leaves the README, schema and price digests unchanged is marked
fast-merge with a 48-hour merge target, because the operator's merge is the critical path until
a Builder returns. Through phases 2 and 3, before the runtime is deployed, Apify's own test and
its notification after three failed days are the monitor (E-256).

### 15.10 Prices

The first price is the operator's, from the card. After that, the daily ledger workflow compares
each Actor's measured cost per result with its price. Below the floor, it opens a
`gate:price:<slug>:<yyyy-mm>` card recommending an increase, at most one per Actor per month
(E-05, E-246). A decrease takes effect at once (E-246) and is recommended in the digest. Both
are made by the operator in Console in the first wave.

## 16. Agents

### 16.1 The first-wave roster

| PLAN agent | First-wave form | Phase | Human gate | Budget |
|---|---|---|---|---|
| Scout | Pydantic AI agent under `DBOSDurability`, weekly, read-only tools on an allowlist of public sources; returns typed niche leads | 3 | none on its run; its leads feed niche research, and the niche approval is the gate | per run: `request_limit` 15, `tool_calls_limit` 30, `input_tokens_limit` 200,000, `output_tokens_limit` 16,000, `cost_limit` $0.50; monthly cap $5; Workspace `scout` with its own limit (assumed values) |
| Builder | cut: Actors 2 to 5 and repairs are coding-agent pull requests | returns by ADR-0002's trigger | the operator's review and merge | the coding-agent session, outside the runtime |
| QA | deterministic: the CI gate (tests, template checker, hidden oracle, prefill mirror), staged release runs, daily health | 1, 3 | a failed check refuses the release | platform runs from the Creator bonus usage (E-13), metered once the run API reports usage |
| Publisher | split: first publish and first price by the operator from the Console card; releases by the release workflow; price recommendations by the ledger workflow | 1, 3 | first publish and price (U-51); price increases through the `price` gate | none (no model) |
| Support | deferred: the operator answers Store issues within 14 days (E-05 capture, clause 8.1) and Apify's direct requests within three business days (clause 8.2) | returns by trigger | escalations | not applicable |
| Finance | deferred as an agent: the deterministic ledger workflow meters model spend, run usage and fixed costs, holds payouts the operator records, and tracks the 2026 osek patur ceiling of about 122,833 NIS from received ILS (E-213, E-216) | 2, 3 | the monthly invoice reminder on the 11th; Apify approves automatically on the 14th (E-04 capture) | none (no model) |
| Compliance | the policy module, not a model (section 11) | 2 | changes only by a merged pull request | none |

The Scout model is named in `budgets.toml`. The assumed default is Claude Haiku 4.5 at $1 input
and $5 output per million tokens (E-42), so the per-run worst case is $0.20 + $0.08 = $0.28.
Scout's fetch tool is a `@DBOS.step` because it does I/O (E-237, E-238). It honours the host
allowlist and a per-run request ceiling, and it checks the control state. Scout's sources are
collected with Research-Kit at the start of phase 3. A test feeds Scout, under `FunctionModel`,
a recorded listing that carries injected instructions and asserts that the output is still only
typed leads and that no tool outside the read-only set exists or is called.

### 16.2 How agents run durably (U-46)

Each agent is built before `DBOS.launch()`, has a unique `name`, and is given
`capabilities=[DBOSDurability()]`. Our own `@DBOS.workflow` calls `agent.run()` (E-237). Model
requests and MCP calls become DBOS steps (E-237). `DBOSAgent` is never used: it is deprecated
and removed in v3 (E-237).

The import path of `DBOSDurability` and the fields of `StepConfig` are U-46 KNOWN-UNKNOWNs,
answered by the day-one check. If `DBOSDurability` fails that check, each whole `agent.run()`
goes inside one `@DBOS.step`, which may hold arbitrary I/O (E-226). A crash then repeats one
run, bounded by `UsageLimits` and the reservation.

### 16.3 Human touches, measured

| Touch | What keeps it human | Frequency | Minutes (assumed, in `budgets.toml`) |
|---|---|---|---|
| Read the weekly digest | this design | weekly | 5 |
| Approve a niche (card, or pull-request comment before phase 4) | PLAN sections 4 and 7 | at most monthly | 2 |
| Start an Actor session; review and merge its pull request | ADR-0002; the operator merges (BUILD.md) | per new Actor, at most 4 in the first wave | 30 |
| First publish and price in Console from the card | U-51; E-253, E-246, E-40 | per new Actor | 15 |
| Merge a repair pull request (fast path) | the Operate spec's reviewed edit; ADR-0011 | when a source breaks | 10 |
| Change a price in Console after a `price` card | E-05, E-246; U-51 | at most monthly per Actor | 5 |
| Answer a Store issue | E-05 capture, clause 8.1 (14 days) | as issues arrive | 10 each |
| Answer a direct request from Apify | E-05 capture, clause 8.2 (three business days) | rare | 10 |
| Raise a provider limit or replace a credential | E-43, E-87 | rare | 5 |
| Review the monthly Apify invoice; record the payout | PLAN section 7; E-04 capture | monthly | 5 |
| Merge a phase pull request | BUILD.md | per phase, during the build only | not counted |

Each touch done through the CLI or API is journaled with its kind. Console and email touches are
recorded with `kashmula payout record`, `kashmula actor confirm-published`, or a touch note.
`kashmula status` shows the weekly sum against one hour.

## 17. Testing strategy and the quality gate

### 17.1 Lanes

| Lane | What it covers | Database |
|---|---|---|
| `unit` | ids, policy rules, guard and `Permit`, ledger arithmetic, cards, the checker, migrations' SQL subset | SQLite or none |
| `dbos_sqlite` | workflows under the `reset_dbos` fixture: `DBOS.destroy()`, `DBOS(config=...)` with a SQLite URL under `tmp_path`, `DBOS.reset_system_database(truncate=True)`, `DBOS.launch()` (E-232; U-43); idempotent starts, gates, the schedule-child rule | SQLite |
| `pg` | listen/notify wakes (E-223), the stop sweep and the in-flight wait, the watcher thread's DBOS calls, CLI and worker racing on decisions and the journal, migrations on PostgreSQL 16, the shared database with schema `dbos` | PostgreSQL 16, one database per builder (`kashmula_test_<builder>`) |
| `recovery` | the crash-injection test of section 10.4 | PostgreSQL 16 |
| `actors` | each Actor's tests, the template's tests, the oracles | none (memory storage) |
| `dayone` | the pinned behaviour checks of 17.3 | SQLite |

Models are swapped with `agent.override(model=TestModel())` or `FunctionModel(...)`, and
`models.ALLOW_MODEL_REQUESTS = False` is set in `conftest.py` (E-236; U-45). A socket guard in
`conftest.py` refuses every non-loopback connection, so no test reaches the network.

### 17.2 Rules every phase follows (lead-orchestrator)

- **A new test fails with the guard it names removed, on its own input.** Each guard and its test
  are listed in `tests/guards.toml` (guard id, file and symbol, test node id, input). A unit test
  checks that every listed symbol and test exists. In each phase the mutation auditor removes
  each new guard and runs its named test alone; the test must fail. A test that stays green is
  an S1 finding, whatever else catches its input.
- **Repeats.** Approval and kill-switch tests are marked `repeat30` and run 30 times in a row;
  any failure is a defect (BUILD.md):
  `for i in $(seq 30); do uv run pytest -q -m repeat30 || exit 1; done`.
- **Filesystem tests hold on every CI platform.** They write only under `tmp_path`, create no
  links (the product creates none), use no fixed host path, and assert on real paths, never on
  a link's stored text.
- **CI legs.** CI has one leg: Linux, Python 3.11, with a PostgreSQL 16 service from phase 2.
  This container reproduces it, so no leg holds the merge. If the operator adds a leg this host
  cannot run (Windows or macOS), that leg holds the merge until it is green.
- Real collaborators over mocks. Substitution happens only at the network boundary (the fake
  Apify server, recorded source responses, `FunctionModel`) and at the SDK charging boundary.
- Never weaken, skip or delete a test to get a pass.

### 17.3 Day-one checks (the first unit of phase 1, kept in `tests/dayone/`)

1. **U-38:** install the three pins together on Python 3.11 and run `uv pip check`.
2. **U-46:** inspect `DBOSDurability` and `StepConfig` in a REPL and record their import paths
   and fields in the pull request. Then a SQLite test runs an agent with `DBOSDurability` and a
   registered model inside a `@DBOS.workflow`, including whether `agent.override(model=TestModel())`
   and `FunctionModel` are accepted. `DBOSDurability` raises `UserError` for an unregistered
   model instance (E-237; U-45 residual). If the check fails, the fallback of section 16.2
   applies and the phase-3 design says so.
3. **U-44:** a stub `http_client` returns 429 (a spend-cap body), 500 and 400
   (`invalid_request_error`) through `AsyncAnthropic(max_retries=0)` as `anthropic_client`. The
   test counts attempts and records the exception classes, which become the breaker
   classifier's allowlist.
4. How a run result exposes `RunUsage`, for ledger settlement.
5. A child workflow started under `SetWorkflowID` from a scheduled workflow returns the existing
   run on a repeat.
6. `cancel_workflows`, `pause_schedule` and `list_workflows` work from a plain thread (SQLite
   here; repeated in the `pg` lane in phase 2).
7. **U-47 residual:** `Actor.get_input` patched with an `AsyncMock` feeds the Actor.
8. What `ACTOR_TEST_PAY_PER_EVENT=true` logs for the synthetic dataset event (E-244), recorded as
   an observation.

They stay in the suite, so a dependency bump that changes pinned behaviour turns CI red instead
of failing in production. Phase 2 adds one more: the `DBOSClient` send signature for the CLI
wake (E-230).

### 17.4 Phase-1 quality gate (run in order)

| Step | Command |
|---|---|
| Research gate | `node "$HOME/.agents/research-kit/bin/preflight.mjs"` (exit 0) |
| Kit health | `node "$HOME/.agents/research-kit/bin/doctor.mjs"` (ends with `READY`) |
| Install | `uv sync --locked --python 3.11` |
| Dependencies resolve | `uv pip check` |
| Lint | `uv run ruff check .` and `uv run ruff format --check .` |
| Types | `uv run mypy src/kashmula` and `uv run mypy actors/<slug>/src` for each Actor |
| Actor rules | `uv run kashmula actor check actors/_template` and `uv run kashmula actor check actors/<slug>` |
| Tests | `uv run pytest -q tests actors/_template/tests actors/<slug>/tests qa/oracles` |
| Actor image | `docker build -f actors/<slug>/.actor/Dockerfile actors/<slug>`, once phase 1's research has settled the base image |

Phase 2 adds `KASHMULA_TEST_PG_URL=postgresql://localhost/kashmula_test_<builder> uv run pytest -q -m "pg or recovery"`
and the 30-run loop above. The phase records every command and its baseline in the AGENTS.md
Orchestrator facts.

## 18. Observability

- **Run log:** DBOS workflow and step history (`list_workflow_steps`, `dbos workflow list` and
  `steps`, E-231).
- **Business log:** `external_write`, `policy_decision`, `spend`, `gate`, `actor_health`,
  `release` and the hash-chained `journal`.
- **Process log:** standard-library JSON logs on stdout, each line carrying the workflow id when
  there is one, with secrets scrubbed (the DROPSCRAP client pattern, `serpapi.py`, read at
  `f200c11`).
- **Status:** `kashmula status`, which phase 4 serves as `GET /v1/status`.
- **Heartbeat:** the daily ledger workflow records a row; a missing row shows on the status board.

There is no OpenTelemetry or Langfuse in the first wave (ADR-0002). dbos has an `otel` extra
(E-220), which is the way back when logs and step history cannot answer a question. Alerts (the
digest, a health failure, an ERROR workflow, a breaker, STOP) need a delivery channel, which is
phase-4 research.

## 19. Security and secrets

- Secrets live only in the environment: the Apify token, the Anthropic key and the database URL.
  In phase 1 they live in the session's environment, and from
  phase 4 in the host's secret store (phase-4 research). They never enter the repository, the
  journal, logs or CI.
- `dbos-config.yaml` names the database only as `${DBOS_SYSTEM_DATABASE_URL}` (E-223). Database
  passwords are escaped in URLs (E-223).
- CI holds no secrets. Every test is offline behind the socket guard, and `APIFY_TOKEN` never
  reaches GitHub (E-48).
- One credential per platform, read at boot, with no code path to another (E-87).
- No model-generated code runs on the runtime host (ADR-0002). Builder-written Actor code runs
  only in CI, in the development environment and on Apify, after a human merge.
- External content is data: source pages, Store listings and gate evidence reach agents and
  cards only as data, and Scout has no write tool (U-30). Before any agent gets a write tool,
  the operator reads OWASP LLM01 and the vendor's agent-safety guidance (U-30's day-one step).
- The Operate API token is stored as a SHA-256 hash and revocable. The Operate spec binds it to
  one endpoint on Moonzila's side.
- `doctor.mjs`'s secret scan stays in the gate (AGENTS.md invariants).

## 20. Deployment and what phase 4 must research

**Target.** One always-on shared-cpu-1x Fly.io Machine with 1 GB ($6.70 a month) or 2 GB ($12.70)
for the worker, with a card on file (E-49). GitHub Actions builds the image (E-48 permits
building and testing the repository's software). No production credential is stored in GitHub,
so the deploy itself runs outside GitHub.

**Deploy discipline.** Every deploy runs `kashmula pause`, waits until no workflow is PENDING,
deploys, then runs `kashmula resume`. New code never replays a run in flight
(`DBOSStepNondeterminismError`, E-225), and whether a new `application_version` recovers an older
version's pending workflows is not in the corpus (U-40 residual).

**Phase 4 collects with Research-Kit, before freezing its contracts:**

- Postgres hosting with backups and point-in-time restore, its price and minimum version. Fly's
  unmanaged Postgres is listed as Unsupported (E-49), and managed prices are not captured (U-17).
- Fly secrets, ingress and TLS for the Operate API, and how the operator's CLI reaches the
  production database or API.
- The HTTP framework for the API.
- How the image reaches Fly without a Fly credential in GitHub.
- An alert channel for the digest and alerts.
- Fly's acceptable-use terms (not captured, U-17).
- The Apify analytics API (cost per 1,000 results, paid users) for `/v1/status`; the Apify Issues
  API is collected later, when Support returns.

## 21. Reuse from the operator's repositories

| Source | Licence | What is reused | How |
|---|---|---|---|
| DROPSCRAP `search-light-signals` (read at `f200c11`) | no LICENSE file; `package.json` says ISC and private; the operator owns it | per-source failure isolation, shape errors, a "blackout" status when every source fails, stable item ids and canonical URLs, Federal Register and CSMS request shapes | ported as a design into Python; no code copied. Its two known bugs (a nonexistent `tier` field in `formatDigest`, a regex without a capture group in `atomLink`) are not ported. GDELT, RSS, Tavily, n8n, Telegram and Sheets are dropped. A per-run request ceiling is added |
| DROPSCRAP `serpapi.py`, `ratelimit.py` | as above | count-before-send budget ceilings, refusals recorded and never sent, named statuses, secrets scrubbed from messages | redesigned with the counter per workflow in Postgres (section 12) |
| DROPSCRAP `gate.py` | as above | KILL, HOLD and PASS on ranges, where PASS never authorises spend | the idea behind "approving a gate causes no write by itself" (section 13.1) |
| DROPSCRAP `.github/workflows/recon.yml` daily cron | as above | nothing | not copied: GitHub's terms forbid running the business on Actions (E-48) |
| DROPSCRAP `compliance.py`, `economics.py` | as above | reference for C6 later | not used in C1 |
| Agent repository (read at `8932fe0`) | **no licence file: ideas only, no text** | R9 and K35 (durable workflows, idempotency keys on every write, E-54), R15 (policy as code on every tool call), R13 (tamper-evident log), R8 (a microVM-class sandbox for generated code, the Builder's return condition), R10 (hidden oracles with injection cases), default deny on approval timeout | cited by file path; nothing copied |
| WindowRunner eval harness (read at `b50ff36`) | Apache-2.0 | hidden oracle outside the builder's reach, scripted fake provider, pass equals oracle exit 0 and a finished run, non-zero exit on any failure | patterns ported to pytest; no code copied, so no notice is owed. If code is ever copied, its Apache-2.0 notice comes with it |
| Research-Kit | the kit's own | the evidence gate before every niche and every phase's facts | run, never vendored |

## 22. Mapping to the phases of docs/BUILD.md

The phase rules stay as they are: one pull request per phase, the operator merges, the agent asks
before the next phase. The phase table changes as follows.

| Phase | Delivers under this design | Exit criteria | Operator |
|---|---|---|---|
| 0 | Handoff, skills, build-stack research at PASS, this spec, ADRs 0001 to 0011, BUILD.md | as now | merges, which approves the design |
| 1 | **Actor first.** In order: Research-Kit quote anchors for the capture-only names this spec uses (E-04 payout days; E-05 clauses 8.1 and 8.2; E-51 and E-52 `DBOSClient`; E-52 and E-228 `apply_schedules` status, `pause_schedule`, `resume_schedule`, `trigger_schedule`, `cancel_workflows`, `workflow_id_prefix`, `DELAYED`); collection of the niche short list's source terms, the Apify Python Actor Dockerfile and local-run pages, the CLI's installation, and the run-start, run-status and dataset-read endpoints; the day-one checks; `pyproject.toml` with the pins; the package skeleton with `actor check` and `actor card`; the template and Actor 1 with recorded responses, tests and the hidden oracle; `actors` added to `codePaths`; CI | preflight PASS; the phase-1 gate (17.4) green locally and in CI; every guard's test fails with its guard removed; Actor 1 runs locally against recorded responses; dataset-content charging tests; template checks match E-247 to E-250, E-05 and E-10 | approves niche 1 in the PR; finishes Apify KYC and the payout method before the merge; after the merge, with the agent: push, two private runs 24 hours apart (one limited), then the Console publish and price from the card |
| 2 | **Runtime core, offline** (the old phase 1, smaller): migrations, ids, journal, policy guard and `Permit`, write intents, ledger, prices and breaker, gate workflow, CLI and digest, PAUSE, STOP and RESUME with the watcher, Actor registry seeded with Actor 1, readiness registration, the frozen Operate models and `docs/contracts/operate-api.md`, the `pg` and `recovery` lanes | full gate green; every guard shown to fail without its code; approval and kill-switch tests repeated 30 times | nothing |
| 3 | **Scout and the deterministic workflows** against test doubles: research first (Scout's sources; the Apify version and build endpoints if the release adapter uses the API); Scout under `DBOSDurability` with its budget; release, health and ledger workflows; then, with the operator's tokens, one live health run and one staged patch release through the twin | end-to-end run against doubles; the two live runs pass; the injection test fails with its guard removed | Anthropic API key with an organization limit and the `scout` Workspace limit |
| 4 | **Operations:** research first (section 20); deployment; Operate API v1; alert channel; daily health live; a day unattended; STOP on the live loop | deployed; STOP confirmed on the live loop; a day of unattended runs | hosting account with a card on file |
| 5 | Gap audit, answer-only (unchanged) | as now | as now |
| 6 | Break test (unchanged), aimed first at the crash points, the in-flight wait, the stop sweep and the deploy drain | as now | as now |
| 7, 8 | C6 and C2/C8 (unchanged, separate designs) | as now | as now |

The Builder, Support and Finance agents and tracing leave phases 3 and 4 for the cut list
(ADR-0002). If the operator keeps BUILD.md's original order instead of ADR-0001, the only change
is that Actor 1's publish moves to the end of phase 3.

## 23. Risks

1. **Actor 1 unwatched in phases 2 and 3.** A source break is caught only by Apify's daily test
   after three failed days (E-256) or by the operator, at a cost in quality score (E-92).
   Mitigations: the fast-path repair target and the deploy in phase 4. The operator may also
   schedule the Actor Testing Actor on Apify itself (E-257) at the cost of platform credits.
2. **Niche terms.** If the shortlisted sources' terms (U-24) do not allow commercial use, phase 1
   needs a different source and the port of `search-light-signals` is lost.
3. **Day-one surprises.** The U-46 check may show that `DBOSDurability` rejects `TestModel`
   overrides, or that `StepConfig` lacks a needed field. The U-44 check may show a generic
   exception for 429. Fallbacks exist (sections 12 and 16.2) but change the agent module.
4. **Capture-only names.** Several DBOS method names come from captures, not Finding cells.
   Phase 1 anchors them before phase 2 codes against them; if one is missing, the kill switch or
   the schedule rule is redesigned before code.
5. **Inferences to prove.** DBOS management calls from a plain thread, and app tables sharing the
   DBOS database. If either fails, the stop sweep moves into a workflow or the app tables get
   their own database.
6. **A write past its guard completes after STOP.** STOP waits for it and reports it rather than
   hiding it.
7. **Synthetic-event overcharge.** Every default-dataset item is charged (E-245), so a bug that
   pushes an error or duplicate item bills a customer. Guards: dataset-content tests, the
   oracle's checks, the run-summary comparison on the platform.
8. **Under-charge by misconfiguration.** If monetization is set up wrongly, revenue is zero with
   no error. Guard: the run-summary check after monetization.
9. **Human time.** Cutting the Builder adds a pull-request review and a Console sitting per Actor
   (about 45 minutes). This is fine for the first wave and does not scale past five Actors
   without the Builder.
10. **Store email duties stay manual.** Store issues and Apify's requests arrive by email with 14-
    day and three-business-day duties (E-05 capture), and no Issues API is in the corpus.
11. **Hosting unknowns.** Postgres hosting, its backups and its cost are unknown until phase 4
    (E-49, U-17), and the one-database design relies on them.
12. **Deploy discipline is process, not enforcement.** PAUSE, drain, deploy and RESUME, with
    versioned workflow names, prevent nondeterminism errors only if they are followed. The
    deploy script runs them in order and refuses to deploy while a workflow is PENDING.
13. **Demand is unproven** (E-12, E-14; U-05, U-33). The design gets the evidence earlier; it
    cannot create it.

## 24. Open questions for the operator

These are intent questions. Facts go to research. Merging the phase-0 pull request approves the
design, including ADR-0001's Actor-first order and ADR-0002's cut list.

1. **Repairs.** While Actors are pull requests, is a 48-hour merge target for fast-path repairs
   (no README, schema or price change) acceptable to you? When a Builder returns, should such
   repairs ship without a gate and with a one-command rollback, or always as a reviewed proposal,
   as the Operate spec's "a broken Actor" example suggests?
2. **Model budget for the first wave.** This design assumes an Anthropic organization limit of
   about $50 a month and a `scout` Workspace limit of $10. Do you want different limits inside
   the 200-1,000 USD budget?
3. **Interim monitoring of Actor 1.** Through phases 2 and 3, rely on Apify's own daily test
   (notice after three failed days), or also spend about 30 minutes and some platform credits to
   schedule the Actor Testing Actor (E-257)?
