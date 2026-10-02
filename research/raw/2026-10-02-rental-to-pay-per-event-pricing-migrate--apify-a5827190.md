---
url: https://blog.apify.com/migrating-to-pay-per-event-pricing/
retrieved: 2026-10-02
command: firecrawl scrape https://blog.apify.com/migrating-to-pay-per-event-pricing/ --only-main-content --json
statusCode: 200
transport: firecrawl-cli
completeness: full
title: Rental to pay-per-event pricing: migrate your Actor
---
[If you haven’t moved your Actor to pay-per-event (PPE) yet](https://blog.apify.com/standardizing-actor-pricing/), this is a practical rental to PPE migration guide that presents what you need to do to change your Actor pricing ahead of the deadline.

## Prerequisites

Before you start, have these ready:

- An Actor currently on rental pricing in [Apify Store](https://apify.com/store)
- Access to your Actor's Publication tab in Apify Console
- The usage data export from the [data pipeline Actor](https://console.apify.com/actors/yp0UJXslEFoM2uYEY/info/readme?build=latest)
- The [rental to pay-per-event calculator](https://rental-to-pay-per-event-calculator.apify.tools/)
- 20 to 30 minutes of quiet time, since setting new prices is not something to rush

## Why the rental to PPE migration matters now

[Rental pricing has been on its way out](https://blog.apify.com/agent-pricing-models/) since March 31, 2026, when Apify stopped accepting price changes or new rental listings. September 30, 2026 is the hard deadline. After that date, your Actor automatically switches to pay-per-usage (PPU, also known as “free”), meaning you collect zero revenue from it going forward.

[This blog post from April](https://blog.apify.com/standardizing-actor-pricing/) explains how the decision was made. Developers who've already migrated are seeing what the post predicted: usage and revenue both up, even for niche Actors.

## PPE overview

Under PPE, you set a price for a specific event that your Actor's code triggers, and the user pays only for that event. You cover the platform cost of producing it. That's the opposite of rental, where you earned a flat fee regardless of how much a user actually ran your Actor. Full details live in [Apify's pay-per-event documentation](https://docs.apify.com/platform/actors/publishing/monetize/pay-per-event). Here are the things to consider:

### Using synthetic events to simplify migration

Apify offers two synthetic events that require zero code changes. Using both of these will simplify your migration process:

- `apify-actor-start` charges per gigabyte of RAM when your Actor starts. Set this up, and Apify automatically covers the first 5 seconds of compute on every run. It's worth adding to every Actor, ideally at the default RAM volume, because it also cushions you against empty runs that fail on input validation.
- `apify-default-dataset-item` charges per item your Actor pushes to the default dataset. Pricing varies a lot by Actor, but this is the simplest migration step for anyone running a result-based scraper.

Set up those two events, and you have a working baseline. If you want to set up more complex pricing, you can create completely custom events within your code. For more info about pricing Actors, and creating custom events, check out this webinar replay:

Creator webinar: Actor pricing 101 - YouTube

Tap to unmute

[Creator webinar: Actor pricing 101](https://www.youtube.com/watch?v=zkF_RI8TE3A) [Apify](https://www.youtube.com/channel/UCTgwcoeGGKmZ3zzCXN2qo_A)

Apify29.6K subscribers

[Watch on](https://www.youtube.com/watch?v=zkF_RI8TE3A)

### Price by plan tier, not by user

Rental gave every subscriber the same flat fee regardless of the plan they're on. PPE lets you set a different price per Apify plan tier, and we encourage you to do this.

Bronze users on the Starter plan run smaller, less frequent jobs. Gold users on Business and above run at scale, and their platform cost per result is lower. Charge everyone the same rate, and you either lose your biggest users to the price or leave money on the table with smaller ones. A reasonable starting point is to price Silver about 10% below Bronze, and Gold about 20% below Bronze.

### Free users

Don't forget to price free-tier users too. You're not paying platform cost for them; they're your acquisition funnel, and pricing them too aggressively cuts off new signups before they ever convert. And if you're tempted to pass platform costs straight to users through the additional options toggle, know that it hurts conversion and lowers your Actor's quality score. It's intended as a short-term tool while you gather pricing data, not a permanent setup.

### Primary event

Pick one event as your primary event, the one that scales most with bigger runs and best communicates your Actor's value to someone who has never used it. For most scrapers, that is the result count. This is the number displayed as the price on your Actor's Store page, so choose the event that most closely reflects the true cost of running Actor for its stated purpose.

## Using the migration calculator to set your new prices

This is the [tool built specifically for this migration](https://rental-to-pay-per-event-calculator.apify.tools/), helping you to balance your pricing with your customers’ usage. Take the JSON export from the data pipeline Actor, paste it into the calculator, and it turns your own usage history into a pricing recommendation instead of a guess.

### What the cost breakdown tells you

Open "show cost breakdown" and you get results, runs, platform cost, and cost per 1k results, broken down by tier. Gold-tier users typically produce the most results at the lowest cost per 1k, because they are running bigger jobs. Small runs cost more per result due to startup overhead, which is exactly why the actor-start event (or a placeholder no-result item) matters: runs that finish empty still cost you money.

In the example data shown in [this webinar](https://www.youtube.com/watch?v=wqnBUPwwK2w) on the topic, 72% of runs were "light," under 100 results, but produced only 15% of total results. The 6% of runs classified as "heavy" produced 47% of all results. That gap is the whole argument for tiered pricing in one chart.

### Reading the cost floor, competitive range, and break-even price

The main graph has three moving parts. The cost floor, in red, is the minimum price per 1k results that covers your platform cost, based on your actual data, including empty and short runs. The competitive range, in green, shows where most Store Actors currently price. The break-even price is where your PPE earnings would exactly match your current rental profit from active users, calculated from last month's tier-by-tier usage.

Note that there's more than one combination of tier prices that hits break-even. You can nudge one tier up and another down, and the calculator lets you play with that instead of forcing one answer. You can adjust the sliders or full amounts, as well as add or remove actor-start.

We recommend you set your event pricing slightly higher than the break-even number shown in the calculator: lowering a price later is instant, but raising one needs 14 days' notice and can only happen once a month - your users will notice that increase more than they will notice a small overcharge now.

### Checking who it actually affects

Scroll down to the user impact analysis table, and you see, run by run, what your current subscribers would pay under your new PPE setup compared to what they pay now. No names, fully anonymized, but enough detail to spot the pattern. Most users pay about the same or less.

A handful of outliers, usually your heaviest users who got a great deal under flat rental pricing, will see a real increase. Click on the Override button next to each user to calibrate custom pricing that protects that customer’s costs and your relationship with them. Apify’s Support team acts on your instructions to set those specific users up with a temporary price override while you both adjust.

## Points worth noting

The calculator excludes subscribers who never canceled but also never ran the Actor last month. That undercounts your churn risk slightly, but including them would push suggested prices higher for everyone still actively using the Actor, so the exclusion is intentional.

If your Actor is not result-based, or it writes to a custom dataset or key-value store instead of the default dataset, the calculator still gives you useful numbers, but it will not give you the full picture.

Creating an override for a user will change the graphs showing projected earnings, so check back as you make changes to confirm that the Actor’s general pricing still protects your revenue.

## If you already have two Actors, one rental and one pay-per-event

When PPE was launched, some of you built a separate Actor from scratch rather than converting your existing rental Actor. That leaves you with two live listings: the old rental Actor with its established subscriber base, and a newer PPE Actor still building its own.

Our advice is to keep both, for now. You have SEO presence for both of them, so they will both continue to draw new customers as well as retain your existing ones.

### Migrate the rental Actor first, worry about consolidation later

Migrate your rental Actor to PPE using everything above. You’ll end up with two PPE Actors rather than one rental and one PPE Actor. That’s fine. Each keeps its own reviews, run history, and Store ranking, and neither loses momentum while you figure out what a merged version should look like. Trying to force a consolidation before September 30 just adds risk to a deadline that is already tight enough.

### Give each Actor a reason to stay separate, or a reason to merge

Once both Actors are on PPE, you have room to think about whether they should stay two products or become one. A natural way to build toward a merge is to add a feature to one Actor that the other doesn't have, and price it as its own event. An LLM-based step that validates or enriches the scraped data is a common example. That gives you a real basis for comparison once both Actors carry a season of PPE data. If usage tells you they should be one Actor, you'll have a much clearer picture of which features to keep than if you had merged them on day one.

### Cross-sell in the meantime

Until you decide, use each Actor's README to point at the other. If someone lands on your rental-turned-PPE Actor looking for a feature that only lives in the newer one, or the other way round, say so directly and link to it. That keeps both Actors visible to relevant users, keeps the SEO juice flowing, and it costs nothing to set up.

Although we're strict about duplicate Actors in Apify Store, we’ll be making exceptions if one of the duplicate Actors was previously published with rental pricing.

## Wrapping up

Rental pricing sunsets October 1, 2026, and anything you haven’t migrated by then moves to pay-per-usage with zero revenue for you. Start with the two synthetic events, apify-actor-start and apify-default-dataset-item, run your usage data through the calculator, and set tier prices slightly above your break-even point.

If your export or setup gets confusing, use the feedback button inside the calculator or drop a message in the community's [#project-rentals Discord channel](https://discord.gg/QfDmA7RGFu).

## FAQ

**Do I need to migrate my Actor 14 days before September 30?**

No. If you have future pricing configured before September, your Actor won't auto-migrate to pay-per-usage. It switches to your new pay-per-event pricing 14 days after that date instead.

**Can I avoid the 14-day notice period for a rental Actor with zero paying users?**

Yes, if there are no users subscribed to your Actor, then you can make pricing changes with immediate effect.

**Is there a best day of the month to migrate to minimize chargebacks?**

Based on current data, migrations and chargebacks are distributed fairly evenly across the month. If you’re concerned about a specific Actor or a group of Actors, ask the developer relations team to take a look at your data specifically.

**What if my Actor does not push results to the default dataset?**

The calculator will still return useful numbers, but not a complete picture, since it's built primarily for result-based Actors. Reach out to [community@apify.com](mailto:community@apify.com) for more tailored support from the developer relations team.

**Where do I get the usage data the calculator needs?**

Run the [data pipeline Actor](https://console.apify.com/actors/yp0UJXslEFoM2uYEY/info/readme?build=latest). It outputs a JSON export fully anonymized on the user impact side, and ready to submit directly into the calculator.

**If I have both a rental and PPE Actor already doing the same thing, can I merge the two?**

We don’t recommend doing this as the benefits of keeping up both Actors outweigh the benefits of merging in the short term. We’ll be allowing duplicate Actors under your account if you have historically migrated one of them from rental pricing.

[![Ella de Jonge](https://storage.ghost.io/c/f2/6e/f26ec999-9a90-4aee-a0d4-9b3ca2bb668f/content/images/2026/08/headshot-91-1-1-1.jpg)\\
\\
Ella de Jonge\\
\\
\\
Senior Developer Community Manager at Apify. Find me in Apify's Discord and subreddit.](https://blog.apify.com/author/ella/)

On this page


1. [Prerequisites](https://blog.apify.com/migrating-to-pay-per-event-pricing/#prerequisites)
2. [Why the rental to PPE migration matters now](https://blog.apify.com/migrating-to-pay-per-event-pricing/#why-the-rental-to-ppe-migration-matters-now)
3. [PPE overview](https://blog.apify.com/migrating-to-pay-per-event-pricing/#ppe-overview)
1. [Using synthetic events to simplify migration](https://blog.apify.com/migrating-to-pay-per-event-pricing/#using-synthetic-events-to-simplify-migration)
2. [Price by plan tier, not by user](https://blog.apify.com/migrating-to-pay-per-event-pricing/#price-by-plan-tier-not-by-user)
3. [Free users](https://blog.apify.com/migrating-to-pay-per-event-pricing/#free-users)
4. [Primary event](https://blog.apify.com/migrating-to-pay-per-event-pricing/#primary-event)
4. [Using the migration calculator to set your new prices](https://blog.apify.com/migrating-to-pay-per-event-pricing/#using-the-migration-calculator-to-set-your-new-prices)
1. [What the cost breakdown tells you](https://blog.apify.com/migrating-to-pay-per-event-pricing/#what-the-cost-breakdown-tells-you)
2. [Reading the cost floor, competitive range, and break-even price](https://blog.apify.com/migrating-to-pay-per-event-pricing/#reading-the-cost-floor-competitive-range-and-break-even-price)
3. [Checking who it actually affects](https://blog.apify.com/migrating-to-pay-per-event-pricing/#checking-who-it-actually-affects)
5. [Points worth noting](https://blog.apify.com/migrating-to-pay-per-event-pricing/#points-worth-noting)
6. [If you already have two Actors, one rental and one pay-per-event](https://blog.apify.com/migrating-to-pay-per-event-pricing/#if-you-already-have-two-actors-one-rental-and-one-pay-per-event)
1. [Migrate the rental Actor first, worry about consolidation later](https://blog.apify.com/migrating-to-pay-per-event-pricing/#migrate-the-rental-actor-first-worry-about-consolidation-later)
2. [Give each Actor a reason to stay separate, or a reason to merge](https://blog.apify.com/migrating-to-pay-per-event-pricing/#give-each-actor-a-reason-to-stay-separate-or-a-reason-to-merge)
3. [Cross-sell in the meantime](https://blog.apify.com/migrating-to-pay-per-event-pricing/#cross-sell-in-the-meantime)
7. [Wrapping up](https://blog.apify.com/migrating-to-pay-per-event-pricing/#wrapping-up)
8. [FAQ](https://blog.apify.com/migrating-to-pay-per-event-pricing/#faq)

Share this article:
Copied!

Publish and earn on Apify Store

The largest marketplace of tools for AI

[Start here](https://apify.com/partners/actor-developers)

### Related articles

[![Create an Actor with a Git repo in a few clicks](https://storage.ghost.io/c/f2/6e/f26ec999-9a90-4aee-a0d4-9b3ca2bb668f/content/images/size/w1200/2026/09/Actor-with-a-git-repo-blog-updated.png)](https://blog.apify.com/create-an-actor-with-a-git-repo/)

[Apify updates](https://blog.apify.com/tag/apify-updates/)

[Developer community](https://blog.apify.com/tag/developer-community/)

[Create an Actor with a Git repo in a few clicks](https://blog.apify.com/create-an-actor-with-a-git-repo/)

[![Patrik Braborec](https://storage.ghost.io/c/f2/6e/f26ec999-9a90-4aee-a0d4-9b3ca2bb668f/content/images/size/w150/2025/08/1733321693558.jpeg)\\
\\
Patrik Braborec](https://blog.apify.com/author/patrik/)

Sep 3, 2026

[![Migrating the Apify MCP Server to the new stateless spec](https://storage.ghost.io/c/f2/6e/f26ec999-9a90-4aee-a0d4-9b3ca2bb668f/content/images/size/w1200/2026/08/MPC_blog-cover.png)](https://blog.apify.com/mcp-stateless-migration/)

[AI agents](https://blog.apify.com/tag/ai-agents/)

[Apify updates](https://blog.apify.com/tag/apify-updates/)

[MCP](https://blog.apify.com/tag/mcp/)

[Migrating the Apify MCP Server to the new stateless spec](https://blog.apify.com/mcp-stateless-migration/)

[![Lukas Bekr](https://storage.ghost.io/c/f2/6e/f26ec999-9a90-4aee-a0d4-9b3ca2bb668f/content/images/size/w150/2025/12/322734882_1467698230305967_3359969301068252144_n.jpg)\\
\\
Lukas Bekr](https://blog.apify.com/author/lukas-bekr/)

Aug 18, 2026

[![Meet Apify AI: describe a task, get the data](https://storage.ghost.io/c/f2/6e/f26ec999-9a90-4aee-a0d4-9b3ca2bb668f/content/images/size/w1200/2026/07/Apify-AI-launch.png)](https://blog.apify.com/introducing-apify-ai/)

[AI](https://blog.apify.com/tag/ai/)

[Apify updates](https://blog.apify.com/tag/apify-updates/)

[Thought leadership](https://blog.apify.com/tag/thought-leadership/)

[Meet Apify AI: describe a task, get the data](https://blog.apify.com/introducing-apify-ai/)

[![Marek Mouček](https://storage.ghost.io/c/f2/6e/f26ec999-9a90-4aee-a0d4-9b3ca2bb668f/content/images/size/w150/2026/07/Sni--mek-obrazovky-2026-07-16-v--11.55.47.png)\\
\\
Marek Mouček](https://blog.apify.com/author/marek/)

Jul 21, 2026
