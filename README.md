# KashMula

A research-first plan for a fully automated, multi-agent online income bot, built for an
operator who is an Israeli tax resident selling to US and worldwide customers, on a running
budget of 200-1,000 USD a month before revenue, with no YouTube Shorts and as little human
time as the platforms legally allow.

The research was done with [Research-Kit](https://github.com/StepenkoAnatoli/Research-Kit):
every decisive fact was fetched from the page that owns it, every claim carries a verbatim
quote from a cached capture, and the gate (`preflight.mjs`) passes before anything is built.

## Read in this order

0. [`HANDOFF.md`](HANDOFF.md): where the project stands and how a fresh session resumes.
1. [`docs/PLAN.md`](docs/PLAN.md): the decision, the ranked candidates, the architecture,
   the roadmap, the costs, the human steps that cannot be automated, and what was rejected.
2. [`research/BRIEF.md`](research/BRIEF.md): the kit's phase-1 to phase-2 handoff: the
   prior registered before collection, the verified claims with their sources, the
   contradictions and how they were resolved, the known unknowns with their day-one checks.
3. [`research/DISCOVERY.md`](research/DISCOVERY.md): the 37 blocking unknowns and their
   status, and [`research/EVIDENCE.md`](research/EVIDENCE.md): one row per captured page.

## Status

Phase 1 (research) is complete: `node "$HOME/.agents/research-kit/bin/preflight.mjs"` prints
`PASS`. Phase 2 (the build) runs in phases, one pull request each (`HANDOFF.md`), and starts from `docs/PLAN.md` and `research/BRIEF.md`; a builder
should not need to re-research anything. If a fact is missing, that is a phase-1 gap to
close with the kit, not a guess to make.

## Rules for agents working here

`AGENTS.md` carries the rules; `CLAUDE.md` points at it and records the operator's standing
instruction that all research runs through Research-Kit.

The skills every session here uses (`lead-orchestrator`, `brainstorming`, `careful-coding`,
`gap-audit`, `break-test`) are vendored under `.claude/skills/`.
