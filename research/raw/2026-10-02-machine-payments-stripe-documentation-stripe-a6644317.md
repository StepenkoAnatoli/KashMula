---
url: https://docs.stripe.com/payments/machine
retrieved: 2026-10-02
command: firecrawl scrape https://docs.stripe.com/payments/machine --only-main-content --json
statusCode: 200
transport: firecrawl-cli
completeness: full
title: Machine payments | Stripe Documentation
---
hCaptcha

hCaptcha

Please try again. ⚠️

Verify

Afrikaans

Albanian

Amharic

Arabic

Armenian

Azerbaijani

Basque

Belarusian

Bengali

Bulgarian

Bosnian

Burmese

Catalan

Cebuano

Chinese

Chinese Simplified

Chinese Traditional

Corsican

Croatian

Czech

Danish

Dutch

English

Esperanto

Estonian

Finnish

French

Frisian

Gaelic

Galacian

Georgian

German

Greek

Gujurati

Haitian

Hausa

Hawaiian

Hebrew

Hindi

Hmong

Hungarian

Icelandic

Igbo

Indonesian

Irish

Italian

Japanese

Javanese

Kannada

Kazakh

Khmer

Kinyarwanda

Kirghiz

Korean

Kurdish

Lao

Latin

Latvian

Lithuanian

Luxembourgish

Macedonian

Malagasy

Malay

Malayalam

Maltese

Maori

Marathi

Mongolian

Nepali

Norwegian

Nyanja

Oriya

Persian

Polish

Portuguese (Brazil)

Portuguese (Portugal)

Pashto

Punjabi

Romanian

Russian

Samoan

Shona

Sindhi

Sinhalese

Serbian

Slovak

Slovenian

Somali

Southern Sotho

Spanish

Sundanese

Swahili

Swedish

Tagalog

Tajik

Tamil

Tatar

Teluga

Thai

Turkish

Turkmen

Uyghur

Ukrainian

Urdu

Uzbek

Vietnamese

Welsh

Xhosa

Yiddish

Yoruba

Zulu

EN

[hCaptcha logo, opens new window with more information](https://www.hcaptcha.com/what-is-hcaptcha-about?ref=b.stripecdn.com&utm_campaign=5034f7f0-a742-48aa-89e2-062ece60f0d6&utm_medium=challenge&hl=en "hCaptcha logo, opens new window with more information")

[Skip to content](https://docs.stripe.com/payments/machine#main-content)

Tool calls and HTTP requests

[Create account](https://dashboard.stripe.com/register) or [Sign in](https://dashboard.stripe.com/login?redirect=https%3A%2F%2Fdocs.stripe.com%2Fpayments%2Fmachine)

[The Stripe Docs logo](https://docs.stripe.com/)

Search

`/`Ask AI

[Create account](https://dashboard.stripe.com/register) [Sign in](https://dashboard.stripe.com/login?redirect=https%3A%2F%2Fdocs.stripe.com%2Fpayments%2Fmachine)

APIs & SDKsHelp

[Overview](https://docs.stripe.com/payments) [Accept a payment](https://docs.stripe.com/payments/accept-a-payment)

Online payments

[Overview](https://docs.stripe.com/payments/online-payments) [Find your use case](https://docs.stripe.com/payments/use-cases/get-started)

Use Payment Links

Build a payments page

Build a custom integration with Elements

Build an in-app integration

Use Managed Payments

[Recurring payments](https://docs.stripe.com/recurring-payments) [Migrate legacy integrations](https://docs.stripe.com/payments/migrations)

In-person payments

Terminal overview

[Availability](https://docs.stripe.com/terminal/payments/collect-card-payment/supported-card-brands)

Readers

Ready-made apps

Custom integration

Payment methods

Add payment methods

Manage payment methods

Faster checkout with Link

Payment operations

Analytics

[Balances and settlement time](https://docs.stripe.com/payments/balances)

Compliance and security

Currencies

Declines

Disputes

Payouts

[Receipts](https://docs.stripe.com/receipts) [Refunds and cancellations](https://docs.stripe.com/refunds)

Advanced integrations

Custom payment flows

Flexible acquiring

Off-Session Payments

Multiprocessor orchestration

Beyond payments

Incorporate your company

Agentic commerce

[Overview](https://docs.stripe.com/agentic-commerce)

Build an agent

Sell to agents

[Retail and e-commerce](https://docs.stripe.com/agentic-commerce/sellers/use-cases/retail)

[Service bookings](https://docs.stripe.com/agentic-commerce/sellers/use-cases/booking)

Tool calls and HTTP requests

[Accept payments for MCP tools](https://docs.stripe.com/agentic-commerce/monetize-mcp)

[MPP](https://docs.stripe.com/payments/machine/mpp)

[x402](https://docs.stripe.com/payments/machine/x402)

[Build a custom seller integration](https://docs.stripe.com/agentic-commerce/sellers/custom)

[Manage your integration](https://docs.stripe.com/agentic-commerce/sellers/manage)

Concepts and references

Financial Connections

Climate

United States

English (United States)

[Frontier](https://docs.stripe.com/release-phases)

# Machinepayments [Frontier](https://docs.stripe.com/release-phases)

## Allow agents to pay-per-call using MPP and x402.

Ask about this page

Copy for LLM

View as Markdown

Install tools

Monetizing an API or service typically requires account creation, subscription selection, and payment entry. These flows require human input, which blocks agents from completing tasks autonomously.

Machine payments let agents pay for APIs and services programmatically. Your server returns a payment challenge, the agent presents a valid payment credential, and Stripe settles the payment to your Stripe balance.

Machine payments on Stripe works best with the Machine Payments Protocol (MPP) that is able to accept card and stablecoin payments. Stripe also supports stablecoin payments over the x402 protocol.

Start accepting payments from agents

Learn how to accept machine payments from agents.

[Get started](https://docs.stripe.com/payments/machine/mpp)

![](https://b.stripecdn.com/docs-statics-srv/assets/hero.49388b4fdf3277e6bb8b71d2a97654d7.png)

## Features

Integrating with Stripe means reconciliation, reporting, and the rest of your Stripe workflows continue to work as expected.

| **Stripe payments** | Payments land directly in your Stripe balance and settle in fiat. Metrics, reporting, and multi-currency payouts work the same as any other payment in Stripe. |
| **Refunds** | Refunds are available through the [Refunds API](https://docs.stripe.com/refunds) and in the Dashboard. |
| **Microtransactions** | - For card payments through [Shared Payment Tokens (SPTs)](https://docs.stripe.com/agentic-commerce/concepts/shared-payment-tokens), the minimum amount is 0.50 USD.<br>- For [stablecoin payments](https://docs.stripe.com/payments/stablecoin-payments), the minimum amount is 0.01 USDC.<br>- For [MPP sessions](https://docs.stripe.com/payments/machine/mpp/sessions), you can charge users for work in sub-cent increments, but the minimum settlement amount is 0.01 USDC. |
| **Stripe Connect** | Machine payments are available for Connect platforms across all charge types. |

## Availability

Accept payments from agents with a variety of payment methods, including cards through [Shared Payment Tokens (SPTs)](https://docs.stripe.com/agentic-commerce/concepts/shared-payment-tokens) and [stablecoin payments](https://docs.stripe.com/payments/stablecoin-payments).

### Accept card payments

MPP supports fiat payments using cards with SPTs, which are scoped grants that let an agent use a customer’s payment method, such as a card, through your [Stripe profile](https://docs.stripe.com/get-started/account/profile). Each SPT includes usage and expiration limits.

SPTs are available to businesses in all US states. If your business operates outside the US, [view all supported countries](https://docs.stripe.com/agentic-commerce/concepts/shared-payment-tokens). You can accept SPTs in [all Stripe-supported currencies](https://docs.stripe.com/currencies), and issue them from the [Link Agent Wallet](https://link.com/agents).

### Accept stablecoin payments

Stripe supports stablecoin payments on both MPP and x402 protocols across the following networks and currencies.

| Protocol | Network | Currency |
| --- | --- | --- |
| MPP | Tempo | USDC.e |
| MPP | Solana | USDC |
| x402 | Base | USDC |

Stablecoin payments are available to businesses in all US states, except New York. For businesses operating outside of the US, email [machine-payments@stripe.com](mailto:machine-payments@stripe.com) with your Stripe account ID to request access to stablecoin payments in 30+ countries.

To enable the payment method:

1. Enable the **Stablecoins and Crypto** payment method for your account in the [Dashboard](https://dashboard.stripe.com/settings/payment_methods).
2. Stripe reviews your access request and contacts you for more details if necessary. After we approve your request, the Stablecoins and Crypto payment method becomes active in the Dashboard.

## Submit your integration

After you finish your integration, submit it for listing in the [Stripe Directory](https://docs.stripe.com/directory). The Directory is a catalog of tools and services that helps agents find your business.

Email [machine-payments@stripe.com](mailto:machine-payments@stripe.com) with:

- Your business name
- Your Stripe account ID
- Your Stripe profile ID. If necessary, [claim your Stripe profile](https://docs.stripe.com/get-started/account/profile).
- A link to your `llms.txt` file and links to any agent skills
- Whether your integration accepts SPTs, stablecoins, or both
- One to three example prompts that demonstrate your use case

## Integration guides

Learn how to add machine payments to any API or service using MPP or x402.

[Machine Payments Protocol (MPP)\\
\\
Use MPP to accept machine payments from agents.](https://docs.stripe.com/payments/machine/mpp "Machine Payments Protocol (MPP)")

[x402\\
\\
Use x402 to accept machine payments from agents.](https://docs.stripe.com/payments/machine/x402 "x402")

[Starter code\\
\\
Server](https://github.com/stripe-samples/machine-payments "Starter code")
