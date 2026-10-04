# 0001. Build the first Actor before the runtime

- Date: 2026-10-04
- Status: proposed

## Context

The draft `docs/BUILD.md` builds the offline runtime core in phase 1, the Actor template and
the first Actor in phase 2, and the agents in phase 3. Under that order the first Store publish
waits until the end of phase 3.

The revenue clock is Apify Store, not the runtime:

- A new Actor in the one first-person account waited a full week for its first run and had
  single-digit weekly runs in months 1 and 2 (E-14).
- The quality score, which drives Store and MCP search placement, rewards a track record (E-92).
- Apify invoices on the 11th and pays on days 21 to 25 of the following month (E-04 capture).
- The day-60-90 review that decides the second wave, and the 90-day verified-payout criterion,
  both count from the first publish (PLAN section 5; U-05, U-33).

An Actor does not need the runtime to earn. Customers' runs execute on Apify (E-06). Apify tests
every Store Actor daily (E-256). The first publish and price are manual in Console anyway
(U-51). Own test runs come out of the Creator plan's bonus usage (E-13).

## Decision

Swap `docs/BUILD.md` phases 1 and 2.

**Phase 1 delivers the template and Actor 1.** It opens with:

- the day-one checks (U-38, U-44, U-46 and the others in spec section 17.3);
- the quote anchors for capture-only names;
- the Research-Kit collection of the niche short list's source terms (U-24) and of the Apify
  pages the Actor needs.

During phase 1 the operator approves niche 1 in the pull request and completes Apify KYC and the
payout method before the merge. After the merge the agent and the operator push the Actor, run
it privately at least twice, 24 hours apart, once with limited permissions forced (E-252), and
the operator publishes and prices it in Console from the card.

**Phase 2 is the runtime core, offline.** It is the old phase 1 with Actor 1 seeded into the
registry.

## Alternatives rejected and why

- **BUILD.md's runtime-first order.** The first payout slips by the time phases 1 to 3 take,
  roughly one payout cycle or more. Nothing is made safer by it, because the first publish and
  price stay manual in either order (U-51) and Apify's daily test watches the Actor either way
  (E-256).
- **Building the Actor and the runtime core in one phase.** One pull request would hold two
  unrelated systems, which breaks the one-reviewable-PR rule of `docs/BUILD.md`.

## Consequences

- Actor 1 runs on the Store through phases 2 and 3 with no runtime watching it. The monitor is
  Apify's daily test, which notifies after three failed days (E-256), plus the repair fast path
  of ADR-0011. Spec risk 1 records this.
- The operator's phase-1 needs change: approve niche 1 inside the phase, and finish KYC and the
  payout method before its merge.
- `docs/BUILD.md`'s phase table and its "Research per phase" paragraph change (spec section 22).
- `research/BRIEF.md`'s "First build step, concretely" line and `docs/PLAN.md` section 5's
  week-1-2 row describe the old order and become stale.
- If the operator rejects this ADR, the rest of the design stands unchanged and only Actor 1's
  publish moves to the end of phase 3.

## Evidence

E-04 (capture: invoice on the 11th, payout days 21 to 25), E-06, E-13, E-14, E-92, E-252, E-256;
U-05, U-24, U-33, U-51.
