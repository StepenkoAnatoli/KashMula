# 0011. Publishing, pricing and releases: the operator in Console first, staged releases after

- Date: 2026-10-04
- Status: proposed

## Context

What the corpus says about publishing and pricing:

- Apify describes publishing to the Store only as a Console flow with required sections (E-253).
- The CLI has no publish or price command (E-255).
- The Update Actor API accepts `isPublic`, Store fields and `pricingInfos`. Its error codes, such
  as `store-terms-not-accepted` and `cannot-monetize-without-payout-billing-info`, point to
  prerequisites set elsewhere (E-254).
- Monetization needs billing and payout details first (E-246).
- A significant price change waits 14 days, cannot be cancelled and happens at most once a month
  per Actor. Decreases are immediate (E-05, E-246).
- U-51 resolves: the first publish and the first price are done in Console.

What the corpus says about testing and staging:

- Apify tests every Store Actor daily and labels it under maintenance after three failed days
  (E-256).
- A single run can be forced to limited permissions (E-252).
- A non-public Actor is visible only to its owner (E-254).
- GitHub may not be used to run the business (E-48).

PLAN section 4 gives the Publisher no human gate after the niche approval, and gives QA a 48-hour
staged run.

## Decision

- **Staging a new Actor.** At least two private runs with the prefill input, at least 24 hours
  apart, one with permissions forced to limited. Each must finish SUCCEEDED with a non-empty
  default dataset within five minutes (E-256).
- **First publish and first price: the operator, in Console, in one sitting.**
  - The sitting works from a paste-ready card that `kashmula actor card` writes: listing fields,
    permission level, the synthetic per-result event, "+ usage" off, and the price floor from
    E-06.
  - It also reviews the README for E-40.
  - It is closed with `kashmula actor confirm-published`.
- **Releases after the first publish (phase 3)** are a workflow, `release:<slug>:<source12>`:
  1. Push to a private twin Actor (the Actor directory with a `-staging` name).
  2. Run its prefill input with limited permissions.
  3. Check the result and the run summary.
  4. Push to the public Actor.

  A failed check refuses the release. The README and schemas were reviewed in the merged pull
  request.
- **Prices after the first.**
  - The ledger workflow recommends an increase through a `gate:price:<slug>:<yyyy-mm>` card, at
    most one per Actor per month. A decrease is recommended in the digest.
  - The operator makes both in Console until a call on a throwaway private Actor with no paying
    users shows that `pricingInfos` works without Console prerequisites (U-51).
- **Tokens.** `APIFY_TOKEN` never reaches GitHub. Pushes run from the development environment
  (phases 1 to 3) or the worker (phase 4).
- **Repairs** that change no README, schema or price digest are fast-merge pull requests with a
  48-hour merge target.

This departs from PLAN section 4 in two places:

- The Publisher's "None after the niche approval" becomes a manual first publish and price, with
  gated increases.
- QA's 48-hour staged run becomes two private runs 24 hours apart for a new Actor, one staged run
  per release, and the daily health check.

## Alternatives rejected and why

- **Publishing and pricing through the API from the start.** The prerequisites the API's error
  codes point to are set in Console, and the corpus does not say the API skips them (U-51).
- **Price increases with no gate,** as PLAN section 4 has them. An increase is uncancellable and
  blocks further changes for a month (E-246), so the operator decides it.
- **A 48-hour stage for every release.** It would use most of the three-day window before a
  broken Actor is labelled under maintenance (E-256), and the daily health check covers the same
  ground continuously.
- **Publishing or pushing from GitHub Actions.** The Apify token would sit in GitHub, and GitHub
  is not used to run the business (E-48).
- **Unattended repairs** (Approach 2). This conflicts with the Operate spec's reviewed-edit rule.
- **Staging under a non-default build tag on the public Actor instead of a twin.** How a run
  selects a build is not in the corpus. A private twin uses only facts we hold (E-254, E-255).

## Consequences

- Each new Actor costs the operator one Console sitting of about 15 minutes, plus a few minutes
  per price change.
- The release workflow needs the Apify run, run-status and dataset endpoints (collected in
  phase 1) and the version and build path (collected in phase 3) before it is coded.
- A twin Actor per published Actor exists in the operator's account, private.
- Agentic buyers get the Actor automatically, because it meets E-10's conditions (pay per event,
  no "+ usage", limited permissions, no Standby, operator KYC done).

## Evidence

E-05, E-06, E-08, E-10, E-13, E-40, E-48, E-246, E-251, E-252, E-253, E-254, E-255, E-256; U-33,
U-51.
