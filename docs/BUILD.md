# Build phases

How KashMula goes from the phase-1 plan (`docs/PLAN.md`) to a bot that runs unattended.
The design these phases implement is `docs/specs/2026-10-04-kashmula-build-design.md`;
the decisions with rejected alternatives are in `docs/adr/`.

## How a phase runs

1. **One phase, one pull request**, from `claude/bold-hopper-oxr543`, restarted from `main`
   after each merge. Draft first, ready for review when its gate passes.
2. **The operator merges.** Agents never merge.
3. **After a merge the agent asks whether to start the next phase, and waits.**
4. Inside a phase the `lead-orchestrator` skill runs the work: facts first (Research-Kit,
   when the phase needs a fact the repository cannot answer), frozen contracts, builders,
   independent reviewers, the gate compared with the baseline, then the PR.
5. Before a phase's code, its design is presented with the `brainstorming` skill. The
   phase-0 merge approves the overall design; each later phase opens with a short design in
   its PR description, inside that approved design. A phase that would change the approved
   design stops and says so first.
6. Every code change follows `careful-coding`: read before changing, run before claiming,
   report mistakes plainly with what, where, impact, cause, fix and how it was verified.

## The phases

| Phase | Delivers | Exit criteria | Skills | Needs from the operator before it starts |
|---|---|---|---|---|
| 0 | Handoff for a fresh chat; the five skills; build-stack research (U-38 to U-51) at `PASS`; design spec, ADRs and this plan | `preflight.mjs` PASS; spec self-reviewed and independently reviewed; operator merges | lead-orchestrator, brainstorming | nothing |
| 1 | Runtime core, offline: Python package, contracts, policy layer, budgets and stop signals, price table, approval queue, kill switch, operator CLI, CI | Full gate green in CI and locally; every guard shown to fail without its code (mutation); approval and kill-switch tests repeated 30 times | lead-orchestrator (Full: money and concurrency), careful-coding, brainstorming | nothing |
| 2 | The Actor template and the first Actor, built and tested locally: definition files, pay-per-event charging, limited permissions, README without external links | Actor runs locally against recorded source responses; charging tests; template checks match the Apify rules in the brief | lead-orchestrator, careful-coding, brainstorming | approve niche 1 from a short list in the phase-2 PR |
| 3 | The agents: Scout, Builder, QA and Publisher as durable workflows with per-agent budgets; QA mirrors Apify's automated tests before anything is published | End-to-end run against test doubles; with the operator's Apify token, one staged publish of the first Actor | lead-orchestrator (Full), careful-coding, brainstorming | Apify account verified, API token; Anthropic API key with an organization spend limit |
| 4 | Operations: deployment, the operator's approval surface (CLI first; the HTTPS API Moonzila's Operate mode will consume), Finance and Support agents, tracing | Deployed; the kill switch stops a live loop; a day of unattended runs | lead-orchestrator (Full), careful-coding, brainstorming | hosting account with a card on file |
| 5 | Gap audit of the running bot against its purpose, answer-only | Audit report in `docs/audits/`; nothing changes until the operator writes `IMPLEMENT THE RESEARCH` | gap-audit (then brainstorming for any approved fix) | nothing |
| 6 | Break test before going live: clean checkouts, lockfile drift, missing environment variables, database restarts, time zones, flaky tests; fixes as separate commits | Every finding has a repro command; every retained fix removes its failure and keeps the gate at the baseline | break-test, careful-coding | nothing |
| 7 | C6: disclosed AI print-on-demand on Etsy through Printify, on the same skeleton, human-gated | 10 approved designs listed; disclosures on every listing | lead-orchestrator, careful-coding, brainstorming | Etsy shop and Printify account opened by hand |
| 8 | C2/C8, conditional: the customs and tariff alert feed | Only after the four checks in `docs/PLAN.md` section 5 | all, as above | the four checks |

Phases 5 and 6 come after the bot runs end to end, because both judge a running system.
Phases 7 and 8 are optional and follow the 60-day Store review in `docs/PLAN.md` section 5.

## Research per phase

Phase 0 collects what phases 1 to 3 are coded against. Each later phase starts by checking
whether its design depends on a fact the corpus does not hold (hosting Postgres for phase 4,
Apify analytics and Store issues for the Finance and Support agents, the niche's source
terms for phase 2), and collects it through Research-Kit before freezing contracts.

## Recorded for later

- `careful-coding` refers to `references/self-review-checklist.md`, which no copy of the
  skill contains.
