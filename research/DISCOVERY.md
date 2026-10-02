# Discovery Contract - Which fully automated multi-agent online income business (no YouTube Shorts) can a US operator build in 2026 on 200-1000 USD a month, and which GitHub and Hugging Face tooling does it rest on

Started 2026-10-02. This file is the definition of "enough information to build".
`node "$HOME/.agents/research-kit/bin/preflight.mjs"` reads it and blocks the build until every unknown
below is either `CLOSED` with evidence or `KNOWN-UNKNOWN` with a verification step.

## Build intent

KashMula is a multi-agent bot that runs an online business for one operator who is paid out
in the United States. Several cooperating agents (for example: market research, product or
content production, publishing/listing, sales and customer messages, and a finance/metrics
agent that decides what to do next) run on a schedule with as few human touchpoints as the
platforms legally allow. Running cost before revenue must stay within 200-1,000 USD a month
(AI APIs, hosting, paid tools). It must not depend on YouTube Shorts or short-form video
farms, and it must not depend on spam, fake engagement, ToS evasion or undisclosed AI or
affiliate links. Phase 1 (this research) chooses the business model and the stack, and
proves each decisive fact with a captured primary source. "Done" for the built bot means:
it runs unattended for 30 days on the chosen platforms without a policy strike, every
remaining human step is listed and takes under one hour a week, every cost is metered
against the budget, and it records real revenue (any amount, verified by the payment
processor) within the first 90 days, or it reports clearly why not.

## Unknowns

A fact belongs here when guessing it wrong changes the design: API limits and pricing,
auth model, data schemas, rate limits, licensing/ToS, platform behavior, current library
versions, competitor pricing, data availability.

Status is exactly one of:
- `CLOSED` - proven by an `E-##` row in `research/EVIDENCE.md` (which must point at cached raw text).
- `KNOWN-UNKNOWN` - unreachable now; the `Evidence` cell names the day-one verification step.

Anything else (`OPEN`, blank, "in progress") fails the gate.

| ID | Unknown | Why it blocks the build | Status | Evidence |
|---|---|---|---|---|

## Questions for the human (maximum 3)

Intent questions only - things no document can answer. Facts never go here; they go in
the table above. If a question's answer is in public documentation, it is a research
task, not a question.

Asked once, 2026-10-02, and answered by the operator:

1. Where is the money paid out? **United States.**
2. Monthly spend on tools and APIs before the bot earns? **200-1,000 USD a month.**
3. Which kinds of money-making to include? **"Suggest"** - the operator left it to the
   research. Chosen scope: selling products or services, content earning from ads,
   affiliate links or sponsorships, and agents doing paid work. Trading and crypto bots
   get a skeptical evidence check only, because they put the operator's capital at risk.

## Already decided

Locked decisions for this project. Do not revisit these without the human.

- Payout country: United States. Budget: 200-1,000 USD a month before revenue.
- No YouTube Shorts (operator's instruction); faceless short-form video farms are treated
  as out of scope too.
- As automatic as possible: several agents at once, least human in the loop.
- All research for this project runs through Research-Kit (the operator's instruction:
  "always use the research kit").
- The operator's own repositories may be reused ("take anything from here"), including
  DROPSCRAP (dropshipping research), which the operator is unsure about.
