---
url: https://docs.apify.com/actors/monetize/set-up-monetization.md
retrieved: 2026-10-04
command: firecrawl scrape https://docs.apify.com/actors/monetize/set-up-monetization.md --only-main-content --json
statusCode: 200
transport: firecrawl-cli
completeness: full
---
---
title: Set up Actor monetization
url: https://docs.apify.com/actors/monetize/set-up-monetization.md
parents:
  - [Apify documentation](https://docs.apify.com/llms.txt)
  - [Actors](https://docs.apify.com/actors.md)
  - [Monetize](https://docs.apify.com/actors/publishing/monetize.md)
previous: [Monetize](https://docs.apify.com/actors/publishing/monetize.md)
next: [Pay per event pricing model](https://docs.apify.com/actors/publishing/monetize/pay-per-event.md)
---

> ## Documentation index
> Fetch the complete documentation index at: https://docs.apify.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Set up Actor monetization

Set up monetization to earn revenue every time users run your Actors on the Apify platform.

## Monetize your Actor

To set up monetization for your Actor, first complete your billing and payment details. Then, you can define the pricing for your Actor:

1. Log in to [Apify Console](https://console.apify.com).
2. In the left-side panel, go to **Development** > **My Actors**.
3. From the table, select the Actor you want to monetize.
4. Go to the **Publishing** tab.
5. In **Monetization** section, select **Set up monetization**.

The monetization setup consists of three steps:

1. In the **Actor pricing** step, you can:

   <!-- -->

   * Modify or delete the [apify-actor-start](https://docs.apify.com/actors/publishing/monetize/pay-per-event.md#synthetic-start-event) event.
   * Modify or delete the [apify-default-dataset-item](https://docs.apify.com/actors/publishing/monetize/pay-per-event.md#synthetic-default-dataset-item-event) event.
   * Define [custom events](https://docs.apify.com/actors/publishing/monetize/pay-per-event.md#actor-events) and their prices.
   * [Transfer the platform usage costs on to users](https://docs.apify.com/actors/publishing/monetize/pay-per-event.md#platform-usage-costs).
   * Set the minimal cost that users can choose as max cost per run.

2. In the **Primary event** step, select the event that best represents the main value of your Actor. By default, the dataset event or the only existing event is used.

3. In the **Review** step, verify the final pricing for your Actor before confirming.

![Publishing tab in Apify Console](/assets/images/monetization-23ad2412d287748a457af98d72e3e93b.svg)

## Change monetization

To update the monetization of your Actor, follow the same steps as in the Monetize your Actor section.

Be careful about increasing prices. If you make your Actor too expensive, users might find an alternative solution in Apify Store. Avoid setting high prices exclusively for users on a free plan. Such users often become paying users once they see the value of your Actor, but they need to test it on enough data first.

Negative profit

If your Actor generates negative profit, [follow the recommendations](https://docs.apify.com/actors/publishing/monetize/pay-per-event.md#avoid-negative-profit) before increasing the price.

### Significant changes

The following changes are considered significant:

* Changing the pricing model. For example, from rental to pay per event.
* Increasing prices.
* Adding a new paid event.

When you submit a significant change, users of your Actor are notified and the change is scheduled to take effect after 14 days. During this notice period, the current pricing remains active.

You can't cancel a planned change

Once you submit a significant change, you can't cancel or modify it. To revert a planned change, [contact support](https://apify.com/contact).

You can submit significant changes once per month per Actor, so plan your pricing strategy carefully. A pending change blocks submitting new ones. Wait for the significant change to take effect before submitting another one.

Note that if your Actor has no paying users, the waiting period doesn't apply and the change takes effect immediately.

For details, see [Apify Store publishing terms and conditions](https://docs.apify.com/legal/store-publishing-terms-and-conditions.md).

### Non-significant changes

The following changes take effect immediately and don't have any restrictions:

* Decreasing prices.
* Increasing prices if the Actor has no paying users.
* Removing events.
* Updating event descriptions.
* Adjusting settings that aren't related to pricing.

