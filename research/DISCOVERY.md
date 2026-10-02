# Discovery Contract - Which fully automated multi-agent online income business (no YouTube Shorts) can a US operator build in 2026 on 200-1000 USD a month, and which GitHub and Hugging Face tooling does it rest on

Started 2026-10-02. This file is the definition of "enough information to build".
`node "$HOME/.agents/research-kit/bin/preflight.mjs"` reads it and blocks the build until every unknown
below is either `CLOSED` with evidence or `KNOWN-UNKNOWN` with a verification step.

## Build intent

KashMula is a multi-agent bot that runs an online business for one operator, an Israeli
tax resident selling to US and worldwide customers (see the correction under Already
decided). Several cooperating agents (for example: market research, product or
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
| U-01 | The operator is an Israeli tax resident with no US status (operator's answer, 2026-10-02). Given that: is a US Stripe account possible at all without a US-present owner and SSN/ITIN, is Israel a Stripe-supported business country, and which US form (W-8BEN) do US platforms and marketplaces require from a foreign individual? | This decides whether any Stripe-based checkout is open to the operator, and which tax paperwork every US platform will demand before paying out. Every candidate's onboarding depends on it. (candidates: C1, C2, C3, C4, C5, C6; map: T-2, D-2, D-4) | OPEN | |
| U-02 | How exactly does Apify pay a US (or non-US) individual: which payout methods (PayPal/Wise/SWIFT; no ACH), what KYC steps, which tax forms (W-9/1099 or W-8BEN), and what happens to sub-minimum balances? | Payout friction and tax handling could make C1 impractical for this operator. The payout pages do not mention US tax forms. (candidates: C1; map: T-2, D-2, D-4) | OPEN | |
| U-03 | What are Apify platform usage costs per Actor run compared with a viable pay-per-event price, and is rental pricing fully retired so that PPE is the only monetisation path? | Profit = 0.8 x revenue - platform costs. A compute-heavy Actor can be loss-making even with users. The pricing model was changed unilaterally on 2026-10-01. (candidates: C1; map: D-7, S-2) | OPEN | |
| U-04 | Which Actor content does Apify's acceptable-use policy permit, and what conditions make an Actor eligible for agentic x402/MCP payments (PPE pricing, limited permissions, no Standby, developer KYC)? | Defines which Actor niches are allowed and whether the agent sales channel (and so C4 via Apify) is available. (candidates: C1, C4; map: D-1, D-4, T-10) | OPEN | |
| U-05 | What does a new Apify creator actually earn, and how many hours a week does maintenance take (8-11 h vs 15-20 h reported for the same 98-Actor developer)? | The $1.6M/4,500 figure is self-reported and the human-time figures conflict. Both drive the C1 vs C2/C3 ranking and the minimal-human-time goal. (candidates: C1; map: T-1, T-3, S-1) | OPEN | |
| U-06 | Will customers pay for a narrow AI OCR-to-JSON or background-removal tool, at what price points relative to competitors, and what do comparable indie tools verifiably earn? | C3's existence depends on demand and on a price that covers GPU cost. Only one claimed comparable (CoverLetterGPT) is known. (candidates: C3; map: S-1, S-2, T-1, D-9) | OPEN | |
| U-07 | What is the real, wash-adjusted demand for paid agent-to-agent API calls (x402/MPP) per seller today? | Decides whether C4 is worth building beyond a free add-on, and whether agentic payments materially lift C1. (candidates: C4, C1; map: T-1, S-1, D-9) | OPEN | |
| U-08 | Can the operator's Stripe account accept machine payments (state eligibility, New York exclusion, the crypto enablement review), and what are the facilitator settlement costs and limits? | C4 is blocked if the account or state is ineligible, and the per-call economics depend on the minimums ($0.50 by card, 0.01 USDC) and fees. (candidates: C4; map: D-1, D-2, D-7) | OPEN | |
| U-09 | Does our product qualify for Stripe Managed Payments ('fully automated digital product', eligible tax codes, supported business location), given that C2 includes a human editorial review step? | If it does not qualify, the operator must handle sales-tax nexus and disputes or switch to Paddle. That changes cost (3.5% vs 5% + 50c) and the human workload. (candidates: C2, C3, C5; map: T-8, D-4, D-7) | OPEN | |
| U-10 | Which processors' acceptable-use policies permit selling AI tool subscriptions and AI-generated digital goods (Gumroad AI-services ban, Paddle likeness and human-service bans, Stripe restricted list)? | Choosing a prohibited processor gets the account closed and funds held. (candidates: C2, C3, C4, C6; map: T-8, D-4) | OPEN | |
| U-11 | Are the text LLMs we would ship outputs from licensed for commercial and paid-API use without MaaS clauses (Qwen3.8-27B Apache-2.0, gpt-oss USAGE_POLICY, the Gemma 4 prohibited-use policy)? | A MaaS clause or usage policy could make a paid API or data product a licence breach. Qwen3.8-Flash-Next already shows such a clause with no revenue floor. (candidates: C2, C3, C4, C5; map: T-4, D-4) | OPEN | |
| U-12 | Do the image models planned for C3/C6 (FLUX.2-klein-4B, BiRefNet, Qwen-Image-Edit-2511) carry clean commercial licences on the base model and every dependency? | Licence laundering is common, and the popular alternatives (RMBG-2.0, FLUX dev-family, Qwen-Image-2.1) are non-commercial. A wrong pick makes every sale infringing. (candidates: C3, C6; map: T-4, D-4, D-9) | OPEN | |
| U-13 | Are the OCR models we would serve (GLM-OCR, DeepSeek-OCR-2, PaddleOCR-VL) free of revenue caps and non-compete clauses, and good enough to sell? | Chandra and Surya carry caps and a non-compete, and jina-ocr is NC. Output quality decides whether C3's OCR variant can be sold. (candidates: C3; map: T-4, D-9) | OPEN | |
| U-14 | What do Anthropic's Commercial Terms and AUP require for an unattended commercial agent loop (no automated account creation, AI disclosure in consumer-facing agents, no claude.ai login), and does the Claude Agent SDK's MIT LICENSE or the Commercial Terms govern it? | Using a subscription login or failing to disclose AI would breach terms. The answer constrains auth and customer-facing design. (candidates: C1, C2, C3, C4, C5, C6; map: D-2, D-4, T-4, T-9) | OPEN | |
| U-15 | What will frontier-model tokens cost at expected volume, and can hard provider-side monthly spend caps be enforced (Anthropic Start $500 / Build $1,000 tiers, custom limits returning HTTP 400)? | The LLM bill is the main cost; without a provider-side cap a runaway agent can blow the $200-1,000 budget. (candidates: C1, C2, C3, C4, C5, C6; map: D-7, D-3, T-6) | OPEN | |
| U-16 | What do cheap routed models (gpt-oss-120b, deepseek-flash, Gemini 3.8 Flash before and after its 2027-01-01 price doubling) cost per 1M tokens, and in what units does the HF router list prices? | Two-tier routing is what keeps the stack inside budget. The HF router omits units, and the Gemini price doubles on 2027-01-01. (candidates: C1, C2, C3, C5; map: D-7, D-6, T-6) | OPEN | |
| U-17 | Where can the always-on bot run within ToS and budget (GitHub Actions and Pages prohibitions confirmed; Fly.io, Cloudflare Workers, VPS costs)? | The operator's existing scheduler pattern (DROPSCRAP on GitHub-hosted Actions) is prohibited for this use, so a host must be chosen and budgeted. (candidates: C1, C2, C3, C4, C5, C6; map: D-8, D-7, T-11) | OPEN | |
| U-18 | Does DBOS Transact with Pydantic AI give exactly-once cron, durable queues with rate limits, and a HITL approval gate on Postgres alone, satisfying the operator's rule R9? | The loop's reliability and human-approval design depend on the orchestration backbone. Choosing LangGraph instead would need an external scheduler or an Enterprise licence. (candidates: C1, C2, C3, C5, C6; map: T-5, D-8) | OPEN | |
| U-19 | What is the GPU cost per image or page for C3/C6 on HF Jobs, Endpoints or ZeroGPU, and can a free or PRO HF account host a Gradio/Docker Space at all (the docs conflict)? | Unit GPU cost decides C3's price floor and margin, and the HF hosting contradiction could force a different host. (candidates: C3, C6; map: D-7, D-8) | OPEN | |
| U-20 | Can self-hosted Ghost create draft posts and run paid Stripe memberships via the Admin API, and does beehiiv's AUP or Enterprise-only post API rule it out as the alternative? | Picks the C5 platform. beehiiv's AUP bans fully AI-generated and affiliate-primary newsletters. (candidates: C5, C2; map: D-1, D-4) | OPEN | |
| U-21 | What can a small, disclosed, human-approved niche newsletter realistically earn from sponsorships or ad networks, and what does CAN-SPAM require of an automated sender? | C5 has no revenue evidence at all, and CAN-SPAM penalties are up to $53,088 per email. (candidates: C5, C2; map: T-1, S-2, D-4) | OPEN | |
| U-22 | What exactly do Etsy's current rules require for AI-designed POD items (disclosure wording, 'Designed by' scope, the prompt-bundle ban) and for automated access (API terms on scraping, Seller App scope)? | Non-compliance risks shop suspension, and trend research must not scrape Etsy. The pages returned 403 to plain fetch, so the kit must capture them with a browser transport. (candidates: C6; map: D-4, D-1, T-9) | OPEN | |
| U-23 | What are the current Etsy and Printify API rate limits and terms at volume (per-app query-per-day caps, the 200 publishes per 30 minutes limit, IP indemnity, products created via API skipping the quality check), and is FLUX.1-schnell's output commercially clean? | Limits cap listing throughput, and the indemnity puts all IP risk on the operator. (candidates: C6; map: D-3, D-4, T-4) | OPEN | |
| U-24 | Do the Federal Register API and CBP CSMS terms allow commercial redistribution of derived alerts, and what are their schema stability and rate limits? | C2's first niche, and possibly a C1 Actor, is built on these sources. Any reuse restriction or schema churn changes feasibility. (candidates: C2, C1; map: T-10, D-5, D-6, D-3) | OPEN | |
| U-25 | Which identity and verification steps are unavoidable for each provider (Paddle Sumsub/liveness and domain review, OpenAI Verified Organization ID, Stripe first-payout timing)? | These are the fixed human touchpoints in the setup budget, and some (OpenAI ID) gate model access. (candidates: C1, C2, C3, C4, C5, C6; map: T-3, D-2) | OPEN | |
| U-26 | What recurring US tax obligations apply at small revenue (1099-K thresholds, 15.3% self-employment tax, quarterly estimated payments)? | These are recurring human touchpoints and net-margin drags that apply to every candidate, if the operator is a US person (see U-01). (candidates: C1, C2, C3, C4, C5, C6; map: T-2, T-3, D-7) | OPEN | |
| U-27 | What is the payment-verified revenue distribution for small data products, APIs and micro-SaaS (TrustMRR), and do the verified examples (AltIndex, isMalicious) hold up on capture? | This is the main evidence that ranks C2 and C3 above content candidates. A biased or misread sample would reorder the shortlist. (candidates: C2, C3; map: T-1) | OPEN | |
| U-28 | Which customer-acquisition channels can an agent use without breaching platform rules (Google scaled-content and gen-AI guidance, Reddit's Responsible Builder Policy)? | Distribution is the bottleneck for C2, C3 and C5. If no compliant automated channel exists, human time rises sharply. (candidates: C2, C3, C5, C6; map: T-7, D-4, S-3) | OPEN | |
| U-29 | What AI-chatbot and affiliate/sponsorship disclosure must customer-facing agents and content carry (CA BPC 17941, Utah 13-77, FTC endorsement guidance on placing disclosure near the link)? | These are hard legal lines for support bots, newsletters and sponsored content. (candidates: C2, C3, C5, C6; map: T-9, D-4, S-3) | OPEN | |
| U-30 | What guardrails do unattended business agents need, based on documented misconduct and failure modes (fabricated supplier quotes, ignored refunds, collusion, spam, ban evasion, prompt-injection honeypots)? | Without hard guardrails the bot can commit consumer-protection or ToS violations that end the business. (candidates: C1, C2, C3, C4, C5, C6; map: T-12, T-3) | OPEN | |
| U-31 | Self-hosted Ghost supports only Mailgun for bulk newsletter email. What are Mailgun's cost at the expected list size, its acceptable-use policy (including AI-generated or automated content) and its account verification steps? | C5 cannot send newsletters without it, and it is an unbudgeted cost and an extra KYC touchpoint. The synthesis currently lists email delivery cost as 'not captured'. (candidates: C5, C2; map: D-7, D-4, T-3) | OPEN | |
| U-32 | Under each residency answer (US person vs Israeli resident), which checkout and payout rails are open: a Stripe account (country list), Stripe Managed Payments locations, Paddle supported seller countries, AWS Marketplace seller eligibility? What US withholding applies via W-8BEN under the US-Israel tax treaty? | If Stripe is unavailable, C4 as written and the named checkout for C2/C3/C5 are blocked, which reorders the shortlist toward C1 and the marketplace channels. (candidates: C1, C2, C3, C4, C5; map: T-2, T-8, D-2) | OPEN | |
| U-33 | How does Apify's Actor quality score (reliability, automated QA tests, other factors) govern ranking in Apify Store search and in the Apify MCP search-actors tool used by AI agents? How long do new Actors take to become visible? | C1's demand comes from marketplace discovery in both the human and agent channels. A cold-start penalty changes time-to-first-revenue and the case for many narrow Actors versus a few strong ones. (candidates: C1, C4; map: T-7, D-9, S-1) | OPEN | |
| U-34 | What are the Shopify App Store's current revenue share, registration fee, app-review requirements and payout methods for the operator's jurisdiction? Is there any payment-verified evidence of revenue for small indie apps? | This decides whether a second buyer-supplying marketplace belongs on the shortlist next to C1. (candidates: C1, C2, C3; map: T-1, T-7, T-8) | OPEN | |
| U-35 | Can the operator list a paid data product on AWS Data Exchange: jurisdiction eligibility, the onboarding case, support obligations, the fee structure and the tax and bank requirements for US vs non-US sellers? | It would give C2 a compliant marketplace channel that works if Stripe is unavailable. (candidates: C2; map: T-2, T-7, D-2) | OPEN | |
| U-36 | Does selling tariff, de-minimis and classification alerts or landed-cost estimates to importers fall within 'customs business', which only licensed customs brokers may conduct (19 CFR 111.1)? What wording keeps the product informational? | If the product strays into customs business it is unlicensed activity. This decides how C2's first niche must be scoped and worded. (candidates: C2, C1; map: D-4, T-10, S-3) | OPEN | |
| U-37 | If the operator is an Israeli tax resident, which Israeli registrations and filings apply to foreign-platform income (business registration type, VAT on digital services sold abroad, advance tax payments)? No owning primary URL has been identified yet; an Israel Tax Authority (gov.il) page must be found. | These are recurring human touchpoints and margin drags under the non-US branch, and U-26 covers only US taxes. (candidates: C1, C2, C3, C4, C5, C6; map: T-2, T-3, D-7) | OPEN | |

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

One follow-up to question 1, asked after the scouts found a conflict with the StockeR
repository's owner note: **"Israeli resident, no US status."** Recorded under Already
decided. It is a fact about the operator, which no page could have answered.

## Already decided

Locked decisions for this project. Do not revisit these without the human.

- **Correction, 2026-10-02 (operator's answer to the residency question):** the operator is
  an **Israeli tax resident with no US status**. The first answer ("United States") meant
  that US platforms and US customers are fine, not that the operator is a US person. So:
  no US Stripe account (it needs a US-present owner with an SSN or ITIN), W-8BEN rather
  than W-9, and the checkout/payout rails must be ones open to an Israeli seller (Paddle,
  PayPal/Wise/SWIFT payouts, marketplaces that pay Israeli sellers). The project topic
  string still says "US operator"; read it as "operator selling to US and worldwide
  customers". Budget: 200-1,000 USD a month before revenue.
- No YouTube Shorts (operator's instruction); faceless short-form video farms are treated
  as out of scope too.
- As automatic as possible: several agents at once, least human in the loop.
- All research for this project runs through Research-Kit (the operator's instruction:
  "always use the research kit").
- The operator's own repositories may be reused ("take anything from here"), including
  DROPSCRAP (dropshipping research), which the operator is unsure about.
