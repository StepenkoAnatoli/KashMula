# 0008. Kill switch: PAUSE and STOP, coupled to the loop, confirmed only when swept

- Date: 2026-10-04
- Status: proposed

## Context

The corpus's lesson: "Disabling a trigger is not the same as stopping the system." Unattended
agents ran 24 hours past their pause (E-87). The Operate spec says Stop halts the scheduler and
the queues, and that Moonzila shows the runtime's confirmation, never its own assumption.

What DBOS offers:

- Cancelling a workflow interrupts it at its next step and dequeues it if queued (E-228, E-231).
  `cancel_workflows` takes a list with `cancel_children` (E-228 capture).
- Schedules can be paused and resumed at runtime (E-52), and `apply_schedules` keeps a
  schedule's paused status across restarts (E-228 capture).
- Workflow states include ENQUEUED, DELAYED and PENDING (E-228 capture).
- `resume_workflow` restarts a cancelled workflow from its last completed step (E-228).
- A step already running cannot be preempted (E-228, E-226).

## Decision

The control state is one row: RUNNING, PAUSED, STOPPING or STOPPED.

**PAUSE** closes admissions and pauses business schedules, and lets running workflows finish,
including their writes. Deploys use it to drain.

**STOP**:

1. Commit STOPPING and the journal row. From then on every guard refuses every write.
2. The stop watcher, a worker thread that runs every 5 seconds and at startup, pauses every
   business schedule.
3. It cancels every ENQUEUED, DELAYED and PENDING workflow with `cancel_children=True`, except
   gate workflows, which only wait and read.
4. It waits until no `external_write` row is still SENT.
5. It repeats the sweep until nothing is left.
6. It writes `swept_at`, STOPPED and a stop report with the cancelled ids.

Nothing reports STOPPED before `swept_at`. On timeout the answer is
`STOPPING: <n> writes in flight, <m> workflows left`.

**RESUME** is operator-only. It sets RUNNING and resumes the schedules. Cancelled workflows
stay cancelled unless the operator passes `--workflows`, which calls `resume_workflow` on the
ids in the stop report.

**Automatic STOP** happens when the global monthly spend cap is reached. Spend signals and
credential rejections open a breaker instead (ADR-0006).

## Alternatives rejected and why

- **Disabling the trigger or scheduler only.** E-87 shows the loop keeps going.
- **Setting queue limits to zero.** There are no queues of our own (ADR-0002), and limits at zero
  are not described (U-41).
- **A Postgres row lock held across in-flight calls, with STOP taking it exclusively**
  (Approach 1). Lock behaviour is not in the corpus. A hung call or an exhausted pool stalls the
  STOP. An intent row written inside the lock transaction rolls back on a crash and lets the
  write repeat. Waiting on committed intent rows gives the same honest confirmation using only
  our own tables.
- **Refusing ticks at admission instead of pausing schedules** (Approach 1). It is weaker than
  the evidence allows (E-52), and the Operate spec asks Stop to halt the scheduler.
- **Confirming STOP as soon as the flag is set** (Approaches 2 and 3). A write already past its
  guard could still land after "stopped" was reported.
- **Resuming every cancelled workflow on RESUME** (Approach 1). The cause of the stop may still
  be present, so it is an explicit option instead.
- **Cancelling gate workflows too.** Pending approvals would be lost and would need recreating,
  for no safety gain, since gates write nothing external.

## Consequences

- A model request or write already past its guard completes after STOP. STOP waits for it and
  says so.
- STOP never touches customers' runs on Apify. Withdrawing a public Actor is an operator action
  in Console (`isPublic`, E-254).
- Two inferences are proven by tests before phase 2 merges: that DBOS management calls work
  from the watcher thread, and that the sweep holds when repeated 30 times.
- Phase 4's exit criterion is a STOP confirmed on the live loop.

## Evidence

E-52, E-87, E-225, E-226, E-228, E-228 (capture), E-231, E-254; U-41, U-42; the Operate spec.
