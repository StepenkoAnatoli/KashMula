---
url: https://apify.com/change-log/pay-for-apify-actors-with-x402
retrieved: 2026-10-02
command: firecrawl scrape https://apify.com/change-log/pay-for-apify-actors-with-x402 --only-main-content --json
statusCode: 200
transport: firecrawl-cli
completeness: partial
omitted: only 1481 characters of main content were returned (below the 1500-character bar)
title: Pay for Apify Actors with x402 · Change log · Apify
---
[Back to all change logs](https://apify.com/change-log)

Jun 26, 2026

# Pay for Apify Actors with x402

New

Actor

API

![Pay for Apify Actors with x402](https://images.apifyusercontent.com/DXH2n0xIm5rAC9B15VK4siBHG0RMH3DcSYeNKP4c14Q/w:1800/cb:1/aHR0cHM6Ly9jZG4tY21zLmFwaWZ5LmNvbS9hZ2VudGljX3BheW1lbnRzXzNfMV9hMTY2NWY5ZTg1LnBuZw.webp)
AI agents can now run and pay for eligible Apify Actors in USDC on the [Base](https://www.base.org/) network. No Apify account, billing, or API key required. Payments use the open [x402 protocol](https://www.x402.org/) and settle at the time of request, over both Apify MCP server and the Apify API.

The fastest and easiest way is to use [Coinbase Agentic Wallet CLI](https://docs.cdp.coinbase.com/agentic-wallet/welcome):

```
npx awal
npx skills add coinbase/agentic-wallet-skills
```

To get started, give this skill to your agent: [apify.it/x402-awal](https://apify.com/change-log/apify.it/x402-awal).

If you're building Actors, you can review the [eligibility criteria](https://docs.apify.com/platform/actors/publishing/monetize#make-your-actor-eligible-for-agentic-payments) to make sure yours can accept agentic payments. For more information, see [the docs](https://docs.apify.com/platform/integrations/x402) and [blog post](https://blog.apify.com/p/6702de5c-8bb2-46be-b591-edc1ebf52706/).

![](https://apify.com/_next/image?url=https%3A%2F%2Fcdn-cms.apify.com%2Froman_rostar_7613ea12d3.png&w=3840&q=75)

Roman Roštár

Product Manager
