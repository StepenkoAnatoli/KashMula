# 0010. Charge per item with the synthetic dataset-item event only

- Date: 2026-10-04
- Status: proposed

## Context

Apify offers two per-item charging mechanisms:

- The synthetic `apify-default-dataset-item` event is on by default and charges every item in
  the run's default dataset with no code (E-245).
- A custom event can be charged per item with `push_data(item, charged_event_name=...)` (E-244,
  E-245).

The corpus does not say whether both would charge one push (U-48 residual). The reviewed brief
resolves this as one per-item mechanism per Actor, with the synthetic event deleted in Console
when a custom event is used (BRIEF, build-stack contradictions; E-246).

Local test mode (`ACTOR_TEST_PAY_PER_EVENT=true`) logs explicit charge calls to a local
`charging-log` dataset (E-244). The synthetic event makes no call, so its local behaviour is not
shown. On the platform, `push_data` returns a `ChargeResult` under the synthetic event (E-245),
and the user's `ACTOR_MAX_TOTAL_CHARGE_USD` is already applied in it (E-244).

## Decision

- **One mechanism.** Every Actor charges per result through the synthetic
  `apify-default-dataset-item` event and has no charging code. The template checker fails on
  `Actor.charge(` or `charged_event_name=`.
- **Only results enter the default dataset.** Error items never go there, and items are
  deduplicated within a run.
- **Charge limit.** The `ChargeResult` from `push_data` is checked for
  `event_charge_limit_reached`, and the Actor stops cleanly when it is set.
- **Run summary.** The Actor writes a summary (items pushed, summed `charged_count`, limit
  reached) to its default key-value store.
- **The local guard tests what is charged.** The default dataset holds only valid, unique result
  items, and the prefill input yields a non-empty dataset. What test mode logs for the synthetic
  event is recorded by a day-one check as an observation, not used as the guard.
- **The revenue path is proven on the platform.** The first run after monetization is set up
  must show a summed `charged_count` equal to the items pushed. That run is a private run if
  Console allows monetization before publishing, and otherwise the first health run after
  publishing. A mismatch blocks releases and raises an alert.
- **The Console card says so.** It keeps the synthetic event as the per-result and primary event
  (E-246) and adds no custom per-item event.

## Alternatives rejected and why

- **A custom per-item event, with the synthetic event deleted in Console** (Approach 3). Its
  local charge log is testable (E-244), but it rests on a manual Console step that no test can
  observe. If the step is missed, a customer may be charged twice for one item (U-48 residual).
  An error there lands on a customer's bill, while the synthetic event's failure mode, a
  misconfiguration that under-charges, costs only revenue and is caught by the run-summary
  check.
- **Asserting local charge counts under `ACTOR_TEST_PAY_PER_EVENT` as the overcharge guard**
  (Approaches 1 and 2). It rests on behaviour E-244 does not show for the synthetic event.
- **Explicit `Actor.charge` calls per item.** This is the same double-mechanism risk as a custom
  event, plus charging code in every Actor.

## Consequences

- Any item pushed to the default dataset is billed, so a bug that pushes an error or duplicate
  item overcharges. The guards are the dataset-content tests, the hidden oracle and the
  run-summary comparison.
- The local suite cannot prove revenue. The first monetized platform run does.
- No per-Actor Console deletion step exists, which removes one manual line from every publish
  sitting.
- `docs/BUILD.md`'s phase exit criterion "charging tests" means dataset-content tests plus the
  platform run-summary check.

## Evidence

E-244, E-245, E-246; U-48; `research/BRIEF.md` ("Contradictions and how they were resolved",
build stack, "Per-item charging").
