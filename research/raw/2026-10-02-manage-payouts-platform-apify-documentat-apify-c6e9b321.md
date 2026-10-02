---
url: https://docs.apify.com/platform/actors/publishing/monetize/monthly-payouts
retrieved: 2026-10-02
command: firecrawl scrape https://docs.apify.com/platform/actors/publishing/monetize/monthly-payouts --only-main-content --json
statusCode: 200
transport: firecrawl-cli
completeness: full
title: Manage payouts | Platform | Apify Documentation
---
[Skip to main content](https://docs.apify.com/actors/publishing/monetize/monthly-payouts#__docusaurus_skipToContent_fallback)

On this page

# Manage payouts

Copy for LLM

To be eligible for payouts, you need to complete your billing details, choose a payment method, and verify your identity.

## Complete billing details [Direct link to Complete billing details](https://docs.apify.com/actors/publishing/monetize/monthly-payouts\#complete-billing-details)

To complete your billing details:

1. Log in to [Apify Console](https://console.apify.com/).
2. In the left-side panel, go to **Development** \> **My Actors**.
3. From the table, select one of your Actors.
4. Go to the **Publishing** tab.
5. In the **Monetization** section, set your billing details and payment method.

### Edit billing details [Direct link to Edit billing details](https://docs.apify.com/actors/publishing/monetize/monthly-payouts\#edit-billing-details)

Make sure that your billing information is always up to date. To edit your billing details:

1. Log in to [Apify Console](https://console.apify.com/).
2. In the left-side panel, go to **Development** \> **Insights**.
3. Go to the **Payouts** tab.
4. In the **Billing details** section, select **Edit**.

If you update more information than just the payment method, you have to repeat the identity verification process.

## Verify your identity [Direct link to Verify your identity](https://docs.apify.com/actors/publishing/monetize/monthly-payouts\#verify-your-identity)

To comply with anti-money laundering (AML) regulations, Apify verifies that everyone receiving payments is who they say they are, whether they are an individual or a company. This requirement is part of Apify's [Terms and Conditions](https://docs.apify.com/legal/store-publishing-terms-and-conditions).

To be eligible for payouts, complete the Know Your Customer (KYC) verification process:

1. Log in to [Apify Console](https://console.apify.com/).
2. In the left-side panel, go to **Development** \> **Insights**.
3. Go to the **Payouts** tab.
4. Select **Verify identity**.

If you don't complete the verification process by the time Apify issues payouts for the current month, your earnings roll over to the next month.

### Prepare for verification [Direct link to Prepare for verification](https://docs.apify.com/actors/publishing/monetize/monthly-payouts\#prepare-for-verification)

If you are an individual:

- Provide the full name that matches your legal ID card. Don't use nicknames or aliases.
- Upload a clear, high-resolution photo of your ID card or driver's license. Screenshots, paper copies, or damaged documents are automatically rejected.

If you are a company:

- Provide the full name of the person that performs the verification. This person doesn’t have to be the owner or official representative.
- Provide the official company name, as it appears on your documentation.
- Ensure the business ID or the registration number matches your official registration documents.

## Monthly payouts [Direct link to Monthly payouts](https://docs.apify.com/actors/publishing/monetize/monthly-payouts\#monthly-payouts)

Payout invoices are automatically generated on the 11th of each month. They summarize the profits from all your Actors for the previous month. In accordance with the [Terms and Conditions](https://docs.apify.com/legal/store-publishing-terms-and-conditions), only funds from legitimate users who have already paid are included in your payout invoice.

How negative profits are handled

If your PPE Actor's price doesn't cover its monthly platform usage costs, it will have a negative profit. When it happens, Apify automatically sets that Actor's profit to $0 for the month. This way, a single Actor's loss doesn't reduce your total payout.

### Payout timeline [Direct link to Payout timeline](https://docs.apify.com/actors/publishing/monetize/monthly-payouts\#payout-timeline)

Monthly payouts follow the same schedule, counted in days of the calendar month:

- **Days 1-10**: Apify prepares invoices.
- **Day 11**: Apify issues invoices.
- **Days 11-14**: You [review your invoice](https://docs.apify.com/actors/publishing/monetize/monthly-payouts#review-invoice).
- **Days 21-25**: Apify issues payouts.

### Review your payout invoice [Direct link to Review your payout invoice](https://docs.apify.com/actors/publishing/monetize/monthly-payouts\#review-invoice)

Once your payout invoice is generated, you have 3 days to review it. During this period, you can either approve the invoice or request a revision.

To review your payout invoice:

1. Log in to [Apify Console](https://console.apify.com/).
2. In the left-side panel, go to **Development** \> **Insights**.
3. Go to the **Payouts** tab.

If you take no action, the invoice is automatically approved on the 14th.

### Minimum payout thresholds [Direct link to Minimum payout thresholds](https://docs.apify.com/actors/publishing/monetize/monthly-payouts\#minimum-payout-thresholds)

Your payout invoice must meet the minimum threshold that depends on the payout method:

- $20 for PayPal and Wise
- $100 for other payout methods

If your monthly profit doesn't meet these thresholds, the funds roll over to the next month until the threshold is reached.

### Transfer fees for payouts [Direct link to Transfer fees for payouts](https://docs.apify.com/actors/publishing/monetize/monthly-payouts\#transfer-fees-for-payouts)

Due to transfer fees, the payout you receive might be lower than the invoiced amount.

International transfers involve intermediaries that often deduct transfer fees. These fees typically range from $10 to $50 and depend on the destination country and the banks involved in the process. Deductions are usually applied automatically during the transfer.

Apify sends payments from the Czech Republic (CZ) through the SWIFT wire transfer. For international transfers, Apify uses the SHA (shared costs) method, where you pay the fees charged by an intermediary or recipient bank and Apify covers its own bank fees.

For payments to the United States, the Automated Clearing House (ACH) method isn't possible.

Consider PayPal as your payout method

For more transparent and lower fees, as well as faster transactions, consider using PayPal. As the only intermediary between Apify and you, PayPal is also the only party that might charge a fee.

Note that Apify's payment methods and banking partners might change without prior notice.

## Common issues [Direct link to Common issues](https://docs.apify.com/actors/publishing/monetize/monthly-payouts\#common-issues)

Check the most common issues related to payouts.

### Deduction on the invoice [Direct link to Deduction on the invoice](https://docs.apify.com/actors/publishing/monetize/monthly-payouts\#deduction-on-the-invoice)

A deduction is an amount subtracted from your payout. It might happen if a platform user requests credit compensation related to your Actor when, for example, the Actor malfunctioned or didn't deliver the expected results.

The Apify team manually reviews each compensation request before processing a deduction. You can request a revision of the deduction during the [review period](https://docs.apify.com/actors/publishing/monetize/monthly-payouts#review-invoice).

### Payout delays [Direct link to Payout delays](https://docs.apify.com/actors/publishing/monetize/monthly-payouts\#payout-delays)

The following are the most common reasons for payout delays:

- **Wire transfer processing.** Wire transfers can take longer to arrive. Allow a few additional business days for the funds to appear in your account.
- **Usage review.** If Apify detects suspicious usage patterns related to your Actors, your payout might be withheld during the investigation. If it happens, Apify will contact you.

### Payout didn't arrive [Direct link to Payout didn't arrive](https://docs.apify.com/actors/publishing/monetize/monthly-payouts\#payout-didnt-arrive)

The following are the most common reasons for not receiving a payout:

- Your payout invoice didn't meet the [minimum threshold](https://docs.apify.com/actors/publishing/monetize/monthly-payouts#minimum-payout-thresholds).
- Your bank or service provider declined the transaction, causing the payment to fail or be returned.
- You updated your account details after the invoice has already been approved and processed for payment. The payout is sent to the account listed on the invoice.
- You didn't complete the [identity verification](https://docs.apify.com/actors/publishing/monetize/monthly-payouts#verify-your-identity) process.

- [Complete billing details](https://docs.apify.com/actors/publishing/monetize/monthly-payouts#complete-billing-details)
  - [Edit billing details](https://docs.apify.com/actors/publishing/monetize/monthly-payouts#edit-billing-details)
- [Verify your identity](https://docs.apify.com/actors/publishing/monetize/monthly-payouts#verify-your-identity)
  - [Prepare for verification](https://docs.apify.com/actors/publishing/monetize/monthly-payouts#prepare-for-verification)
- [Monthly payouts](https://docs.apify.com/actors/publishing/monetize/monthly-payouts#monthly-payouts)
  - [Payout timeline](https://docs.apify.com/actors/publishing/monetize/monthly-payouts#payout-timeline)
  - [Review your payout invoice](https://docs.apify.com/actors/publishing/monetize/monthly-payouts#review-invoice)
  - [Minimum payout thresholds](https://docs.apify.com/actors/publishing/monetize/monthly-payouts#minimum-payout-thresholds)
  - [Transfer fees for payouts](https://docs.apify.com/actors/publishing/monetize/monthly-payouts#transfer-fees-for-payouts)
- [Common issues](https://docs.apify.com/actors/publishing/monetize/monthly-payouts#common-issues)
  - [Deduction on the invoice](https://docs.apify.com/actors/publishing/monetize/monthly-payouts#deduction-on-the-invoice)
  - [Payout delays](https://docs.apify.com/actors/publishing/monetize/monthly-payouts#payout-delays)
  - [Payout didn't arrive](https://docs.apify.com/actors/publishing/monetize/monthly-payouts#payout-didnt-arrive)

reCAPTCHA

Recaptcha requires verification.

protected by **reCAPTCHA**
