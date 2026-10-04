# 0004. Idempotency: business-key workflow IDs and write intents

- Date: 2026-10-04
- Status: proposed

## Context

DBOS gives once-only starts but not once-only writes:

- A workflow started under an existing ID returns the existing run by default (E-225, E-228).
- A step can run again until it completes (E-225). Step retries are opt-in (E-226).
- A crash between an external call and its checkpoint can therefore repeat the call.
- The operator's own rule asks for idempotency keys on every external write (E-54, rule K35).

Three more facts shape the keys:

- `fork_workflow` gives the copy a new ID (E-231).
- Scheduled ticks are keyed by schedule name and time, and missed ticks can be backfilled (E-52).
- A price increase may happen at most once a month (E-05, E-246).

## Decision

**Workflow IDs are business keys.** Every workflow starts under `SetWorkflowID(key)` with the
default `return-existing` policy. The keys:

- `gate:<kind>:<subject>:<evidence12>`
- `gate:price:<slug>:<yyyy-mm>`
- `release:<slug>:<source12>`
- `health:<slug>:<yyyy-mm-dd>`
- `ledger:<yyyy-mm-dd>`
- `digest:<yyyy>-W<ww>`
- `scout:<yyyy>-W<ww>`

**Schedules start children.** A scheduled tick only starts its business workflow as a child
under the business key, so a tick, a backfill and a `trigger_schedule` call (E-52 capture) for
one period collapse into one run. `automatic_backfill` stays off (E-228 capture). Lookups use
the `workflow_id_prefix` filter (E-228 capture), not attribute filters, which need Postgres
(E-231).

**Every external write is one effects step with an intent row.** The step runs in this order:

1. Run the guard (ADR-0005).
2. Commit an `external_write` row in state SENT, in its own transaction.
3. Call the adapter with a timeout.
4. Record CONFIRMED or FAILED.

No database transaction spans a network call. The intent key is the business key plus the step
name, **never the workflow ID**.

**Every action carries a class**, which decides what happens when a step re-enters with a SENT
row and no result:

| Class | Meaning | On re-entry |
|---|---|---|
| B, repeat-safe | pushing a source version (E-255); a field-scoped Actor update (E-254) | repeat the call; retries allowed |
| C, spend-only | starting runs; model requests | repeat at most once more, bounded by the budget reservation |
| A, irreversible or customer-visible | publishing, pricing, visibility, Store replies | read the provider back; if that cannot settle it, mark UNKNOWN and open a gate; never repeat blindly |

The first wave has no class-A action. The gateway refuses to register a class-A action whose
adapter has no read-back method.

## Alternatives rejected and why

- **Random UUID workflow IDs with a separate dedupe table.** This duplicates what
  `SetWorkflowID` already guarantees, and a second table can disagree with it.
- **Relying on step checkpoints and retries alone.** A crash between the provider call and the
  checkpoint repeats the write (E-225).
- **Intent keys built from the workflow ID** (Approaches 2 and 3). A forked workflow (E-231)
  would not see the original's row and could repeat a write that already happened.
- **`automatic_backfill` on.** An outage would replay a burst of ticks.
- **Queue deduplication IDs.** There are no queues of our own in the first wave (ADR-0002).
- **Attribute filters for lookups.** They are Postgres-only (E-231), which would break the
  SQLite lane.
- **Building the full class-A read-back protocol in the first runtime phase** (Approach 1).
  No class-A action exists yet, and the read-back endpoints are not in the corpus. Refusing
  unregistered class-A actions keeps the rule without the machinery.

## Consequences

- A price key spent in a month blocks a second price card that month, even after a rejection.
  This is intended (E-05).
- The first class-A action, a Support reply or an API price change, cannot ship until its
  read-back endpoint is in the evidence.
- A crash-injection test on PostgreSQL 16 proves one CONFIRMED write per key after a restart
  (spec section 10.4).

## Evidence

E-05, E-52, E-52 (capture), E-54, E-225, E-226, E-228, E-228 (capture), E-231, E-246, E-254,
E-255; U-40.
