---
url: https://soloopslab.com/blog/app-store-payouts-taxes
retrieved: 2026-10-03
command: firecrawl scrape https://soloopslab.com/blog/app-store-payouts-taxes --only-main-content --json
statusCode: 200
transport: firecrawl-cli
completeness: full
title: App Store Payout Schedule and Taxes: Apple vs Google Play | Solo Ops Lab
---
[Skip to content](https://soloopslab.com/blog/app-store-payouts-taxes#main)

Your app sold something today and the dashboard shows it, but Apple only promises to pay within 45 days after its fiscal month closes, and Google pays around the 15th of the following month. This guide settles exactly when each store pays, what each one deducts on the way, which tax form each sends a US developer, and how to report the number on that form without paying tax twice on the commission. It is built from Apple’s and Google’s own help pages and the IRS, collected on September 28, 2026.

I have shipped my own app, and the store paperwork is the part most launch guides skip. So this is the reference I wanted: dates, minimums, fees, forms.

This is not licensed tax or financial advice. Rules change, and your situation is yours; the IRS’s own [Form 1099-K guidance](https://www.irs.gov/businesses/what-to-do-with-form-1099-k) is the primary source to check against.

## When Apple pays: fiscal months, not calendar months

Apple does not pay on calendar months. It pays on its fiscal calendar, and the fiscal year is a 52- or 53-week period ending on the last Saturday of September. Fiscal 2026 ran 52 weeks, so a new fiscal year started on Sunday, September 27, 2026.

The official promise is short. Apple says payments go to your bank “within 45 days of the last day of the fiscal month in which the transaction was completed”. Payout-date lists from analytics companies show earlier estimated dates, and they are useful, but they are estimates. Plan cash on the 45 days. Treat anything earlier as a pleasant surprise.

A few mechanics shape what lands:

- Financial reports for the previous fiscal month are ready by the first Friday of the current one.
- Apple’s bank consolidates each currency into a single payment per fiscal month.
- Conversion to your account currency uses a rate typically set no more than three business days before the money arrives, so the estimate in App Store Connect can differ from the deposit.
- You need a Paid Apps Agreement in effect, banking details on file, and proceeds above the minimum threshold.

For a US bank account in US dollars, the threshold table lists 0.02, which is effectively no minimum. Bank countries and currencies not in the table must exceed 40 USD. Below the line, proceeds carry forward to the next period instead of disappearing.

One detail from the proceeds page matters more than it looks. If your bank returns a payment, Apple says it can take up to two regular payment cycles to resend it. A typo in a routing number can cost you two months.

## When Google Play pays: the 15th

Google runs on the plain calendar. Orders processed, refunded, or charged back from the first to the last day of a month are paid out around the 15th of the following month. May sales, for example, start moving on June 15.

![Two stylized clocks, one with uneven segments and one with even monthly segments, both feeding into a bank icon.](https://soloopslab.com/images/posts/app-store-payouts-taxes/01-two-payout-clocks.jpg)

Google does not start payouts on weekends or holidays; a 15th that lands on a Saturday starts the following Monday. After initiation, an electronic funds transfer takes 2 to 3 business days and a wire 5 to 7. The balance has to clear US$1 for local-currency payouts or US$100 for USD wires.

If you sell on both stores, you get two deposits on two rhythms. Google’s is the one you can put in a calendar without thinking.

## Apple vs Google Play side by side

Every cell below comes from the store’s own help page or agreement, collected on September 28, 2026. Where a store’s page is silent, the cell says so rather than guessing.

| Question | Apple App Store | Google Play |
| --- | --- | --- |
| Payout period | Apple fiscal month | Calendar month |
| Official timing | Within 45 days after fiscal month ends | Initiated around the 15th of next month |
| Minimum (US, USD account) | 0.02, effectively none; 40 USD default elsewhere | US$1 local currency, US$100 USD wire |
| Small-developer rate | 15% in Small Business Program, under $1M proceeds | 10% service fee on first $1M + 5% billing fee, US since June 30, 2026 |
| Subscriptions | 70% to you in year one, 85% after one year of paid service | 10% + 5% billing fee |
| Tax form you submit | W-9 with SSN, ITIN, or EIN | W-9 for US persons |
| Year-end form you get | 1099-K; Apple says it won’t issue a 1099-MISC | 1099-K by postal mail by January 31 |
| What the 1099-K amount is | Unadjusted gross sales, before commission, fees, refunds | Gross sales, no adjustment for refunds or chargebacks |
| US sales tax | Apple collects and remits | Google collects and remits in every state, with Play billing |

Two cells deserve a second look before you rely on them. They come next.

## What each store takes before you see a dollar

Outside the Small Business Program, Apple’s subscription page says you receive 70% of the price, minus applicable taxes, during a subscriber’s first year. After a subscriber builds one year of paid service, your share of that subscription rises to 85%. Free trials do not count toward that year.

The Small Business Program moves the rate to 15% for developers with up to $1 million in proceeds in the prior calendar year, and for new developers. Cross $1 million during the year and the standard rate applies to later sales. It is not automatic. You enroll, declare associated developer accounts, and the reduced rate takes effect 15 days after the end of the fiscal month in which Apple approves you. If you are a solo developer who has not enrolled, do it before your next release. Every fiscal month you wait is a month at the higher rate.

Google changed its US fees on June 30, 2026. Service and billing fees are now separate: 10% on your first $1 million in annual earnings, plus a 5% billing fee when the purchase goes through Google Play’s billing. Auto-renewing subscriptions also carry 10% plus the billing fee. Before the change, Google’s 15% rate on the first $1 million went to developers enrolled in its 15% tier. The help pages do not say whether the new 10% needs a separate sign-up, so check the fee settings in Play Console instead of assuming.

## Sales tax: why you do not collect it on store sales

This is the one piece of paperwork the stores take off your plate. Apple’s agreement lists the United States among the regions where Apple collects and remits sales taxes on your app sales, and it says Apple will collect and remit any state or local sales or use tax it believes is due. You still pick a tax category for each app and in-app purchase, and that choice can change your proceeds.

Google says it determines, charges, and remits sales tax for Play Store app and in-app purchases in US states. The exception is alternative billing: route a purchase through your own processor and the sales tax becomes your job.

Income tax is another matter. Apple’s exhibit puts it plainly: tax on your income is solely your responsibility.

## The tax forms: W-9 in, 1099-K out

Both stores want a W-9 from US developers. Apple asks for an SSN or ITIN if you are an individual, or an EIN for a business entity. Once submitted, you cannot edit the form in App Store Connect; corrections go through Apple. Get the legal name and number right the first time.

Google requires a W-9 from US persons. Skip it or give a bad number and Google may withhold 24% as backup withholding, and it can hold payouts.

At year end, both stores issue Form 1099-K, not 1099-MISC. Apple is explicit: it won’t issue a 1099-MISC, because App Store sales are between you and the customer and you are the seller. Some tax guides still say Apple sends a 1099-MISC. It does not.

Now the threshold wrinkle. Apple’s help page, as of today, still describes a 1099-K line of $5,000 in unadjusted gross sales. The IRS says that after the One Big Beautiful Bill, a payment platform files only when payments exceed $20,000 and transactions exceed 200, and that rule was reinstated retroactively. So you might get a form, or not. It does not matter for what you owe. The IRS is clear that income is reportable whether or not a 1099-K arrives.

## Gross vs deposits: what goes on Schedule C

This is the question none of the payout guides answer, and it is where solo developers either double count or under-report.

![3D blocks showing a tall stack losing two slices before a shorter stack flows into a vault.](https://soloopslab.com/images/posts/app-store-payouts-taxes/02-gross-to-deposit.jpg)

The 1099-K shows gross sales. Your bank shows what is left after the store’s cut and refunds. The IRS says the 1099-K amount is not adjusted for fees, credits, or refunds, that those items are not taxable income, and that you can deduct them from the gross.

Here is a made-up example with round numbers, not anyone’s real results. Say your 1099-K from one store shows $10,000. Customers were refunded $400. The store’s commission on what stuck was $1,440. Your deposits for the year, before any timing differences, add up to $8,160.

| Schedule C line | What goes there | Example |
| --- | --- | --- |
| Line 1, gross receipts | The 1099-K gross | $10,000 |
| Line 2, returns and allowances | Customer refunds | $400 |
| Line 10, commissions and fees | Store commission | $1,440 |
| Net from this store | Should match deposits | $8,160 |

Reporting only the $8,160 gives the same profit, but the gross on your return then sits below the gross the IRS received. Mismatches like that are what trigger letters. Report gross, subtract on the proper lines, and both numbers reconcile.

The harder question is the calendar year. Sales in December settle into a fiscal month that Apple pays in the following calendar year. Apple’s 1099-K counts sales in the calendar year. Your deposits land in the next one. IRS Publication 538 says income is constructively received when it is credited or made available to you, and that income received by your agent counts as received when the agent gets it. Apple’s agreement appoints Apple Inc. as your agent for US App Store distribution. Read together, that points toward reporting sales in the year they happen, matching the 1099-K. Take that exact question to whoever prepares your return, then do it the same way every year.

## Planning cash around the lag

The lag is what hurts a launch. If your app earns in its first week, Apple money from that week can arrive up to 45 days after the fiscal month closes, and your ad bill does not wait. That is one reason I lean on free channels while my own app is new; the approach is in [how to promote an app with no budget](https://soloopslab.com/blog/promote-app-no-budget), and the messaging side is in [cold outreach for an app launch](https://soloopslab.com/blog/cold-outreach-app-launch).

Taxes do not wait for Apple’s calendar either. Estimated payments run on federal due dates, so park a share of each deposit the day it lands. The mechanics of setting that share and paying it are in [how creators pay taxes](https://soloopslab.com/blog/how-creators-pay-taxes). If a brand deal or a contractor also pays you, the difference between the two forms that can arrive is in [1099-NEC vs 1099-K for creators](https://soloopslab.com/blog/1099-nec-vs-1099-k-creators). More money-side guides live under [money ops](https://soloopslab.com/category/money-ops).

## January reconciliation checklist

Run this once a year, in January, before any 1099-K arrives. It takes an hour and it gives you your own numbers to compare against the forms.

![Overhead view of a blank ledger, laptop, envelope, coins, and calendar on a mustard background.](https://soloopslab.com/images/posts/app-store-payouts-taxes/03-january-reconciliation.jpg)

1. Download every App Store financial report for fiscal months touching the calendar year; Apple keeps them for ten years.
2. Download the Transaction Tax Report to see US sales tax Apple applied, so you never book it as income.
3. Export Google Play earnings for January through December.
4. Add up gross sales, refunds, and commissions per store, by calendar month.
5. Match deposits in your bank to each store’s payments; flag any returned or held payment.
6. When the 1099-K arrives, compare its gross to your gross. If it is wrong, ask the store for a corrected form.
7. Hand your preparer gross, refunds, and commissions as three numbers, per store.

Open App Store Connect today, go to Business, and confirm three things: the Paid Apps Agreement is active, your W-9 is on file, and you are enrolled in the Small Business Program. Then do the same check for the W-9 in your Google payments profile.

## Frequently asked questions

Does Apple send app developers a 1099-MISC?

No. Apple's App Store Connect help says it won't issue a 1099-MISC because App Store sales are between you and the customer. US developers who meet the reporting threshold get a Form 1099-K instead, mailed by January 31. The amount is unadjusted gross sales, before Apple's commission, fees, and refunds.

When does Google Play pay developers?

Google initiates payouts on the 15th of each month for the previous calendar month's orders, skipping weekends and bank holidays. Electronic funds transfers take about 2 to 3 business days to land and wires about 5 to 7. The balance must be at least US$1 for local-currency payouts or US$100 for USD wires.

Do I report App Store gross sales or my net deposits on Schedule C?

The IRS says a 1099-K shows gross payments that are not adjusted for fees or refunds, and that you can deduct those items. The common approach is to report the gross on line 1 of Schedule C, refunds on line 2, and store commissions on line 10, so the result ties to both the form and your deposits.

Do I have to collect sales tax on in-app purchases?

Not for sales through the stores' own billing. Apple's agreement lists the United States among regions where Apple collects and remits the taxes, and Google says it handles US sales tax for Play billing purchases in every state. If you use Google's alternative billing, that responsibility shifts to you.

## Sources

01. [App Store Connect Help: Overview of receiving payments](https://developer.apple.com/help/app-store-connect/getting-paid/overview-of-receiving-payments/)
02. [App Store Connect Help: Minimum payment threshold](https://developer.apple.com/help/app-store-connect/reference/reporting/minimum-payment-threshold)
03. [App Store Connect Help: View payments and proceeds](https://developer.apple.com/help/app-store-connect/getting-paid/view-payments-and-proceeds/)
04. [App Store Connect Help: Download financial reports](https://developer.apple.com/help/app-store-connect/getting-paid/download-financial-reports/)
05. [Apple Inc. Form 10-Q for the quarter ended December 27, 2025 (fiscal year definition)](https://www.sec.gov/Archives/edgar/data/320193/000032019326000006/aapl-20251227.htm)
06. [Apple Developer: App Store Small Business Program](https://developer.apple.com/app-store/small-business-program/)
07. [Apple Developer: Auto-renewable subscriptions](https://developer.apple.com/app-store/subscriptions/)
08. [App Store Connect Help: Provide tax information](https://developer.apple.com/help/app-store-connect/manage-tax-information/provide-tax-information/)
09. [App Store Connect Help: Manage invoices and other tax documents](https://developer.apple.com/help/app-store-connect/manage-tax-information/manage-invoices-and-other-tax-documents/)
10. [Apple: Exhibits to Schedule 2 and 3 (Aug 21, 2025)](https://developer.apple.com/support/downloads/terms/exhibits/Exhibits-to-Schedule-2-and-3-20250821-English.pdf)
11. [App Store Connect Help: Set a tax category](https://developer.apple.com/help/app-store-connect/manage-app-information/set-a-tax-category/)
12. [Play Console Help: Order processing and payouts](https://support.google.com/googleplay/android-developer/answer/137997?hl=en)
13. [Google Payments Center Help: Merchant payout schedule](https://support.google.com/paymentscenter/answer/7159355?hl=en)
14. [Play Console Help: Understanding Google Play's lower service fees](https://support.google.com/googleplay/android-developer/answer/16954621?hl=en)
15. [Play Console Help: Service fees](https://support.google.com/googleplay/android-developer/answer/112622?hl=en)
16. [Play Console Help: Frequently asked questions (Form 1099-K)](https://support.google.com/googleplay/android-developer/answer/7161649?hl=en)
17. [Google Payments Center Help: US tax information reporting and withholding](https://support.google.com/paymentscenter/answer/10349995?hl=en)
18. [Play Console Help: Tax rates and value-added tax (VAT)](https://support.google.com/googleplay/android-developer/answer/138000?hl=en)
19. [IRS: Understanding your Form 1099-K](https://www.irs.gov/businesses/understanding-your-form-1099-k)
20. [IRS: Form 1099-K FAQs, general information](https://www.irs.gov/newsroom/form-1099-k-faqs-general-information)
21. [IRS: What to do with Form 1099-K](https://www.irs.gov/businesses/what-to-do-with-form-1099-k)
22. [IRS Publication 538: Accounting Periods and Methods](https://www.irs.gov/publications/p538)
23. [IRS: Instructions for Schedule C (Form 1040)](https://www.irs.gov/instructions/i1040sc)
24. [Android Developers Blog: Expanded billing choice and lower fees on Google Play](https://android-developers.googleblog.com/2026/06/play-expanded-billing.html)

app-storegoogle-playapp-payouts1099-kindie-devdeveloper-taxes

This article is general information based on the author's experience. It is not licensed financial, legal, or tax advice. See the [editorial policy](https://soloopslab.com/editorial-policy).

## More in Money Ops

September 28, 2026

### [Business Insurance for Online Businesses: What to Buy or Skip](https://soloopslab.com/blog/business-insurance-online-business)

Six coverages mapped to creators, app makers and digital product sellers, with when to skip each one, the homeowners gap, and a pre-quote checklist.

September 28, 2026

### [Gumroad vs Lemon Squeezy vs Payhip Fees: Net at 5 Prices](https://soloopslab.com/blog/gumroad-vs-lemonsqueezy-vs-payhip)

What Gumroad, Lemon Squeezy and Payhip leave you on a $5 to $299 sale, from their official pricing pages, plus sales tax handling, payout timing and break-evens.

September 28, 2026

### [How to Pay Yourself as a Solopreneur: Draw, Salary, or Split](https://soloopslab.com/blog/pay-yourself-solopreneur)

Owner's draw, S corp salary plus distributions, or a fixed-percentage split: how each way to pay yourself works and what the IRS taxes, with every rule sourced.
