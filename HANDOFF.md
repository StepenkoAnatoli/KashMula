# Handoff

The state of KashMula for an agent (or a person) starting in a fresh chat. Read this first,
then `AGENTS.md`, then `docs/BUILD.md` once it exists. Everything a fresh session needs is
in this repository; nothing depends on the chat that produced it.

_Written 2026-10-04 at the end of the research phase, before the build starts._

## What KashMula is

A fully automated, multi-agent online income bot with as little human time as the
platforms legally allow. Hard constraints from the operator:

- **No YouTube Shorts.**
- **Operator:** Israeli tax resident with no US status. No Stripe account of any kind can be
  opened (`docs/PLAN.md`, section 2).
- **Budget:** 200-1,000 USD a month before revenue.
- **Human time:** as close to zero as the platforms allow; the steps that cannot be automated
  are listed in `docs/PLAN.md`, section 7.

## Where things stand

| Item | State |
|---|---|
| Phase-1 research (Research-Kit) | Done. PRs #1, #2 and #3 merged into `main`. `preflight.mjs` prints `PASS`, 0 blocking. |
| The decision | `docs/PLAN.md`: C1, pay-per-event Actors on Apify Store first; C6, disclosed AI print-on-demand on Etsy via Printify, in parallel and human-gated; C2/C8, a customs and tariff alert feed, conditional in month 2-3. |
| The build | Starting. Phase 0 (this handoff, the skills, the build research and the design) is the first build PR. |

## How the build runs: phases, one PR each

1. Each phase is one pull request from the branch `claude/bold-hopper-oxr543`, restarted
   from `main` after every merge.
2. The operator reviews and merges. Agents never merge.
3. **After a merge, the agent asks the operator whether to start the next phase, and waits.**
   It does not start the next phase on its own.
4. The phase table, with each phase's scope, exit criteria and the skills it uses, is in
   `docs/BUILD.md`.

## Skills used here

They are vendored under `.claude/skills/` so every session in this repository has them.

| Skill | Used for |
|---|---|
| `lead-orchestrator` | Every phase: plan, research through the kit, frozen contracts, parallel builders, independent reviewers, gate against the baseline. |
| `brainstorming` | Before each phase's code: the design is presented and approved first. Merging the phase-0 PR is the approval of the build design. |
| `careful-coding` | Every code change: read before changing, verify by running, report mistakes plainly. |
| `gap-audit` | Later, once the bot runs end to end: an answer-only audit; nothing changes until the operator writes `IMPLEMENT THE RESEARCH`. |
| `break-test` | Later, before going live: prove build and test failures with repro commands, then fix them in separate commits. |

Known gap: `careful-coding` points at `references/self-review-checklist.md`, which is
missing from every copy of the skill (this repository, the Monnzila repository and the
synced original). The skill works without it; the operator decides whether to add it.

## Rules that bind every session

- `CLAUDE.md` and `AGENTS.md`: all research goes through Research-Kit
  (https://github.com/StepenkoAnatoli/Research-Kit). Facts the design depends on are
  collected into `research/` and pass `preflight.mjs` before anything is built. A page
  fetched by hand is not evidence.
- Commit reports have five parts: what changed, why, what it touched, what was verified,
  what went wrong and was fixed.
- A commit touching a code path (`src`, `lib`, `bin`, `scripts`, `app`) stages
  `docs/ARCHITECTURE.md` with it; the kit's commit hook enforces this.
- No force-push, no `--no-verify`, no `research/GATE_OFF`.
- Secrets never enter the repository. Keys live in `~/.agents/research-kit.config.json`,
  the Firecrawl CLI login or the environment.

## The machine

This work ran in a Claude Code cloud container. A fresh container does not keep the kit or
its keys; a cleared chat in the same container does.

| Item | Value on 2026-10-04 |
|---|---|
| Kit | `~/.agents/research-kit`, version 0.9.3, `doctor.mjs` READY, role `collector` |
| Collection transport | `firecrawl-cli` 1.25.2, logged in, 1,058 credits left |
| Search transport | SerpAPI, 0 searches left until the cycle renews on 2026-10-14; plan URLs directly until then |
| Commit gate | `core.hooksPath` points at the kit's `githooks` |
| Toolchain | Python 3.11, uv 0.8, PostgreSQL 16, Docker |

To rebuild the kit in a new container: clone the Research-Kit repository, run its
`research-kit/bin/install.mjs`, log the Firecrawl CLI in, write
`~/.agents/research-kit.config.json` with `transport`, `searchTransport` and the SerpAPI
key, then run `node "$HOME/.agents/research-kit/bin/doctor.mjs"` until it prints `READY`.

## Related work outside this repository

- **Moonzila (formerly MoonAliza).** Draft PR
  [StepenkoAnatoli/Moonzila#31](https://github.com/StepenkoAnatoli/Moonzila/pull/31)
  renames the product in user-facing text and specifies **Operate mode**: the desktop app as
  the operator's seat for this bot (approval queue, status board and Stop, evidence review,
  code-change proposals) over an HTTPS API that KashMula's runtime will serve. Open
  question to the operator: the product text says "Monnzila" while the repository is now
  named "Moonzila"; one of them should change.
- **Builder choice.** The operator asked which coding agent should build this; the answer
  was Claude Code first, with GPT-6.1 Sol as the second opinion.
- **Hardware.** For running the bot and developing locally, the GMKtec NucBox K11 at
  5,279 NIS on KSP was judged a reasonable buy unless a K8 Plus is cheaper; a desktop parts
  build came to about 3,750-3,950 NIS. Production runs on Fly.io regardless (`docs/PLAN.md`).

## Resuming in a fresh chat

1. `git fetch origin && git status` in `/home/user/KashMula` (or a fresh clone).
2. Read this file, `AGENTS.md` (including "Orchestrator facts") and `docs/BUILD.md`.
3. Check which phase PRs are open or merged on GitHub.
4. If the last phase PR is merged: ask the operator whether to start the next phase.
   If it is open: carry on with its open items (CI, review comments).
