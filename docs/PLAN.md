# KashMula: the plan

_Phase-1 result, 2026-10-03. Every claim below is tied to an unknown (`U-nn`) in
`research/DISCOVERY.md` or an evidence row (`E-nn`) in `research/EVIDENCE.md`, each of which
points at a cached capture of the page that owns the fact. The gate passes:
`preflight.mjs` prints PASS, 0 blocking._

## 1. The decision in one paragraph

Build **C1, a small portfolio of pay-per-event Actors on Apify Store**, first. It is the
only candidate where the three things that kill the others are all proven on the
platform's own pages for an Israeli resident with no US status: the payout rail (Apify pays
by PayPal, Wise or SWIFT from the Czech Republic with a $20 PayPal/Wise floor, E-04, E-05;
PayPal Israel's merchant receiving fees are published, E-197), the permission (Apify's
acceptable-use and agentic-payment rules, E-09, E-10) and the unit economics (profit =
0.8 x revenue minus platform usage at $0.20 per compute unit, E-06, E-08). What it does not
prove is demand and human time: Apify's "$1.6M paid out monthly to 4,500 developers" is
marketing (E-12), and the one first-person account says 15-20 hours a week for a 98-Actor
catalogue (E-14). So the first wave is 3-5 reliable Actors, not dozens, and the first 60
days of Store data decide the second wave (U-05, U-33). In parallel, and human-gated, open
an Etsy shop for **C6, disclosed AI-designed print-on-demand via Printify**: Etsy's own pages
list Israel for Etsy Payments with a 4.5% + 2 ILS processing fee (E-195, E-196), the AI
disclosure rules are explicit (E-63, E-64), and pre-revenue cost is tens of dollars; it has
zero revenue evidence, so it is a cheap experiment, not a bet. **C2/C8, a US customs and
tariff alert feed** sold by subscription through Paddle and listed on AWS Data Exchange, is
the month-2-3 option, conditional on four human checks (source reuse terms, Paddle
verification, Mailgun verification, Israeli VAT registration class). Everything else is out
of scope now (section 8).

## 2. Who the operator is, and what that rules out

- **Israeli tax resident, no US status** (operator's answer, 2026-10-02). No Stripe account
  of any kind can be opened: a US account needs a US-present owner or US registration plus
  an EIN and an SSN or ITIN (E-03), and Israel is on none of Stripe's three country lists
  (E-89, E-73, E-188). Stripe Managed Payments is therefore unavailable (U-09). Every design
  routes money through rails that accept an Israeli individual and keeps the payment layer
  behind one interface so a US-entity Stripe account could be added later (U-01, U-32).
- **US platforms will ask for Form W-8 BEN, never W-9** (E-02), and may withhold US tax
  unless treaty benefits are claimed (E-98; the treaty rate itself is not captured, U-32).
- **Israeli side (U-37, closed on gov.il and btl.gov.il pages):** register a dealer file with
  the Israel Tax Authority online (E-213); the 2026 exempt-dealer (osek patur) turnover
  ceiling is about 122,833 NIS (E-213, E-216), above which the dealer is an osek murshe and
  files VAT; AWS Data Exchange requires a VAT registration number for paid products (E-96),
  which pushes C8 toward osek murshe; register as self-employed with the National Insurance
  Institute (E-214, E-215). The zero-rate VAT position for services sold to foreign residents
  (VAT Law section 30(a)(5), E-217 and law-firm commentary) is the one point to settle with
  an Israeli CPA before the first invoice.
- **Agent stack available in Israel:** Anthropic's supported-countries page lists Israel
  (E-193) and so does OpenAI's API list (E-194). The Claude Agent SDK and API are used under
  the Commercial Terms with API keys only, never a claude.ai login (E-41, E-39), and every
  customer-facing agent session opens with an AI disclosure (E-40, U-14).

## 3. The ranked candidates

Scores are the adversarial verifiers' fit for this operator (0-100), after the follow-up
captures. "Unproven" means the platform rules and costs are known but no page shows money
being made at small scale.

| Rank | Candidate | Verdict | Score | What it rests on | What kills or caps it |
|---|---|---|---|---|---|
| 1 | **C1** Pay-per-event Actors on Apify Store, also sold to AI agents through Apify MCP and x402 | viable with conditions | 58 | Rail, permission and unit economics proven (E-04, E-05, E-06, E-08, E-09, E-10); agentic buyers pay in USDC with no account since 2026-06-26 (E-11); PayPal IL fees known (E-197) | Demand and human time unproven (E-12 marketing-grade, E-14 15-20 h/week anecdote); Apify changes terms unilaterally (rental retired 2026-10-01, E-08); scraping legality is wholly the creator's (E-05); tax documents Apify's KYC asks of a non-EU individual are not on any page (U-02) |
| 2 | **C6** Disclosed AI-designed print-on-demand on Etsy via Printify | unproven | 45 | Etsy Payments open to Israel with 4.5% + 2 ILS (E-195, E-196); AI and production-partner disclosure rules explicit (E-63, E-64); Seller App approved in minutes, own shop only (E-68); Printify API limits and indemnity known (E-66, E-67); Apache-2.0 image models (E-33) | No revenue evidence at all; Etsy's discretion over mass-produced items; all IP risk on the seller because API-created products skip Printify's quality check (E-67); AI-generated designs cannot be copyrighted, so nothing stops copying |
| 3 | **C2** Niche B2B data/alert feed by subscription (US customs and tariff change alerts first) | unproven | 34 | A pure alerts feed on published rule changes is outside "customs business" (19 CFR 111.1, E-97); sources are public with RSS (E-70) and a keyless API (E-203); Paddle accepts Israeli software sellers as merchant of record (E-90, E-28); DROPSCRAP's monitor code exists | CBP emails every bulletin free; redistribution terms of the Federal Register and CSMS are uncaptured (U-24); a qualified human must review generated alerts before dissemination (E-40); the only verified alert-feed comparable earns $0 (E-78) |
| 4 | **C8** The C2 feed listed on AWS Data Exchange | unproven | 33 | Israel is an eligible seller jurisdiction (E-95, E-96); publishing guidelines allow government-record data (E-200); sender fees published (E-199) | Needs a VAT registration number, a support organization, a Support-case qualification and a US or Hyperwallet bank account (E-96); no sale of any data product on the platform is in the corpus |
| 5 | **C7** Narrow Shopify App Store app | unproven | 32 | 0% revenue share on the first $1M lifetime, $19 registration, human app review (E-93, E-94); Partner payouts by PayPal, bank or wire depending on country (E-198) | Israel-specific payout confirmation and the Partner agreement are uncaptured (U-34); no payment-verified indie-app revenue in the corpus |
| 6 | **C3** Narrow AI document/image utility API on licensed open weights | unproven | 31 | GLM-OCR is MIT with an Apache-2.0 layout model (E-36); HF GPU rates per minute with scale-to-zero (E-56, E-57, E-192); Paddle as merchant of record (E-90) | No payment-verified comparable (CertTrack at $0, E-16); OCR quality claims conflict (94.62 vs 29.6 on different benches, U-13); background removal is price-collapsed and BiRefNet's dependency licences are unread (U-12, E-211) |
| 7 | **C4** Pay-per-call API or paid MCP tool via machine payments | unproven | 25 | Apify's agentic leg comes free with C1 once KYC is done (E-10); CDP facilitator fees known (E-22) | Stripe machine payments are closed to this operator (U-08); demand for a new seller is near zero (E-18, L); own-wallet USDC receipts have no proven payout or tax path |
| 8 | **C5** Human-approved niche digest newsletter on self-hosted Ghost | unproven | 23 | Ghost Admin API creates drafts (E-58); Mailgun prices known (E-191) | Ghost's only native payment provider is Stripe (E-189); sponsorship needs thousands of subscribers (E-113, S); every issue needs a qualified human review (E-40); Mailgun's AUP excludes affiliate marketing (E-190) |

## 4. Architecture: one loop, several agents, a hard policy layer

**Runtime.** Python. Pydantic AI (MIT) for typed agents with per-run `UsageLimits`; DBOS
Transact (MIT) for durable workflows, cron with exactly-once ticks, durable queues with rate
limits and a human-approval gate built on Postgres notifications (E-51, E-52, E-53). This
matches the operator's own rule R9 in the Agent repo: every run is a Postgres-backed durable
workflow from day one, with idempotency keys on every external write (E-54). Hosting: an
always-on Fly.io shared-cpu-1x Machine (1-2 GB, $6.70-12.70 a month) plus a Postgres
Machine, card on file (E-49, U-17). GitHub is for source, tests and image builds only:
its terms forbid running the business on Actions or hosting it on Pages (E-48). Tracing
through OpenTelemetry to a self-hosted Langfuse or any OTel backend.

**Models and cost control.** Claude through the API with an organization spend limit set
below the Start-tier $500 cap and per-workspace limits per product; HTTP 400 "usage limits"
and 429 spend-limit responses are circuit-breaker stop signals, not retries (E-43, U-15).
A two-tier router sends bulk work to Apache-2.0 open weights (Qwen3.8-27B, E-30) or
DeepSeek flash off-peak (E-46) through providers, with a price table that carries effective
dates (Gemini 3.8 Flash doubles on 2027-01-01, E-47; the HF router lists no unit, U-16).
Customer data never goes through a free tier that trains on it (E-47).

**The agents** (each a DBOS workflow, each with a budget):

| Agent | Does | Human gate |
|---|---|---|
| Scout | Finds niches where a lawful public source (government API, open data, user-supplied input) can be turned into a pay-per-event Actor; checks the source's terms before anything is built (U-04, U-24) | Approves each new niche (one line in the approval queue) |
| Builder | Generates the Actor from the operator's template: input and dataset schemas, PPE events, limited permissions, no Standby, README without external links (E-10, E-05) | None |
| QA | Runs the automated tests Apify's quality score rewards, then a 48-hour staged run; refuses to publish on failure (E-92, U-33) | None |
| Publisher | Publishes and prices (per-result event at or above platform cost / 0.8, tier discounts, raises only once a month with 14 days' notice, E-06, E-08) | None after the niche approval |
| Support | Triages Store issues and replies within hours (hard limit three business days), detects target-site changes, opens a Builder task | Escalations only |
| Finance | Logs cost per 1,000 results and paid users from Actor Analytics, flags any Actor floored at $0 profit, tracks the osek patur ceiling and each buyer's country for VAT reporting (U-03, U-37) | Monthly invoice review (auto-approves on day 14, E-04) |
| Compliance | The policy layer outside the model: no messaging, engagement, review or SEO-manipulation niches (E-09); AI disclosure on every customer-facing session (E-40); refunds auto-approved within a threshold and never deniable by an agent; no account or credential switching after a suspension; per-channel outbound rate limits; a kill switch coupled to the loop, not just to the trigger (U-30, E-86, E-87) | Changes to the policy itself |

For C6 the same skeleton runs a design agent (FLUX.2-klein-4B, Apache-2.0, E-33), a prepress
QA agent, an in-house IP and trademark screen (adapted from DROPSCRAP's `compliance.py`),
and a listing agent that writes the AI-use and production-partner disclosure into every
description (E-63, E-64) and stays under Etsy's and Printify's rate limits (E-66); a human
approves each design batch before it is listed.

## 5. Roadmap

| When | What | Human time |
|---|---|---|
| Week 0 | Apify identity verification and payout method; ITA dealer file and National Insurance registration with a CPA; PayPal Israel business account; Anthropic Console with spend caps; Fly.io card on file; Etsy shop and Printify account by hand | About 6-10 hours, once |
| Weeks 1-2 | Runtime skeleton (DBOS + Pydantic AI + Postgres on Fly.io), policy layer, price table, approval queue; first HTTP-only Actor from a lawful public source, built to the E-10 checklist, tested, staged 48 hours, published | Approve niche 1 |
| Weeks 3-8 | Actors 2-5 at most, each from an approved niche; Support and Finance agents live; C6: 10 approved designs listed, then wait 30 days for sales data before automating further | Under 1 hour a week plus design approvals |
| Day 60-90 | Read the Store data: visibility, runs, cost per 1,000 results, paid users, PayPal payouts; decide the second wave; expose the Actors to agentic buyers (free with KYC, E-10) | Half a day |
| Month 2-3, conditional | C2/C8 only after: Federal Register and CSMS reuse terms captured (U-24), Paddle verification passed (E-71, E-90), Mailgun verification recorded (E-190, E-191), CPA settles osek murshe for AWS's VAT rule (E-96, E-213) | Paddle and AWS onboarding, support inbox |

**Done, as defined in the contract:** the bot runs unattended for 30 days without a policy
strike, every remaining human step is listed and takes under one hour a week, every cost is
metered against the budget, and real revenue (verified by the payout) is recorded within 90
days, or the bot reports clearly why not.

## 6. Money

- **Before revenue, C1:** about $30-250 a month. Apify Creator plan $1 a month with $500
  bonus usage (E-13); platform usage for paid users' runs is netted against the 80% share
  (E-06); Fly.io $7-25 (E-49); Claude and routed models $20-150 with the caps above.
- **C6 adds** roughly $60-250 a month before any ads: Etsy's $0.20 listing fee and 6.5%
  transaction fee, Printify base costs, image generation on per-minute GPU (E-192).
- **Hard ceilings:** the Anthropic organization spend limit and workspace limits (E-43); a
  per-agent `UsageLimits` budget; DeepSeek bulk jobs outside its peak hours (E-46).
- **Payout timing:** Apify issues the invoice on the 11th, auto-approves on the 14th and
  pays on days 21-25 of the following month, once the $20 PayPal/Wise floor is crossed; a
  balance under the floor for 12 months is forfeited (E-04, E-05).

## 7. The human steps that cannot be automated

Identity verification at Apify (ID card or passport, E-04), Etsy (E-116), Paddle
(three phases, E-71), OpenAI and Anthropic organization setup; tax forms (W-8 BEN for each
US payer, E-02; the Israeli dealer file and National Insurance registration, E-213,
E-214); bank and PayPal accounts; approving each niche and each design batch; reviewing
generated content before it is published externally (E-40); disputes and refunds above the
auto-approve threshold; the monthly Apify invoice review (E-04). The corpus found no
platform that lets an agent clear a KYC wall, and the one documented attempt to run
revenue agents unattended ended in suspension, credential-switching and $0 (E-87).

## 8. Rejected, with the reason

Platform rule or law: Upwork and Fiverr auto-bidding (Upwork bans auto-proposals), MTurk and
Prolific task completion by agents, Shutterstock AI uploads, Medium Partner Program AI
writing behind the paywall, beehiiv AI-first newsletters (its AUP, E-59), unattended
Pinterest pinning and Reddit bots (E-82), programmatic SEO and affiliate page farms
(Google's scaled-content-abuse policy, E-80), mass social posting and cold email to
harvested addresses (CAN-SPAM, E-62), multi-accounting to stack free tiers, running the
bot on GitHub Actions or Pages (E-48), any Stripe-based checkout (U-01), and any
non-commercial or US-excluded model in a paid pipeline (U-11, U-12).

Evidence: dropshipping (the operator's own DROPSCRAP run produced 25 HOLD and 0 PASS
products and needs $3,000+ of capital), trading and prediction-market bots (no audited edge;
Kalshi takers average -31% after fees; StockeR's own status says "unvalidated hypothesis"),
autonomous code bounties (Algora bans robots, many projects ban AI pull requests, the market
collapsed), bug-bounty submission (human validation required by rule), agent labour
marketplaces (two boards paid $96.87 in total ever), "AI runs my business" info products
(95-99% revenue decay within six months on Stripe-verified data), Amazon KDP AI books
(capped at two titles a week, no revenue evidence), Adobe Stock AI portfolios (allowed with
a label, no revenue evidence), article-to-audio SaaS (popular TTS models non-commercial),
Kaggle competitions (a lottery), RapidAPI or MCP marketplaces as the primary channel (25%
take, PayPal-only, no earnings data).

## 9. What stays unknown, and who checks it on day one

Eighteen unknowns are KNOWN-UNKNOWN with a named day-one step (`research/BRIEF.md`, "Known
unknowns"). The ones that decide the first month: which tax documents Apify's KYC asks of an
Israeli individual (U-02); what a new creator actually earns and how many hours a week it
takes (U-05); how long a new Actor takes to appear in Store search and the MCP search tool
(U-33); whether the Federal Register and CSMS terms allow commercial redistribution (U-24);
the Israeli VAT zero-rate position and self-employed National Insurance rates (U-37, only
the registration and ceiling are on primary pages).

## 10. Reused from the operator's own repositories

DROPSCRAP: `search-light-signals` (keyless Federal Register, CBP CSMS and GDELT monitor with
per-source failure isolation) as the seed of the first lawful Actor and of C2's ingestion;
`compliance.py` as the C6 IP screen; `economics.py` for landed-margin pricing; `gate.py`'s
KILL/HOLD/PASS pattern where a PASS never authorises spend; strict API clients with per-run
budget ceilings. Agent repo: rule R9 and the cost-engineering notes (E-54). WindowRunner:
the eval harness as a regression gate before any Actor is published. Research-Kit: the
evidence gate before each new niche. DROPSCRAP's daily GitHub Actions cron must not be
copied: GitHub's terms forbid it for this use (E-48).

## 11. How the research was done

Research-Kit, end to end: a prior registered in the ledger before any page was fetched;
37 unknowns traced to 25 map rows; 219 captured pages with a hash-chained ledger; findings
rewritten by 19 reviewer agents and checked by 19 verifier agents (every quote anchor
grepped verbatim against its capture); eight candidates attacked by adversarial agents,
twice; a critic pass that found 17 owner pages the first collection missed, all captured;
`preflight.mjs` PASS with 0 blocking findings. The 100 or so remaining warnings are
quote anchors that are a single number from a pricing table cell, which the kit rates as
weak anchors; each sits next to the page it came from.
