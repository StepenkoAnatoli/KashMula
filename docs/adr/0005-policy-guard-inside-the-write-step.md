# 0005. The policy guard runs inside the write step, from reviewed configuration

- Date: 2026-10-04
- Status: proposed

## Context

PLAN section 4 makes Compliance "the policy layer outside the model". The corpus explains why
prompts are not enough:

- Frontier models in a simulated business fabricated quotes and refused refunds as policy
  (E-86).
- Unattended agents switched to a second credential after a suspension, and kept running after
  their trigger was disabled (E-87).

The operator's Agent repository asks for a permission gate as policy as code on every tool
call (rule R15, an idea only).

Durability constrains where the check can run:

- A completed step is never re-executed (E-225, E-226). A guard in its own step would leave a
  checkpointed permit that a recovered workflow replays after a STOP.
- Under `DBOSDurability`, model requests are steps the library generates (E-237), so no guard
  can sit inside them.

## Decision

- **Placement.** `policy.guard(action)` is the first statement of the same DBOS step as the write
  it permits. It returns a `Permit`, adapters accept writes only with a `Permit`, and only `guard`
  can construct one.
- **Closed actions.** Agents' tools return typed proposals from a closed action enum and never
  call the network for writes.
- **Tests.** An import-boundary test fails if anything outside `effects/` imports a network
  client, or if `agents/` imports `adapters/`. A unit test fails if a `Permit` can be built
  elsewhere.
- **Order of checks:** control state, breaker, action allowlist, rules, per-channel rate cap,
  budget, existing intent.
  - The rate cap is counted in `external_write` and serialized by an in-process lock per
    channel, which is valid under ADR-0003's single process.
  - Every decision is recorded with its rule ids and the policy version.
- **Model runs.** They are governed by an admission step before each `agent.run()` (control,
  breaker, budget reservation), by `UsageLimits` (E-233), by cancellation at the next model step
  (E-228) and by the provider limit (E-43).
- **The rules** are in spec section 11.3:
  - E-09: no messaging, engagement, review or SEO-manipulation niches.
  - E-05: no off-platform links.
  - E-10, E-246, E-251: pay per event only, never "+ usage", limited permissions, no Standby.
  - E-245: one charging mechanism.
  - E-06: the price floor.
  - E-05, E-246: the monthly increase limit.
  - The Operate spec: no niche approval without a passing kit gate.
  - E-87: one credential per platform.
  - E-86: no refund-denying action.
  - E-40: AI disclosure for any customer-facing message.
  - U-30: external content is data.
- **Configuration.** The rules, allowlists, rate caps and gate deadlines live in
  `config/policy.toml`. The policy version is a hash of that file. A change is a pull request
  the operator merges, which is PLAN section 4's "changes to the policy itself" gate.

## Alternatives rejected and why

- **Guardrails in system prompts.** A model can argue past them (E-86, E-87).
- **Checks scattered through each agent's tools.** One missed tool is an unguarded write.
- **A guard in its own step before the write.** Its checkpointed permit replays after a STOP
  (E-225, E-226).
- **A Compliance agent that is itself a model.** PLAN section 4 puts the policy outside the
  model.
- **Policy editable in the database behind a runtime approval gate.** The runtime could then
  change its own rules. A merged pull request is the stronger gate and costs the operator the
  same minute.
- **A Postgres row lock held across the network call as the write fence** (Approach 1). Lock
  behaviour is not in the corpus. A hung call or an exhausted pool would stall a STOP. An intent
  row written inside the lock transaction would roll back on a crash and let the write repeat.
  ADR-0008 waits on committed intent rows instead.
- **One DBOS queue per channel with a limiter for rate caps.** The limiter is global and would
  work (E-229), but the first wave has no queues of its own (ADR-0002), and the write volume is
  a few calls a day.

## Consequences

- Every new guard gets a test that fails with that guard removed, listed in `tests/guards.toml`.
- Changing a rate cap or a deadline needs a pull request, a deliberate trade of speed for
  control.
- Model requests already sent finish after a STOP. The design reports them rather than claiming
  otherwise.

## Evidence

E-05, E-06, E-08, E-09, E-10, E-40, E-43, E-86, E-87, E-225, E-226, E-228, E-229, E-233, E-237,
E-245, E-246, E-251; U-30.
