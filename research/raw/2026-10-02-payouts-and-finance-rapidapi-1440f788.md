---
url: https://docs.rapidapi.com/docs/payouts-and-finance
retrieved: 2026-10-02
command: firecrawl scrape https://docs.rapidapi.com/docs/payouts-and-finance --only-main-content --json
statusCode: 200
transport: firecrawl-cli
completeness: full
title: Payouts and Finance
---
For AI agents: visit https://docs.rapidapi.com/llms.txt for an index of all pages formatted in Markdown and endpoints in OpenAPI. Append .md to any documentation page URL to get its markdown version.

> 📘
>
> ### rapidapi.com only   [Skip link to rapidapi.com only](https://docs.rapidapi.com/docs/payouts-and-finance\#rapidapicom-only)
>
> This page applies rapidapi.com providers. It does not apply to Enterprise Hub customers.

When a developer subscribes to a pricing plan for your API on Rapid or incurs an overage, you as an API provider will receive a payout after Rapid processes a final payment from the developer.

> ❗️
>
> ### Updated marketplace fee   [Skip link to Updated marketplace fee](https://docs.rapidapi.com/docs/payouts-and-finance\#updated-marketplace-fee)
>
> Starting November 15th, 2025, our transaction fees will be updated to cover processing costs that the platform has been absorbing until now. This change helps ensure the long-term sustainability of the marketplace.
>
> The marketplace fee on all payments made through the API Hub will be %25.

> 📘
>
> ### Rapid's marketplace fee   [Skip link to Rapid's marketplace fee](https://docs.rapidapi.com/docs/payouts-and-finance\#rapids-marketplace-fee)
>
> Rapid takes a flat 25% marketplace fee on all payments made through the API Hub. For example, if you price an API subscription plan at $100, you will receive $75 from Rapid if a developer purchases your plan. This marketplace fee covers payment processing, site infrastructure, and administrative fees. This marketplace fee does not cover the fees associated with payouts processed through PayPal.

## How payouts work   [Skip link to How payouts work](https://docs.rapidapi.com/docs/payouts-and-finance\#how-payouts-work)

A developer's credit card is charged after one of three instances:

|  |
| --- |
| 1. A developer subscribes to an API's pricing plan for the first time |
| 2. A developer is billed every month for their API plan subscription |
| 3. A developer incurs an overage on an API |

All charges related to your API are consolidated within the given month and processed for payment at the end of the following month. This allows Rapid time for the collection of payments, processing of refunds or disputes, and the reconciliation of accounts. Rapid will then issue the payment (reduced by the marketplace fee and PayPal processing fee) to your PayPal account.

As an example, if developers subscribe to your API’s PRO plan on January 1st, 5th, and 20th for $10 each, you should receive a total payment of $24 less any applicable PayPal fees for that month. In this example, the $24 payment should arrive in your PayPal account in the first week of March.

## Adding your PayPal account information   [Skip link to Adding your PayPal account information](https://docs.rapidapi.com/docs/payouts-and-finance\#adding-your-paypal-account-information)

Rapid currently only pays out API providers via PayPal. Unfortunately, we cannot accommodate other payout methods. Each payout on PayPal will include the name of the user, the name of the API plan the user has subscribed to, and the name of the API marketplace.

Here's how to add your PayPal information to the system:

Log in to rapidapi.com, click your avatar in the upper right and select **Personal Payouts**.

![Navigating to a user's personal payout information.](https://files.readme.io/40a1f1f-personal-payouts.png)Navigating to a user's personal payout information.

Click **Link PayPal** account and log in to your PayPal account to link it to Rapid.

![Linking a PayPal account to Rapid to enable payments from your API subscribers.](https://files.readme.io/90f141d-link-paypal-account.png)Linking a PayPal account to Rapid to enable payments from your API subscribers.

> 🚧
>
> ### Adding a PayPal email address   [Skip link to Adding a PayPal email address](https://docs.rapidapi.com/docs/payouts-and-finance\#adding-a-paypal-email-address)
>
> If you do not add a PayPal address to your account, there is unfortunately no way for us to send you money! We will attempt to email you at least three times to add an email if a payment is generated and no address is found (or the address is invalid). Please be sure to fill out this information and keep it up to date so that we can send your payments.

## Forgiveness, disputes, and failed payments   [Skip link to Forgiveness, disputes, and failed payments](https://docs.rapidapi.com/docs/payouts-and-finance\#forgiveness-disputes-and-failed-payments)

Very occasionally, there will be an issue where a developer fails to make a payment for their API usage. These tend to fall into four categories:

|  |
| --- |
| 1. Forgiveness request |
| 2. Disputes and Chargebacks |
| 3. Failed payments |
| 4. Rapid error |

## Forgiveness request   [Skip link to Forgiveness request](https://docs.rapidapi.com/docs/payouts-and-finance\#forgiveness-request)

Rapid alerts users via email when they reach their quota limits. On occasion, a developer may have a bug in the system or inadvertently generate large overages. In these instances, he or she may reach out to us or you (the API provider) to ask for the overage fee to be waived. We do not refund any overage without your explicit permission. We leave these instances to your discretion as an API provider and fellow developer.

## Disputes and chargebacks   [Skip link to Disputes and chargebacks](https://docs.rapidapi.com/docs/payouts-and-finance\#disputes-and-chargebacks)

Rapid incorporates an industry-standard credit card verification and anti-fraud solution to prevent fraudulent charges. In rare instances, a user may dispute a charge or initiate a chargeback. Rapid will then conduct a full investigation and aim to achieve resolution by working with the user and you, the API provider. If a refund is issued or a chargeback occurs, Rapid will offset the amount paid to you by the refunded amount. If you have suspicions of fraudulent behavior from one of your users, please contact support at [https://support.rapidapi.com/](https://support.rapidapi.com/) and we will investigate.

## Failed payments   [Skip link to Failed payments](https://docs.rapidapi.com/docs/payouts-and-finance\#failed-payments)

Rapid makes several attempts to collect a payment before failing and cancelling a user's subscription. We are diligent in communicating with developers that have failed payments on an outstanding balance to come to a resolution. Rapid will make payouts to the API provider only when Rapid has received final payments from or on behalf of the user. A final payment is deemed to have occurred when the applicable credit card company or bank has fully settled the payment.

## Rapid error   [Skip link to Rapid error](https://docs.rapidapi.com/docs/payouts-and-finance\#rapid-error)

If you think there is a processing error on our side, reach out to support at [https://support.rapidapi.com/](https://support.rapidapi.com/) and we will investigate the issue and come to a fair resolution.

## Invoices and custom documents   [Skip link to Invoices and custom documents](https://docs.rapidapi.com/docs/payouts-and-finance\#invoices-and-custom-documents)

We can generate custom invoices for you or your developers per request (see the [Invoices](https://docs.rapidapi.com/docs/billing) section). W9 forms are also available upon request by reaching out to support at [https://support.rapidapi.com/](https://support.rapidapi.com/).

Updated11 months ago

* * *
