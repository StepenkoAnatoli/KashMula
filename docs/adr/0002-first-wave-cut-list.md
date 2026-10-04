# 0002. One model agent in the first wave, and what returns when

- Date: 2026-10-04
- Status: proposed

## Context

`docs/PLAN.md` section 4 lists seven agents: Scout, Builder, QA, Publisher, Support, Finance and
Compliance. The draft `docs/BUILD.md` builds Scout, Builder, QA and Publisher in phase 3, and
Finance, Support and tracing in phase 4.

The first wave is 3 to 5 Actors (PLAN section 1):

- A new Actor takes 4 to 8 hours of focused work, and "three reliable Actors out-earn ten
  unmaintained ones" (E-14).
- A runtime Builder would run model-generated code. The operator's Agent repository asks for a
  microVM-class sandbox with egress denied by default for that (rule R8,
  `docs/core/05-orchestration-runtime.md`, an idea only, since the repository has no licence),
  and the corpus has no sandbox facts for Fly.io.
- The Operate spec says nothing lands on the bot without a reviewed edit, and names "a broken
  Actor" as a reviewed proposal.
- A Support agent would send customer-facing text, which carries the AI-disclosure duty (E-40).
  Its Issues API is not in the corpus.

## Decision

The first wave has **one model agent, Scout**: weekly, read-only, under `DBOSDurability`, with
its own budget. Three roles become deterministic code:

- QA: the CI gate, staged release runs and the daily health check.
- Publisher: the operator's Console sitting for the first publish and price, then the release
  workflow and price recommendations.
- Finance: the ledger workflow.

Compliance is the policy module. Everything else is deferred, each with a return trigger:

| Deferred | Instead, in the first wave | Returns when |
|---|---|---|
| Builder agent | Actors 2 to 5 and repairs are coding-agent pull requests built from the template, reviewed and merged by the operator | the day-60-90 review wants more than five Actors **and** a sandbox (microVM-class, egress denied by default, no runtime secrets in it) is designed with its facts collected; a new ADR decides it |
| Support agent | the operator answers Store issues within 14 days and Apify's requests within three business days (E-05 capture, clauses 8.1 and 8.2) | the first issue needing a written reply, or two issues a week; it needs the AI disclosure (E-40), the OWASP LLM01 reading (U-30), the Issues API in the evidence and the class-A read-back protocol (ADR-0004) |
| Finance agent | the deterministic ledger | the Apify analytics API is collected and a monthly question cannot be answered by the ledger |
| Model router, open weights | Claude only | model spend passes about $50 a month (PLAN section 4; E-46, E-47) |
| Tracing (OpenTelemetry, Langfuse) | DBOS step history, business tables, JSON logs | a question those cannot answer; dbos has an `otel` extra (E-220) |
| DBOS queues of our own | schedules on DBOS's internal queue | a second concurrent workload needs concurrency or rate limits (U-41; E-229) |
| Publishing and pricing by API | Console (ADR-0011) | a call on a throwaway private Actor shows `pricingInfos` works without Console prerequisites (U-51; E-254) |

## Alternatives rejected and why

- **PLAN section 4's full roster by phase 4** (Approaches 1 and 2). It means more model spend,
  more code and more attack surface before any Store data shows the first wave needs it.
- **A runtime Builder that generates and tests Actor code on the control-plane host.** That
  code would run beside the Apify token, the Anthropic key and the database password. Target
  pages are the most likely injection vector, and R8's sandbox is not in place.
- **Unattended repairs that ship without review** (Approach 2). This conflicts with the Operate
  spec's reviewed-edit rule.

## Consequences

- Each of Actors 2 to 5 costs the operator about 30 minutes of pull-request review and a
  15-minute Console sitting (spec section 16.3). That is fine for five Actors and does not scale
  past them.
- Store issues and Apify's requests reach the operator by email.
- `docs/PLAN.md` section 4's agent table no longer describes the first wave. `docs/BUILD.md`
  phase 3 becomes "Scout and the deterministic workflows", and phase 4 loses Finance, Support
  and tracing.
- The Operate API's proposal endpoints return empty lists in the first wave, because code
  changes are GitHub pull requests.

## Evidence

E-05 (capture, clauses 8.1 and 8.2), E-14, E-40, E-46, E-47, E-220, E-229, E-254; U-30, U-41,
U-51.
