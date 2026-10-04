# 0009. Actors are self-contained, deterministic Python projects copied from a template

- Date: 2026-10-04
- Status: proposed

## Context

What the platform requires of an Actor's files and code:

- `apify push` deploys from `.actor/actor.json` at an Actor's root and creates or updates the
  Actor named there (E-247, E-255).
- Store publishing needs an output schema (E-249). The input schema's `prefill` drives Apify's
  daily test, which expects a non-empty dataset within five minutes (E-248, E-256).
- The Python SDK (`apify==4.0.2`, Python 3.11 or later, U-38) gives the lifecycle, input,
  storage and test-storage facts (E-239 to E-243; U-47).
- Limited permissions need no changes for default storages (E-251, E-252; U-50).

The seed source code, DROPSCRAP's `search-light-signals`, is JavaScript (repository read at
`f200c11`). The runtime package's declared code paths are `src`, `lib`, `bin`, `scripts` and
`app` (`research/kit.json`).

## Decision

- **Layout.**
  - Each Actor is a self-contained project at `actors/<slug>/`, beside the runtime package in
    `src/kashmula/`.
  - The project holds every definition file under `.actor/` (`actor.json`, input, output and
    dataset schemas, README, CHANGELOG, Dockerfile), named explicitly in `actor.json` (E-247),
    plus `requirements.txt`, `src/` and `tests/`.
  - Actors import nothing from `kashmula`. New Actors are copies of `actors/_template`, which is
    itself checked and tested.
- **Behaviour.** Actors are Python and deterministic. They read a lawful public source within a
  per-run request ceiling and make no model call at run time.
- **Port, not copy.** `search-light-signals` is ported to Python as a design (per-source
  isolation, shape errors, stable item ids). No code is copied.
- **Architecture-map rule.** The phase-1 pull request adds `actors` to `codePaths` in
  `research/kit.json`, so Actor commits stage `docs/ARCHITECTURE.md`. The operator approves that
  configuration change by merging.
- **Hidden oracles.** Each oracle is written by a separate sub-agent before the build, held
  outside the builder's worktree, and committed under `qa/oracles/<slug>/` after the build as a
  regression test.

## Alternatives rejected and why

- **Actors inside `src/kashmula/`.** Deployable Actor roots would be mixed into the runtime
  package, and a runtime change could break a live Actor.
- **A shared Actor library imported by every Actor.** Three to five Actors do not justify it.
  Each Actor's Docker build would need the library shipped into its context.
- **Generated Actor versions stored as content-addressed bundles in the database and pushed by
  the runtime** (Approach 2). Code would reach paid Actors without entering a reviewed pull
  request, against the Operate spec.
- **Shipping `search-light-signals` as a Node Actor.** The template, tests and pins are Python
  (U-38, U-47). Facts about the JavaScript SDK are not in the corpus beyond samples (E-252).
- **Actors that call a language model at run time.** Their output would carry E-40's
  AI-content duties, model cost would come out of the 80% share (E-06), and run time would
  threaten the five-minute daily test (E-256).
- **Keeping `actors/` outside the declared code paths.** The architecture-map rule would not
  apply to the code that earns the money.

## Consequences

- A fix to the template does not reach existing Actors automatically. Each Actor takes it in its
  own pull request, which is acceptable at five Actors.
- The Actor's Dockerfile base image and the CLI's local-run flow are not in the corpus. Phase 1
  collects them before writing the template.
- `tests/guards.toml` and the template checker cover every Actor the same way.

## Evidence

E-05, E-06, E-10, E-40, E-239, E-240, E-241, E-242, E-243, E-247, E-248, E-249, E-250, E-251,
E-252, E-255, E-256; U-38, U-47, U-49, U-50.
