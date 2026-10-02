---
url: https://blog.apify.com/building-98-actors-on-apify-store/
retrieved: 2026-10-02
command: firecrawl scrape https://blog.apify.com/building-98-actors-on-apify-store/ --only-main-content --json
statusCode: 200
transport: firecrawl-cli
completeness: full
title: How I built 98 Actors on Apify Store in 6 months
---
👉

This article was written by [Olivier Reynaud](https://apify.com/silentflow) as part of [Write for Apify](https://apify.com/resources/write-for-apify) \- a program for developers sharing original articles about what they've built with Apify.

On a Sunday afternoon in November 2025, I pushed my first scraper to Apify Store. It pulled rental listings from Leboncoin, the French classifieds site where most apartments are listed before they ever reach a dedicated real estate portal. I gave it a generic name, wrote a README that read like an API reference, and went to bed refreshing the Actor page every two hours. A full week passed before anyone ran it.

Six months later, my profile showed 98 public Actors, 2,500 total users, 855 monthly active users, a 98.8% run-success rate, and a 6.2-hour average response time on issues. Almost everything I assumed in November about how Apify Store works was wrong, and almost everything that ended up working was non-obvious.

This is what I actually learned: not how to write a scraper, but how to build, price, ship, and maintain a catalog of them on Apify.

## Why Apify (and not building my own SaaS)

Before Apify, I freelanced as a developer, mostly writing custom scrapers for clients. The work paid fine, but every project was bespoke: build, deliver, get paid, never reuse the code. After a few of those, I started thinking: what if I shipped scrapers I could sell to many people instead of one client at a time?

There were two paths:

- **Build my own SaaS.** Billing, infrastructure, dashboards, auth, monitoring, marketing site. The hardest part is getting strangers to find me.
- **Publish on Apify.** Infrastructure, proxies, billing, scheduling, concurrency, run history, dataset storage, retries, all handled. Apify Store gives you distribution: when someone Googles “ziprecruiter scraper,” Apify's listing pages rank, and my Actor shows up. The trade-off is that Apify takes a cut, and I'm building on someone else's platform.

I'd rather have 75% of something that sells than 100% of something nobody finds. Six months in, I don't regret the choice.

## My first Actor (and everything I did wrong)

The Leboncoin scraper itself worked. What I got wrong was every product decision around it.

My README was a 1,500-word technical specification. I documented every input field, the retry logic, and the dataset schema. The opening sentence read: “ _Configurable Leboncoin scraper supporting pagination, filtering, and detail-page enrichment.”_

It got almost no traction. So I studied the top Actors on the Store, the ones with hundreds of users. Their READMEs looked nothing like mine. They opened with a single sentence stating the use case (“ _Extract rental listings from any French city for market research, lead generation, or price tracking”_), followed by three bullets of what you'd get, a sample JSON output, and a short filter list. Technical details lived at the bottom, almost as an appendix.

I rewrote my README. Use case first. Sample output second. Configuration last. Usage picked up over the following weeks.

**The lesson, in one sentence:** Your README is your sales page, not your reference manual. If a buyer can't tell _what data they'll get and what they'll do with it_ in the first ten seconds, they leave.

## How I decide what to build next

After the first few Actors started getting traction, I wanted to scale. But which sites?

My instinct was the obvious one: build for the biggest, most-searched platforms. LinkedIn, Indeed, Amazon, and Instagram. I learned quickly that's exactly where 90% of new Apify developers go. The Store has 5 to 15 competing Actors per major site, several of which are maintained by Apify itself. I'd be competing on price and polish with incumbents that have thousands of users.

So I changed my heuristic. I now evaluate every potential target against three signals.

**1\. Search demand without good supply.** Someone is searching Apify Store for \[site\] scraper and getting back nothing, or only a stale Actor with 1-star reviews. That's an opening.

**2\. High-value data, moderate scraping difficulty.** Job boards, B2B directories, lead-gen sources, and real estate. Worth real money to buyers; protected enough to filter out lazy competitors; not so locked-down that maintenance eats your margin.

**3\. Regional or vertical specialization.** Everyone builds for the global giants. Almost nobody builds for the European #1 in their category.

That last signal is what made my [Welcome to the Jungle Scraper](https://apify.com/silentflow/welcome-to-the-jungle-scraper) one of my top performers. WTJ is Europe's #1 job board, covers seven European markets, and is where developers and product people actually job-hunt in France, Germany, Spain, and the UK. Before I shipped it, there was no production-grade WTJ scraper on Apify Store. The pay-per-event (PPE) variant now has 60 users, more than my LinkedIn-targeted competitors expected for a “regional” board.

My biggest surprise was Skool, the online community / cohort-course platform. I almost didn't build it; I'd barely heard of it outside a few creator threads on Twitter. The PPE variant has 45 users and steady weekly runs. Recruiters, course operators, and competitive researchers all wanted that data; nobody else had built it.

**Heuristic:** Find underserved niches in markets you half-understand. Avoid the LinkedIn / Amazon / Instagram turf war.

## The pricing decision that changed everything

Every Actor I shipped in 2025 was available in two variants: a **standard** version priced by compute time, and a **PPE** version priced per result. Adding PPE was the single highest-leverage business decision I made on the Store.

Most of my buyers aren't engineers running pipelines. They're recruiters, small-agency operators, real estate investors, market researchers, or growth marketers. They don't think in “compute units” or “Actor seconds.” They think: “ _I need 200 leads from this city. How much will that cost me?”_

PPE makes the answer immediately scannable. “ _1,000 results for $2”_ is a yes. “ _$0.30 per compute unit on an estimated 45-second run with a 1.2× memory multiplier”_ makes people close the tab.

Here's what this looked like across my own catalog. Every Actor I built in both variants told the same story:

| Actor (same data, two variants) | Standard users | PPE users | Ratio |
| --- | --- | --- | --- |
| **Welcome to the Jungle** | 3 | **38** | 12.7× |
| **ZipRecruiter** | 2 | **25** | 12.5× |
| **Facebook Company** | 2 | **12** | 6.0× |
| **Jora (jobs)** | 2 | **6** | 3.0× |
| **Dealroom** | 3 | **8** | 2.7× |
| **Realtor Rental** | 3 | **7** | 2.3× |
| **Airbnb Search** | 3 | **6** | 2.0× |
| **Trulia Rental** | 3 | **5** | 1.7× |
| **Storeleads** | 17 | **29** | 1.7× |
| **eBay** | 8 | **13** | 1.6× |
| **Clutch** | 3 | **2** | 0.7× |

Eleven matched pairs, ten won by the PPE variant. The single PPE loser (Clutch) is the exception that proves the rule. Clutch's main buyers are agencies running large recurring scans, the one customer profile where compute-time pricing actually wins.

**Apify is sunsetting compute-time (standard) pricing in October 2026.** For me, this is the moment the data already pointed to. Every Actor I publish today is PPE-only. If you're starting in 2026, skip standard pricing entirely. You'll be ahead of where I had to be dragged.

## “How does one person maintain 98 Actors?”

This is the question I get asked most. The honest answer: I don't, in any meaningful sense. A canonical example does the heavy lifting.

The monorepo has a folder called `exemple-scrapper/` that contains a working PPE Actor plus four documents: `STRUCTURE.md`, `CONVENTIONS.md`, `CODE_GUIDELINES.md`, `README_GUIDE.md`. Every new Actor starts as a copy of that example, then I write only the site-specific bits: the parser, the input schema, and the field list on the `Item` struct.

There's no shared library that every Actor imports; each Actor is a standalone Go binary with its own `go.mod`. The leverage comes from **a template plus conventions I religiously stick to**, audited by `grep` across the monorepo whenever a pattern changes.

When a site changes selectors, only one Actor's parser changes. When I discover a new failure mode, I add a pattern to the example so the next 50 Actors I build will already have it.

The math: 98 Actors at 15 to 20 hours per week means each Actor gets about 10 minutes of attention per week on average. Most weeks, most Actors get zero. A few weeks per month, a single Actor consumes half my time because its target site shipped a major change. The template is what makes those numbers possible.

## What I actually spend my time on

Across 98 Actors, my 15 to 20 hours per week roughly break down as:

- **5 to 7 hours: Maintenance.** Selector updates, parser fixes, schema migrations when target sites change shape.
- **3 to 4 hours: Customer support.** Apify publishes my issue response time on my profile (6.2 hours), and buyers compare it.
- **2 to 3 hours: Monitoring & triage.** Reading run logs, investigating success-rate dips, and validating error-category alerts.
- **2 to 3 hours: New Actor development.** With the template mature, a brand-new Actor takes 4 to 8 hours of focused work end to end.
- **2 to 3 hours: SEO & metadata.** Title, description, README opening, category tags. I rewrite metadata more often than code.

Notice what's _not_ on this list: writing low-level scraping code. The template covers it.

## Under the hood: a few patterns worth sharing

This is the part of the article relevant to “production-grade”: the engineering choices that make a 98-Actor catalog with a 98.8% success rate possible. I'm keeping it deliberately surface-level on anything that touches a target site's defenses, because publishing a playbook there does nobody any good. What's below is the boring-but-essential plumbing.

### Language and transport

- **Go**, end to end. Each Actor is a single static binary built in a multi-stage Dockerfile.
- **HTTP-only.** No headless browser anywhere in the stack.

The trade-off is real. HTTP-only scrapers cost roughly an order of magnitude less compute, start faster, and break less often, at the price of more reverse-engineering up front. Cheaper compute pays off twice. My Actors are cheap to run per result, which lets me set PPE prices competitively while preserving margin.

### Per-Actor file structure

Every Actor follows the same shape:

```
sitename-apify-ppe/
├── .actor/
│   ├── actor.json
│   ├── INPUT_SCHEMA.json
│   └── dataset_schema.json
├── Dockerfile
├── go.mod / go.sum
├── main.go                 # Input + ScrapingStats + main() flow
├── README.md
└── sitename/               # The only site-specific Go package
    ├── client.go           # HTTP client, retry, headers
    ├── models.go           # Item struct + JSON tags
    └── parser.go           # HTML/JSON parsing → Item
```

To add a new Actor: copy the example, rename the package, write `parser.go`, write the `Item` struct, fill `INPUT_SCHEMA.json`, test locally, push.

### Categorized error counters

Every Actor's `main.go` carries the same `ScrapingStats` struct and `categorizeError()` function, copy-pasted from the template:

```go
type ScrapingStats struct {
    TotalRequests   int
    SuccessfulPages int
    FailedPages     int
    ProxyErrors     int
    RateLimitErrors int
    BlockedErrors   int
    NetworkErrors   int
    OtherErrors     int
    StartTime       time.Time
}

func categorizeError(err error, stats *ScrapingStats) {
    if err == nil { return }
    s := strings.ToLower(err.Error())
    switch {
    case strings.Contains(s, "proxy") || strings.Contains(s, "tunnel") || strings.Contains(s, "403 forbidden"):
        stats.ProxyErrors++
    case strings.Contains(s, "rate limit") || strings.Contains(s, "429") || strings.Contains(s, "too many"):
        stats.RateLimitErrors++
    case strings.Contains(s, "blocked") || strings.Contains(s, "captcha") || strings.Contains(s, "challenge"):
        stats.BlockedErrors++
    case strings.Contains(s, "timeout") || strings.Contains(s, "connection") || strings.Contains(s, "network"):
        stats.NetworkErrors++
    default:
        stats.OtherErrors++
    }
}
```

Go

Copy

This is deliberately crude: no error wrapping, no `errors.As()`, no custom types. The advantage is that any error from anywhere in the call chain automatically lands in the right bucket as long as the message is descriptive. The 98.8% success rate on my profile is computed directly from these counters, and when one Actor misbehaves in production, I can see at a glance which bucket lit up.

### Retry policy, by status code

The HTTP client retries with backoff, but the action depends on the status code:

| Status | Action |
| --- | --- |
| 200, body looks legitimate | Success, return body |
| 200, body looks like a challenge page | Retry |
| 403 | Retry |
| 404 | Immediate error, no retry |
| 429 | Retry with longer sleep |
| 5xx | Retry with standard backoff |
| Other 4xx | Immediate error, no retry |

Default `maxRetries` is 5. Backoff is randomized between attempts. The single most useful row in this table is the second one: a 200 response with a challenge page in the body is the kind of failure that poisons a dataset for a week before anyone notices.

### Silent-failure detection

The hardest production failure isn't an Actor that crashes. It's an Actor that returns HTTP 200 with content that looks like data but isn't. The success metric stays green; the data is junk.

Every Actor runs a body-level sanity check on every successful fetch. The principle is simple: if the response is structurally suspicious (wrong size, wrong shape, or not matching the patterns the parser expects), it is treated as a failed fetch, not a success, and the run logs the appropriate error category.

This single layer is responsible for keeping more reviews from going 1-star than anything else in the codebase.

### The brotli incident

A few weeks into shipping Actors, I started seeing intermittent corruption in roughly 1% of fetches: a parse error, then a successful retry on the same URL. Mildly annoying, not breaking anything.

Then one Actor's success rate dropped to 60% over two days. The HTTP requests succeeded. The retries succeeded. The bodies were unreadable.

The bug: when using Go's `net/http` with `Accept-Encoding: gzip, deflate, br`, Apify Proxy occasionally corrupts brotli-encoded responses (`EXUBERANT_NIBBLE` decoding errors). The proxy and the brotli encoder simply don't get along through `net/http`.

The fix was a one-line change in the template: drop `br` from `Accept-Encoding`. After it propagated, that whole class of bugs disappeared. I'd never have caught this without the categorized error counters showing a sustained OtherErrors spike on one Actor.

### The `rand.Seed()` that did nothing in 78 files

For roughly the first three months, every Actor had a copy of `rand.Seed(time.Now().UnixNano())` at the top of `main()`. I'd carried it over from a Go 1.19 project. In Go 1.20+, the global `rand` source is auto-seeded, so that call is a documented no-op.

When I went to remove it, I found I'd duplicated it across 78 files. Harmless, but a vivid reminder that the cost of conventions you don't audit is conventions that accumulate silently. I now run a quarterly sweep of the monorepo with `grep` against the template to catch this kind of drift.

## The 1-star review that taught me to slow down

Early on, I optimized for shipping fast: more Actors equals more revenue surface area, right? I once pushed an Actor live without testing it on Apify's infrastructure. It worked on my laptop, but failed in production due to a silent, empty-output bug. A buyer ran it, got nothing, and left a 1-star review.

The review sat on the Actor page for days. Every potential buyer saw it. New runs collapsed.

I fixed the bug, replied to the buyer, and the review was eventually updated, but the lost weeks of usage didn't come back. On a marketplace, reputation compounds in both directions. One bad review can break the cycle.

Since then, every new Actor goes through a 48-hour staging period on Apify's own infrastructure (synthetic inputs first, then real ones) before the public flag flips. Slower to ship. Far fewer disasters.

## What actually works on Apify Store

**What works:**

- Underserved sites in regional or vertical niches (WTJ, Skool, Jora)
- READMEs that lead with use cases and sample output, not configuration
- **PPE-only pricing.** Apify is sunsetting standard pricing in October 2026
- Same-day response on issues, under 12 hours earns repeat buyers; under 6 hours is a moat
- A canonical example folder + strict conventions that every new Actor copies
- HTTP-only stacks where the target allows it
- A body-level silent-failure check on every successful fetch
- Categorized error counters so production weirdness is visible

**What doesn't work:**

- Going head-to-head with established LinkedIn / Amazon / Instagram scrapers
- Technical READMEs that read like API documentation
- Rushing a public release without testing on Apify infrastructure
- Building for sites that change layout monthly, unless the data is worth it
- Generic “try 3 times and give up” retry policies. Categorize by status code
- Quantity without operational discipline. Three reliable Actors out-earn ten unmaintained ones

## Honest numbers (the ones I can share)

I'm not going to post revenue here. At six months in, the absolute figure doesn't teach much that generalizes across people, niches, and pricing strategies. What does generalize is the shape of the curve:

- **Months 1 to 2 (Nov to Dec 2025):** First Actors shipped. Single-digit weekly runs. Most of my time went into figuring out Apify's input schema, dataset format, and pricing surface.
- **Months 3 to 4 (Jan to Feb 2026):** First Actors with double-digit user counts. PPE variants started visibly outperforming standards. Revenue became meaningful but inconsistent.
- **Months 5 to 6 (Mar to Apr 2026):** Catalog effect kicked in hard. Cross-discovery (buyers of one Actor finding others in my profile) became a real channel. Issue volume scaled with usage, forcing the maintenance industrialization that the template enables.

The biggest surprise, and the one I want every new Store developer to internalize: **my top-performing Actors are not the ones I expected.** I bet on real estate, the domain I knew from freelance work. The actual wins came from Welcome to the Jungle, Skool, Storeleads, ZipRecruiter, and Airbnb professional-host enrichment. The niche bets returned more than the obvious ones.

## If you're starting on Apify today

1. **Pick one niche you half-understand.** Don't try to do everything. Find an underserved site in a domain you already follow.
2. **Build a canonical example Actor before #5, and write the conventions that go with it.** Every new Actor in your catalog starts as a copy of that example.
3. **Ship PPE-only.** Apify is sunsetting compute-time pricing in October 2026. The data was telling you to do this anyway.
4. **Write the README as a sales page.** Use case first, sample output second, configuration last.
5. **Pick a stack that minimizes compute cost.** HTTP-only over headless where the target allows.
6. **Categorize your errors at the metrics layer.** When a site goes weird in production, you'll see exactly which bucket lit up.
7. **Stage every release on Apify, not just locally.** Working on your laptop is not the same as working in production.
8. **Track your issue response time.** Apify publishes it on your profile. Under 12 hours earns repeat buyers; under 6 hours is a moat.

Building on Apify Store isn't passive income. It's a real product business with a maintenance backlog, customer support, monitoring obligations, and the occasional 2 am wake-up when a target site ships a redesign. But it's the most leveraged thing I've done as a developer: a catalog of products that work while I sleep, sitting on top of an infrastructure stack I didn't have to build, in a marketplace I didn't have to bootstrap.

If you've ever built a scraper that solved a real problem for someone, it's probably worth putting on the Store. Someone is searching for exactly that.

![Apify logo](https://apify.com/ext/logomark-32x32.svg)

Largest marketplace of tools for AI

Thousands of Actors to automate your business. Get real-time web data, track competitors, generate leads, monitor social media, and integrate your apps and agents.

[Browse the marketplace](https://apify.com/store) [Publish an Actor](https://docs.apify.com/platform/actors/publishing)

[![Olivier Reynaud](https://storage.ghost.io/c/f2/6e/f26ec999-9a90-4aee-a0d4-9b3ca2bb668f/content/images/2026/07/Image-from-iOS-1.jpg)\\
\\
Olivier Reynaud\\
\\
\\
Olivier Reynaud is an independent developer who builds and maintains web scraping Actors on Apify Store, all written in Go. He studies software engineering at EPITECH and entrepreneurship at ESCP.](https://blog.apify.com/author/olivier/)

On this page


01. [Why Apify (and not building my own SaaS)](https://blog.apify.com/building-98-actors-on-apify-store/#why-apify-and-not-building-my-own-saas)
02. [My first Actor (and everything I did wrong)](https://blog.apify.com/building-98-actors-on-apify-store/#my-first-actor-and-everything-i-did-wrong)
03. [How I decide what to build next](https://blog.apify.com/building-98-actors-on-apify-store/#how-i-decide-what-to-build-next)
04. [The pricing decision that changed everything](https://blog.apify.com/building-98-actors-on-apify-store/#the-pricing-decision-that-changed-everything)
05. [“How does one person maintain 98 Actors?”](https://blog.apify.com/building-98-actors-on-apify-store/#%E2%80%9Chow-does-one-person-maintain-98-actors%E2%80%9D)
06. [What I actually spend my time on](https://blog.apify.com/building-98-actors-on-apify-store/#what-i-actually-spend-my-time-on)
07. [Under the hood: a few patterns worth sharing](https://blog.apify.com/building-98-actors-on-apify-store/#under-the-hood-a-few-patterns-worth-sharing)
    1. [Language and transport](https://blog.apify.com/building-98-actors-on-apify-store/#language-and-transport)
    2. [Per-Actor file structure](https://blog.apify.com/building-98-actors-on-apify-store/#per-actor-file-structure)
    3. [Categorized error counters](https://blog.apify.com/building-98-actors-on-apify-store/#categorized-error-counters)
    4. [Retry policy, by status code](https://blog.apify.com/building-98-actors-on-apify-store/#retry-policy-by-status-code)
    5. [Silent-failure detection](https://blog.apify.com/building-98-actors-on-apify-store/#silent-failure-detection)
    6. [The brotli incident](https://blog.apify.com/building-98-actors-on-apify-store/#the-brotli-incident)
    7. [The rand.Seed() that did nothing in 78 files](https://blog.apify.com/building-98-actors-on-apify-store/#the-randseed-that-did-nothing-in-78-files)
08. [The 1-star review that taught me to slow down](https://blog.apify.com/building-98-actors-on-apify-store/#the-1-star-review-that-taught-me-to-slow-down)
09. [What actually works on Apify Store](https://blog.apify.com/building-98-actors-on-apify-store/#what-actually-works-on-apify-store)
10. [Honest numbers (the ones I can share)](https://blog.apify.com/building-98-actors-on-apify-store/#honest-numbers-the-ones-i-can-share)
11. [If you're starting on Apify today](https://blog.apify.com/building-98-actors-on-apify-store/#if-youre-starting-on-apify-today)

Share this article:
Copied!

Don't build it. Find it.

Thousands of ready-to-run tools for AI.

[Browse Apify Store](https://apify.com/store)

### Related articles

[![Ranking Google Trends data with Claude](https://storage.ghost.io/c/f2/6e/f26ec999-9a90-4aee-a0d4-9b3ca2bb668f/content/images/size/w1200/2026/10/ranking-google-trends-data-with-claude--1-.png)](https://blog.apify.com/google-trends-compare-keywords/)

[Developer community](https://blog.apify.com/tag/developer-community/)

[AI](https://blog.apify.com/tag/ai/)

[MCP](https://blog.apify.com/tag/mcp/)

[Claude refused to rank my Google Trends data. Then it invented the ranking anyway](https://blog.apify.com/google-trends-compare-keywords/)

[![George Kioko](https://storage.ghost.io/c/f2/6e/f26ec999-9a90-4aee-a0d4-9b3ca2bb668f/content/images/size/w150/2026/10/01-1.jpg)\\
\\
George Kioko](https://blog.apify.com/author/george-kioko/)

Oct 1, 2026

[![I gave my Reddit Actor to an AI agent, and it made every mistake I made](https://storage.ghost.io/c/f2/6e/f26ec999-9a90-4aee-a0d4-9b3ca2bb668f/content/images/size/w1200/2026/09/i-gave-my-reddit-actor-to-an-ai-agent.png)](https://blog.apify.com/reddit-actor-ai-agent-input-schema/)

[Developer community](https://blog.apify.com/tag/developer-community/)

[MCP](https://blog.apify.com/tag/mcp/)

[AI agents](https://blog.apify.com/tag/ai-agents/)

[I gave my Reddit Actor to an AI agent, and it made all the same mistakes I did](https://blog.apify.com/reddit-actor-ai-agent-input-schema/)

[![Mick “labrat” Donahue](https://storage.ghost.io/c/f2/6e/f26ec999-9a90-4aee-a0d4-9b3ca2bb668f/content/images/size/w150/2026/09/MickDonahue.webp)\\
\\
Mick “labrat” Donahue](https://blog.apify.com/author/mick/)

Sep 30, 2026

[![What the Apify MCP server does to your Actor before an AI agent ever sees it](https://storage.ghost.io/c/f2/6e/f26ec999-9a90-4aee-a0d4-9b3ca2bb668f/content/images/size/w1200/2026/09/i-audited-151-actors-for-ai-agents.png)](https://blog.apify.com/fixing-actors-invisible-to-agents/)

[Developer community](https://blog.apify.com/tag/developer-community/)

[MCP](https://blog.apify.com/tag/mcp/)

[AI agents](https://blog.apify.com/tag/ai-agents/)

[What the Apify MCP server does to your Actor before an AI agent ever sees it](https://blog.apify.com/fixing-actors-invisible-to-agents/)

[![Olivier Reynaud](https://storage.ghost.io/c/f2/6e/f26ec999-9a90-4aee-a0d4-9b3ca2bb668f/content/images/size/w150/2026/07/Image-from-iOS-1.jpg)\\
\\
Olivier Reynaud](https://blog.apify.com/author/olivier/)

Sep 24, 2026
