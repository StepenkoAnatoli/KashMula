# MAP - topic decomposition

## Topic

Which fully automated multi-agent online income business (no YouTube Shorts) can a US operator build in 2026 on 200-1000 USD a month, and which GitHub and Hugging Face tooling does it rest on

## Subtopics

Statuses are blank on purpose: phase 0 gathers material, it does not judge. Mark each
row COVERED (cite the U-## rows that cover it), DISMISSED (reason required - dismissing
is fine, omitting is not), or GAP, and add topic-specific subtopics where the checklist
is not enough.

| ID | Subtopic | Why it matters | Status | Covered by |
|---|---|---|---|---|
| D-1 | Access model | Public pages, an official API, an auth-walled app, or a paywall - each is a different collection design | COVERED | U-04, U-08, U-20, U-22 |
| D-2 | Auth and credentials | What accounts, keys, or logins the collection and the product need, and who holds them | COVERED | U-01, U-02, U-08, U-14, U-25, U-32, U-35 |
| D-3 | Rate limits and quotas | Caps every cadence in the design, and caps the research collection itself | COVERED | U-15, U-23, U-24 |
| D-4 | ToS, licensing, legality of the intended use | A prohibition on automated collection, storage, or display ends the design for that source - and sometimes the project | COVERED | U-01, U-02, U-04, U-09, U-10, U-11, U-12, U-14, U-20, U-21, U-22, U-23, U-28, U-29, U-31, U-36 |
| D-5 | Data schema and its stability | How the data is shaped, and how often the source changes the shape without asking | COVERED | U-24 |
| D-6 | Freshness and staleness | How fast the data goes stale, and what staleness costs the product that depends on it | COVERED | U-16, U-24 |
| D-7 | Cost at expected volume | The economics at real usage, not the pricing page's first row - this decides viability | COVERED | U-03, U-08, U-09, U-15, U-16, U-17, U-19, U-26, U-31, U-37 |
| D-8 | Runtime and platform limits | Where this actually executes - OS, runtime version, desktop app, cloud - and what those limits forbid | COVERED | U-17, U-18, U-19 |
| D-9 | Output obtainability | Does the data your stated "done" depends on exist, and can you actually get it? Load-bearing: a project whose output cannot be produced should die in phase 1, not phase 2 | COVERED | U-06, U-07, U-12, U-13, U-33 |
| S-1 | Competitor set and its boundary | Who actually competes, and the rule that decides who is in | COVERED | U-05, U-06, U-07, U-33 |
| S-2 | Pricing and packaging | Published prices, what a tier includes, and where the real cost sits | COVERED | U-03, U-06, U-21 |
| S-3 | Positioning claims | What each player says it is for, in its own words | COVERED | U-28, U-29, U-36 |
| S-4 | Switching costs | What a customer pays to leave, in money and in effort | DISMISSED | dismissed: Not decision-changing at the model-selection stage. Customer switching costs matter only after a niche is chosen. Platform lock-in on the operator side (Apify unilateral term changes) is tracked under D-4/T-2 risks. |
| T-1 | Business-model viability and revenue evidence grade (payment-verified vs platform-claimed vs self-reported), including base rates | Every candidate rests on revenue claims of very uneven quality (TrustMRR Stripe data vs Apify self-report vs Indie Hackers' 'LabGPT $10 quadrillion/month'). The universal checklist does not ask whether the business earns at all. | COVERED | U-05, U-06, U-07, U-21, U-27, U-34 |
| T-2 | Payout rails, KYC and tax residency of the operator (W-9 vs W-8BEN, payout methods per platform, merchant-of-record eligibility by country) | KashMula assumes a US payout, but StockeR records the account holder as an Israeli tax resident. Apify does not pay US payees by ACH, Stripe needs an SSN/ITIN and a US address, and Stripe Managed Payments needs a supported location. This decides which candidates are even reachable. | COVERED | U-01, U-02, U-26, U-32, U-35, U-37 |
| T-3 | Unavoidable human touchpoints and the weekly human-time budget per candidate | The goal is minimal human time. Every scout found irreducible steps (KYC, tax, source legal review, support, editorial approval), and published maintenance figures conflict (8-11 h vs 15-20 h/week for 98 Actors). | COVERED | U-05, U-25, U-26, U-30, U-31, U-37 |
| T-4 | Licences of models whose outputs are sold (open-weight base-model licence, MaaS clauses, revenue caps, territory exclusions, closed-API commercial terms) | Trending models are often non-commercial or exclude the US, derivatives launder licences, and a Model-as-a-Service clause can bar a paid API with no revenue floor. | COVERED | U-11, U-12, U-13, U-14, U-23 |
| T-5 | Multi-agent orchestration, durability and scheduling framework choice | The business must run unattended for months. Durability, cron, HITL pause/resume and licence differ sharply (DBOS+Pydantic AI vs LangGraph needing an Enterprise licence for cron, AutoGen in maintenance mode), and the operator's own R9 rule constrains the choice. | COVERED | U-18 |
| T-6 | Spend guardrails and LLM cost routing (provider-side hard caps, per-agent budgets, two-tier routing) | The LLM bill is the swing cost within $200-1,000/month. Client-side cost estimates (Claude Agent SDK) must not drive financial decisions, and Anthropic spend tiers cap monthly spend. | COVERED | U-15, U-16 |
| T-7 | Compliant distribution and customer acquisition without spam | Each autonomous-business experiment failed at distribution or turned to spam (Ithiel's 1,617 GitHub issues and suspension, AI Village Telegraph posts). The candidates rank by whether a marketplace supplies demand. | COVERED | U-28, U-33, U-34, U-35 |
| T-8 | Payment processor and merchant-of-record acceptable-use fit for AI products | Gumroad bans selling AI tool access fulfilled off-platform, Lemon Squeezy bans services, Paddle bans likeness generation and human services, and Stripe Managed Payments accepts only fully automated digital products. The checkout choice constrains the product. | COVERED | U-09, U-10, U-32, U-34 |
| T-9 | Disclosure obligations (AI content, AI chatbots, affiliate and sponsorship) under platform rules and US state/federal law | Etsy, Adobe, KDP and Google require AI labelling; CA BPC 17941, Utah 13-77 and Maine LD 1727 cover bots; FTC 16 CFR 255 and 465 cover endorsements and fake reviews. These are hard ethical lines. | COVERED | U-14, U-22, U-29 |
| T-10 | Upstream data-source legality and reuse rights for data products and Actors | Data products are the best-evidenced model but the riskiest when built on scraped social data (AltIndex, asksynopsis). Only official APIs or open data with reuse rights qualify. | COVERED | U-04, U-24, U-36 |
| T-11 | Hosting and runtime ToS (where an always-on commercial bot may legally run) | GitHub Actions and Pages forbid this use, the operator's DROPSCRAP already violates the Actions terms, and HF Spaces billing and plan rules conflict across docs. | COVERED | U-17 |
| T-12 | Agent safety: misconduct drift, prompt injection from fetched content, and consumer-protection guardrails | Vending-Bench agents lied to suppliers, ignored refunds and colluded; bounty repos carry honeypot instructions; Project Vend nearly approved an illegal contract. An unattended business needs hard guardrails. | COVERED | U-30 |

## Coverage notes (per dimension)


Judged 2026-10-02 by the agent, from ten scout reports, a synthesis and a critic pass (phase 0 material), before collection. "COVERED" means the unknowns named in the row are the ones whose evidence must settle it; the evidence itself arrives with collection.

- **D-1** (COVERED; judged COVERED here): Access models documented on primary pages: Apify Store publishing and x402 agentic access (U-04), Stripe machine payments (U-08), Etsy Seller/Personal/Commercial tiers (U-23), Ghost Admin API vs beehiiv Enterprise-only (U-20).
- **D-2** (COVERED; judged COVERED here): Auth and KYC requirements identified: Stripe SSN/ITIN and US address (U-01, U-25), Apify ID verification (U-02), Paddle Sumsub (U-25), Anthropic API key only with no claude.ai login and no automated account creation (U-14). Residency remains open under T-2.
- **D-3** (GAP; judged COVERED here): Etsy, Printify and Anthropic spend tiers are covered (U-15, U-23). Apify Actor run limits and the upstream rate limits for the chosen niche (Federal Register, CBP) are not captured (U-24).
- **D-4** (COVERED; judged COVERED here): Extensive primary ToS and licence coverage: Apify AUP, processor AUPs, Etsy/Adobe/KDP/Google/Amazon rules, model licences, Anthropic terms, FTC/CAN-SPAM (U-04, U-10, U-11 to U-14, U-22, U-28, U-29). Pending capture of 403 pages via browser transport.
- **D-5** (GAP; judged COVERED here): Schema stability of the chosen upstream data sources is unknown. DROPSCRAP has already met drift (CJ /product/list deprecated, auth body changed). U-24.
- **D-6** (GAP; judged COVERED here): Prices and terms move quickly (Gemini doubles 2027-01-01, Hetzner +193% US, Apify rental retired, KDP cap changed 2026-09-21). There is no re-capture cadence, and the freshness the alert feed needs is undefined. U-16, U-24.
- **D-7** (COVERED; judged COVERED here): LLM, hosting, payment and MoR fees, and tax costs captured from primary pages (U-03, U-09, U-15, U-16, U-17, U-26). GPU cost per unit for C3/C6 is still to be measured (U-19).
- **D-8** (COVERED; judged COVERED here): Runtime limits and ToS: GitHub Actions/Pages prohibitions, Cloudflare cron CPU, Railway cron interval, DBOS durability, HF Spaces billing (U-17, U-18, U-19).
- **D-9** (GAP; judged COVERED here): Load-bearing and unresolved. Licences show outputs can legally be sold (U-11 to U-13), but no evidence yet shows agents can produce Actors, feeds or tools that paying customers buy (U-05, U-06, U-07, U-27).
- **S-1** (GAP; judged COVERED here): Only the aggregate count of 79,601 Apify tools is known. No niche-level competitor set for Actors, OCR/background APIs or tariff alerts (plan_queries; U-05, U-06).
- **S-2** (GAP; judged COVERED here): Platform fee structures are covered, but end-customer price points and packaging for each candidate are not (U-03, U-06, U-21).
- **S-3** (GAP; judged COVERED here): Allowed claims are bounded by FTC Operation AI Comply, the no-'AI-run'-hype rule and the disclosure laws (U-28, U-29). Actual positioning is not yet drafted or tested.
- **S-4** (DISMISSED; judged DISMISSED here): Not decision-changing at the model-selection stage. Customer switching costs matter only after a niche is chosen. Platform lock-in on the operator side (Apify unilateral term changes) is tracked under D-4/T-2 risks.
- **T-1** (COVERED; judged COVERED here): TrustMRR verified data, Apify self-reports, Felix decay, base rates and experiments catalogued (U-05, U-07, U-27). Candidate-specific demand remains under D-9.
- **T-2** (GAP; judged COVERED here): The tax-residency conflict (US vs Israeli resident) is unresolved, as are Apify tax-form handling and Stripe Managed Payments location eligibility (U-01, U-02, U-09).
- **T-3** (COVERED; judged COVERED here): Human touchpoints enumerated per candidate from primary pages (U-25, U-26). Weekly hours remain contested for Apify (U-05).
- **T-4** (COVERED; judged COVERED here): HF scout captured base-model licences, MaaS clauses, revenue caps and the US exclusion; planned models are all Apache-2.0 or MIT (U-11, U-12, U-13, U-23).
- **T-5** (COVERED; judged COVERED here): Framework scout compared licences, durability, scheduling and HITL. DBOS + Pydantic AI recommended, matching operator R9 (U-18).
- **T-6** (COVERED; judged COVERED here): Anthropic spend caps, Pydantic AI UsageLimits, Managed Agents budgets and two-tier routing costs captured (U-15, U-16).
- **T-7** (GAP; judged COVERED here): No compliant automated acquisition channel has been proven. Only the prohibitions are known (Google, Reddit, Pinterest, GitHub AUP) (U-28).
- **T-8** (COVERED; judged COVERED here): Gumroad, Paddle, Lemon Squeezy and Stripe AUPs and Managed Payments eligibility captured (U-09, U-10). The location question is under T-2.
- **T-9** (COVERED; judged COVERED here): CA/Utah/Maine bot laws, FTC 255/465, and Etsy/Adobe/KDP/Google labelling rules identified (U-22, U-29).
- **T-10** (GAP; judged COVERED here): Reuse rights for Federal Register/CBP/GDELT-derived products, and for any future Actor source, are not yet captured (U-04, U-24).
- **T-11** (COVERED; judged COVERED here): GitHub Actions/Pages prohibitions and alternative host pricing captured; HF hosting contradiction flagged (U-17, U-19).
- **T-12** (COVERED; judged COVERED here): Misconduct and prompt-injection evidence captured (Vending-Bench, Ithiel, Project Vend, honeypot repos) (U-30). The guardrail design itself is a build task.
- **D-4 note from the critic:** several decisive policy pages (Etsy help, creativity, API and fees; Reddit RBP; OpenAI organization verification; Utah 13-77; Upwork bots policy; Adobe helpx) were seen only through search snippets or answered 403 to a plain fetch. They are in the plan and must be captured, with the browser transport where the keyless route is refused, before their unknowns close.

## Candidate material

Gathered 2026-10-02 with recipe `market-research`.

Likely owners of these facts (by how often a search pointed at them):

- `youtube.com` (3)
- `medium.com/codex` (2)
- `x.com` (1)
- `play.google.com` (1)
- `leo-lihao.github.io` (1)
- `instagram.com` (1)

Candidate pages:

- [YouTube](https://www.youtube.com/)
- [Hugging Face Brings Open Source Models to GitHub Copilot ...](https://www.youtube.com/watch?v=3Tgyt_ucN_k)
- [YouTube](https://x.com/YouTube)
- [5 Insane Features on Hugging Face You Should Know](https://medium.com/codex/insane-features-on-hugging-face-you-should-know-not-just-as-a-developer-dc33704d6ade)
- [YouTube - Apps on Google Play](https://play.google.com/store/apps/details?id=com.google.android.youtube&hl=en_US)
- [Tracing License Drift in the Open-Source AI Ecosystem](https://leo-lihao.github.io/files/P10.pdf)
- [YouTube - Instagram photos and videos](https://www.instagram.com/youtube/?hl=en)
- [Hugging Face Is the Public Square for AI. But What If Your ...](https://medium.com/@OpenCSG/hugging-face-is-the-public-square-for-ai-but-what-if-your-enterprise-needs-a-private-fortress-5bb9ae6d41b7)
- [YouTube](https://www.linkedin.com/company/youtube)
- [Does anyone know of any github projects that use ...](https://www.reddit.com/r/huggingface/comments/1hm2k7v/does_anyone_know_of_any_github_projects_that_use/)
- [Harmful or dangerous content policy - YouTube Help](https://support.google.com/youtube/answer/2801964?hl=en)
- [Discover the world of AI with GitHub and HuggingFace](https://www.youtube.com/watch?v=IujHK8qcPX4)
- [The Complete Hugging Face Ecosystem Guide](https://blog.ecitis.org/huggingface-ecosystem-guide/)
- [What does this do that huggingface, github, etc. doesn't ...](https://news.ycombinator.com/item?id=49766585)

## Outlines seen in the material

_No outlines - none of these pages is captured yet. `--max-scrapes <n>` captures the first n; their headings appear here._

