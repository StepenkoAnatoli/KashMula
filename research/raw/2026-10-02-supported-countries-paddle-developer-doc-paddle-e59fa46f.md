---
url: https://developer.paddle.com/concepts/sell/supported-countries-locales
retrieved: 2026-10-02
command: firecrawl scrape https://developer.paddle.com/concepts/sell/supported-countries-locales --only-main-content --json
statusCode: 200
transport: firecrawl-cli
completeness: full
title: Supported countries | Paddle Developer Docs
---
For AI agents and LLMs: a structured documentation index is available at [/llms.txt](https://developer.paddle.com/llms.txt). Every page has a Markdown sibling — append `.md` to any URL.

 [Skip to content](https://developer.paddle.com/concepts/sell/supported-countries-locales/#main)

Copy for LLMCopy

# Supported countries

Go global and sell in over 200 countries and territories, fully tax compliant, with no extra engineering effort.

AI summary

Paddle supports selling in over 200 countries and territories with no additional setup — it automatically calculates taxes, handles compliance, and blocks transactions from sanctioned countries.

- •Paddle only asks customers for their country and ZIP/postal code (where required for tax or compliance) — a full address is never required at checkout, reducing friction.
- •As merchant of record, Paddle calculates, collects, and remits taxes for all supported countries — you have zero sales tax liability for any Paddle transaction.
- •Transactions from countries under international sanctions or that violate platform policies are automatically blocked by Paddle — no action required on your part.

Which countries can I sell in with Paddle?Do I need to register for VAT or sales tax in the countries I sell to?What happens if a customer from a blocked country tries to check out?

With Paddle, you can unlock new revenue by selling in over 200 countries and territories across the world — no additional setup needed.

Paddle automatically calculates taxes and handles sales tax liability for all countries and currencies.

Sell in over 200 markets

Expand into popular and emerging markets, while minimizing your risk.

Global tax compliance

As a merchant of record, Paddle calculates, collects, and remits taxes for you.

No extra engineering effort

All supported countries are ready-to-use as part of the Paddle API and Paddle.js.

## How it works [Copy link to this section](https://developer.paddle.com/concepts/sell/supported-countries-locales/\#how-it-works)

### Localize prices [Copy link to this section](https://developer.paddle.com/concepts/sell/supported-countries-locales/\#localize-prices)

One size doesn't fit all when it comes to currencies. Paddle lets you [set country-specific prices](https://developer.paddle.com/build/products/offer-localized-pricing), rather than pricing for currencies that might apply across markets.

You can also automatically convert prices into local currencies at checkout, making customers more likely to purchase.

### Optimized checkout [Copy link to this section](https://developer.paddle.com/concepts/sell/supported-countries-locales/\#optimized-checkout)

To make buying as frictionless as possible, [Paddle Checkout](https://developer.paddle.com/concepts/sell/self-serve-checkout) doesn't require a full address, only asking customers for their country and (in some countries) their ZIP/postal code or region.

Region information and ZIP/postal codes are only required in some countries for tax calculation, fraud prevention, and banking compliance purposes. Checkout only asks for this in countries where required.

### Unsupported countries are blocked [Copy link to this section](https://developer.paddle.com/concepts/sell/supported-countries-locales/\#unsupported-countries-are-blocked)

Payments from some countries are blocked in compliance with international sanctions regulations, payments platforms policies, and anti-money laundering regulations.

Paddle automatically blocks transactions from unsupported countries. You don't need to do anything.

Supported countries work with no additional setup required.

## List of supported countries [Copy link to this section](https://developer.paddle.com/concepts/sell/supported-countries-locales/\#list-of-supported-countries)

You can also get this list programmatically. GET [`/countries`](https://developer.paddle.com/api-reference/countries/list-countries) returns every country that Paddle knows about, including the currency used for automatic price conversion and whether Paddle supports sales there.

Supported countriesDownload

| ISO | Country | Currency | Tax preference | Postal code? |
| --- | --- | --- | --- | --- |
| `AD` | Andorra | `EUR` | Inclusive |  |
| `AE` | United Arab Emirates | `USD` | Inclusive |  |
| `AG` | Antigua and Barbuda | `USD` | Exclusive |  |
| `AI` | Anguilla | `USD` | Exclusive |  |
| `AL` | Albania | `EUR` | Inclusive |  |
| `AM` | Armenia | `USD` | Inclusive |  |
| `AO` | Angola | `USD` | Exclusive |  |
| `AR` | Argentina | `ARS` | Inclusive |  |
| `AS` | American Samoa | `USD` | Exclusive |  |
| `AT` | Austria | `EUR` | Inclusive |  |
| `AU` | Australia | `AUD` | Inclusive | Yes |
| `AW` | Aruba | `USD` | Inclusive |  |
| `AX` | Åland Islands | `EUR` | Exclusive |  |
| `AZ` | Azerbaijan | `USD` | Inclusive |  |
| `BA` | Bosnia and Herzegovina | `EUR` | Inclusive |  |
| `BB` | Barbados | `USD` | Inclusive |  |
| `BD` | Bangladesh | `USD` | Inclusive |  |
| `BE` | Belgium | `EUR` | Inclusive |  |
| `BF` | Burkina Faso | `USD` | Exclusive |  |
| `BG` | Bulgaria | `EUR` | Inclusive |  |
| `BH` | Bahrain | `USD` | Inclusive |  |
| `BI` | Burundi | `USD` | Exclusive |  |
| `BJ` | Benin | `USD` | Exclusive |  |
| `BL` | Saint Barthélemy | `EUR` | Inclusive |  |
| `BM` | Bermuda | `USD` | Inclusive |  |

1–25 of 229

PreviousNext

### Was this page helpful?

Yes, helpfulNo, not helpfulI have feedback
