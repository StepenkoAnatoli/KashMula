# 0006. Budgets: provider limits, run limits and a worst-case reservation ledger

- Date: 2026-10-04
- Status: proposed

## Context

The budget is 200 to 1,000 USD a month before revenue. An unattended agent loop with no cost
ceiling burned a $200 monthly plan in about 48 hours (E-87).

The tools available:

- **Pydantic AI** caps a run with `UsageLimits` and raises `UsageLimitExceeded`. Its
  `cost_limit` is best effort, "not a hard billing guarantee" (E-233).
- **Anthropic** enforces a monthly tier cap and lower self-set limits per organization and per
  Workspace. A cap answers HTTP 429 and a self-set limit HTTP 400 `invalid_request_error`, and
  retries fail until access resumes (E-43).
- **The client** retries on its own (`max_retries=2`) unless built with `max_retries=0`, which
  the DBOS integration asks for (E-235, E-237). Which exception a 429 or 5xx raises is
  KNOWN-UNKNOWN (U-44).
- **DROPSCRAP's lesson:** a budget counter must be per workflow and stored in Postgres, so a
  recovered step cannot spend twice (repository read at `f200c11`, `serpapi.py`).

## Decision

1. **Provider limits.** The operator sets an Anthropic organization limit below the Start tier's
   $500 cap and one Workspace per agent with its own limit (E-43). The first wave has one
   Workspace, `scout`.
2. **Run limits.** Every `agent.run()` carries `UsageLimits` (request, tool-call and token limits,
   and `cost_limit`) from `config/budgets.toml`. A breach ends the workflow as
   `budget_exhausted` and is never retried.
3. **Reservation ledger.**
   - Before each run, an admission step reserves the worst case:
     `input_tokens_limit` × input price + `output_tokens_limit` × output price. The prices
     come from the dated row in `config/prices.toml` (E-42; E-47 shows prices change on dates).
   - The reservation is checked against the agent, provider and global monthly caps, each set
     at 80% of the matching provider limit (an assumption).
   - The `spend` row is keyed by business key plus step.
   - After the run a step settles the real cost from the run's usage. A reservation a crash
     leaves unsettled stays counted at its maximum.
   - Reaching the global cap triggers STOP (ADR-0008).
4. **Stop signals.**
   - A 429 at the tier cap opens the `anthropic` breaker until 00:00 UTC on the first of the
     next month.
   - A 400 at a self-set limit opens it until the operator resets it (E-43).
   - Neither is retried. Each opens a `breaker` gate card.
5. **Retries.** `AsyncAnthropic(max_retries=0)` is passed as `anthropic_client=`. Model steps get
   no `StepConfig`, so no retries (E-237). A failed Scout run waits for the next weekly tick. The
   U-44 day-one test records the exception classes the breaker classifier matches.
6. **Fixed and platform costs.** Own test runs come from the Creator plan's bonus usage (E-13).
   Run usage is read from the Apify run API once it is collected. Hosting (E-49) is a dated line
   in `budgets.toml`. Status shows the month's total against every cap and the 200-1,000 USD
   budget.

## Alternatives rejected and why

- **`cost_limit` alone.** It is best effort (E-233).
- **Provider limits alone.** They stop spend only after the month's cap is reached, and they do
  not attribute spend to a workflow.
- **An in-process budget counter.** A restart forgets it, and a recovered step spends twice
  (the DROPSCRAP lesson).
- **Reserving `cost_limit` instead of the worst case** (Approach 2). A best-effort figure can be
  lower than what the run actually costs, so the ledger could under-count.
- **DBOS step retries with a `should_retry` allowlist on model calls** (Approach 1). This adds a
  retry path whose exception classes are still unknown (U-44), for a weekly agent whose next
  tick is a retry anyway.
- **Leaving the SDK's own retries on.** They fail during a cap (E-43) and hide wire requests from
  `request_limit` (E-234).

## Consequences

- The ledger can over-count, because unsettled reservations stay at the maximum. It never
  under-counts.
- A breaker trip needs the operator to raise a limit or wait.
- A second agent adds a Workspace, which is a few minutes of operator setup.
- If prices in `prices.toml` are wrong, the provider limits still cap the damage.

## Evidence

E-13, E-42, E-43, E-47, E-49, E-87, E-233, E-234, E-235, E-237; U-15, U-44.
