# 0007. Approval gates: table-backed workflows, digest-bound decisions, CLI first

- Date: 2026-10-04
- Status: proposed

## Context

PLAN section 7 keeps human gates: niche approval, price changes, reviewing generated content, and
refunds and disputes above a threshold. The merged Operate spec defines how Moonzila will answer
them over an HTTPS API that the runtime serves:

- A decision is journaled before it is sent.
- A decision carries the digest of the evidence it was taken on.
- A decision is idempotent by gate id and digest, and a second decision with a different digest
  is refused.
- An unanswered gate stays open, and the runtime decides what that means.
- A niche approval without a passing kit gate is refused by the runtime.

The DBOS primitives:

- `DBOS.recv(topic, timeout_seconds)` waits inside a workflow and returns `None` on timeout.
- `DBOS.send` with an `idempotency_key` delivers once per destination, even from plain Python
  (E-228, E-230).
- The DBOS Client can send (E-230), but its signature is not captured.

## Decision

- **A gate is a workflow** under `gate:<kind>:<subject>:<evidence12>`.
  - The `gate` and `gate_decision` tables are the record of truth. A message only wakes the
    workflow.
  - The workflow loops: a step reads the decision and the clock, and between reads the workflow
    waits on `DBOS.recv(topic="wake", timeout_seconds=3600)`.
  - Past its deadline the gate becomes EXPIRED and nothing happens. Deadlines per kind are in
    `config/policy.toml`.
- **A decision** is one transaction: check PENDING and the evidence digest, insert the
  `gate_decision` row (primary key `gate_id`), set the state, append the journal row.
  - The same decision repeated is answered as a repeat.
  - A different digest, a different verdict, or an expired gate is refused.
- **Waking the gate.** The API path wakes the gate at once with
  `DBOS.send(..., topic="wake", idempotency_key=<request id>)`. The CLI path does the same
  through `DBOSClient` if a phase-2 check confirms its signature; otherwise the decision takes
  effect at the next timeout.
- **Weekly digest.** Gates are batched into a weekly digest of one-line cards. Each card shows
  the recommendation, the digest, the deadline and the default "nothing happens", and is
  answered as `kashmula approve <handle>` or `kashmula reject <handle> "<note>"`. The handle
  carries the digest, so an approval is always bound to what was shown.
- **CLI first.** The CLI arrives in phase 2. The Operate API v1 arrives in phase 4 and calls the
  same service functions.
  - The Pydantic models are frozen in phase 2 in `src/kashmula/contracts.py` and mirrored in
    `docs/contracts/operate-api.md`.
  - The bearer token is stored as a SHA-256 hash.
  - `GET /v1/proposals` returns an empty list in the first wave, because code changes are GitHub
    pull requests.
- **No gate causes an external write by itself** in the first wave. Approving records a
  decision; the action is manual (Console) or a later admitted workflow.

## Alternatives rejected and why

- **DBOS messages as the only approval record.** Message retention and size limits are not in
  the corpus (U-42 residual). The Operate contract also needs a queryable, digest-checked
  record.
- **A CLI that launches DBOS to send decisions.** That makes a second DBOS executor
  (ADR-0003).
- **Approving on timeout.** The Operate spec forbids auto-approval, and the Agent repository's
  rule is default deny.
- **Gates enforced only in the UI.** The Operate spec requires the runtime to refuse.
- **Building the HTTPS API in the first runtime phase.** Its framework, TLS and ingress are
  phase-4 research. Freezing the models early gives Moonzila the contract without the server.
- **Separate logic for the CLI and the API.** The two surfaces would drift.
- **A notification per gate instead of a weekly digest.** Every gate would interrupt the
  operator, and the digest answers the same gates in one sitting.

## Consequences

- A CLI decision may take up to an hour to wake its gate, until the `DBOSClient` send signature
  is confirmed.
- A gate workflow's step history grows by a few dozen steps a day while it waits.
- Moonzila builds against `docs/contracts/operate-api.md` from phase 2 on.
- A niche gate needs a readiness record: package digest, preflight exit code 0, commit SHA.

## Evidence

E-223, E-228, E-230, E-51 (capture), E-52 (capture); U-42; the Operate spec
(`moonaliza/docs/specification/operate-mode.md`); the Agent repository's approval rule
(`docs/core/08-ux-product.md`, idea only).
