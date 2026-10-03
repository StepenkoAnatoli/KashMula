---
url: https://support.stripe.com/questions/physical-presence-requirement-faq
retrieved: 2026-10-03
command: firecrawl scrape https://support.stripe.com/questions/physical-presence-requirement-faq --only-main-content --json
statusCode: 200
transport: firecrawl-cli
completeness: full
title: Physical presence requirement FAQ : Stripe: Help & Support
---
- [What’s changing?](https://support.stripe.com/questions/physical-presence-requirement-faq#what-is-changing)
- [Why is Stripe making these changes?](https://support.stripe.com/questions/physical-presence-requirement-faq#why-make-these-changes)
- [How will screening impact Issuing, Treasury, and Opal users?](https://support.stripe.com/questions/physical-presence-requirement-faq#screening-impact-issuing-and-treasury-users)
- [Will this requirement impact access to other Stripe products?](https://support.stripe.com/questions/physical-presence-requirement-faq#impact-to-other-stripe-products)
- [How will this change impact Stripe Atlas users?](https://support.stripe.com/questions/physical-presence-requirement-faq#stripe-atlas-users)
- [What are physical mailbox and virtual address services?](https://support.stripe.com/questions/physical-presence-requirement-faq#mailbox-virtual-address-services)
- [What is a registered agent?](https://support.stripe.com/questions/physical-presence-requirement-faq#registered-agent)
- [Which account types will be screened?](https://support.stripe.com/questions/physical-presence-requirement-faq#screening)
- [Which address types will be screened?](https://support.stripe.com/questions/physical-presence-requirement-faq#address-screening)
- [How will Stripe determine if an address is from a registered agent, mailbox service or virtual address service?](https://support.stripe.com/questions/physical-presence-requirement-faq#how-does-stripe-screen)
- [What happens when an address is flagged?](https://support.stripe.com/questions/physical-presence-requirement-faq#flagged-address)

## What’s changing?

Starting July 1, 2025, Stripe requires that [Issuing](https://docs.stripe.com/issuing), [Treasury](https://docs.stripe.com/treasury), and Opal US-based accounts have a physical presence in the United States. Stripe will automatically screen Issuing, Treasury, and Opal US-based accounts to ensure they have a physical presence in the United States.

We no longer allow addresses associated with [mailbox services and virtual address services](https://support.stripe.com/questions/physical-presence-requirement-faq#mailbox-virtual-address-services) as a physical presence.

## Why is Stripe making these changes?

The partners we use to provide financial products in the United States require the businesses we support to have a physical presence—not just a mailing address—in the United States.

## How will screening impact Issuing, Treasury, and Opal users?

For existing accounts, we’ll complete a one-time screening of all accounts with Issuing, Treasury, or Opal capabilities on July 1, 2025.

For new accounts, we’ll complete screening whenever you request Issuing or Treasury capabilities for a connected account.

We’ll automatically screen addresses whenever you:

- Request Issuing or Treasury capabilities for a connected account
- Update an address for an account with Issuing, Treasury, or Opal capabilities

If we identify an address we can’t support, your attempt to add these capabilities will fail and we will share more details via email and the accounts.updated webhook.

## Will this requirement impact access to other Stripe products?

The physical presence requirement will only apply to US accounts with Issuing, Treasury, or Opal capabilities. While US accounts with business or account representative addresses associated with [registered agents](https://support.stripe.com/questions/physical-presence-requirement-faq#registered-agent), mailbox services, or virtual address services will no longer be able to access those capabilities, those accounts will still be able to use Stripe for payment processing and other products.

## How will this change impact Stripe Atlas users?

Because Delaware requires all companies formed in the state to have a registered agent for the specific purpose of receiving mail correspondence from the state, Stripe Atlas provides registered agent services for all companies formed on Atlas. This registered agent address doesn't serve as the company’s operating address or physical address.

All users enabling Issuing, Treasury, or Opal must provide evidence of a physical US address. For Atlas companies, this may be a personal address or the address where your company physically does business, but it can’t be your Atlas registered agent, nor can it be a mailbox or virtual address service.

For more information, see [Atlas-provided registered agents](https://docs.stripe.com/atlas/signup#agent-service) and [Managing your registered agent subscription](https://support.stripe.com/questions/managing-your-registered-agent-subscription).

## What are physical mailbox and virtual address services?

Mailbox services and virtual address services provide individuals or businesses with a real street address to receive mail and packages. Physical mailbox services offer in-person pickup, while virtual address services digitize incoming mail for online viewing, forwarding, or management. Addresses associated with physical mailbox services and virtual address services do not meet our requirements for US platforms using Issuing or Treasury, or US connected accounts with Issuing or Treasury capabilities.

## What is a registered agent?

A registered agent is a person or company authorized to receive official legal documents and government notices on behalf of a business, such as service of process. Addresses associated with registered agents don’t meet our requirements for US platforms using Issuing or Treasury, or US connected accounts with Issuing or Treasury capabilities.

## Which account types will be screened?

The screening will apply to both US platforms using Issuing or Treasury and US connected accounts with Issuing or Treasury capabilities.

## Which address types will be screened?

The screening will apply to the business address and account representative address associated with US Issuing, Treasury, and Opal accounts. These address types are used to assess eligibility for financial products.

Other individuals, such as beneficial owners who aren’t account representatives, will still be able to use an address associated with a registered agent, mailbox service, or virtual address service.

## How will Stripe determine if an address is from a registered agent, mailbox service, or virtual address service?

Stripe will screen business and account representative addresses against a proprietary list of addresses associated with registered agents, mailbox services and virtual address services. If an address you provided matches one on this list, we will notify you immediately via email and webhook with details about next steps.

## What happens when an address is flagged?

If an address is flagged, we will notify you immediately. You will be prompted to update the address to one that is not associated with a registered agent, mailbox service or virtual address service. If you believe an address was flagged in error, you will be able submit an appeal with supporting documents.

- **For new users**: your attempt to add Issuing or Treasury capabilities will fail and we will notify you immediately of the reason using the accounts.updated webhook.
- **For existing users**: if the flagged address is not updated or successfully appealed within 30 days, the account will no longer be able to access Issuing, Treasury, or Opal capabilities.

Did this answer your question?

Yes

No

## Related articles

[Which address should I use for Atlas incorporation?\\
\\
Different steps of your company setup have different address requirements. If you have a U.S. physical address You can use it everywhere — it works…](https://support.stripe.com/questions/which-address-should-i-use-for-atlas-incorporation)

[Atlas](https://support.stripe.com/topics/atlas)

[How can I forward my mail to my company address outside of the U.S.?\\
\\
If you are looking for an address to receive mail, we would recommend using a mail forwarding service. Atlas users can access discounts at two…](https://support.stripe.com/questions/how-can-i-forward-my-mail-to-my-company-address-outside-of-the-u-s)

[Atlas](https://support.stripe.com/topics/atlas)

[Get started with stablecoins using Stripe Treasury\\
\\
Treasury with a stablecoin balance is a business account built directly into your Stripe Dashboard, designed for entrepreneurs who operate across…](https://support.stripe.com/questions/get-started-with-stablecoins-using-stripe-treasury)

[Treasury](https://support.stripe.com/topics/treasury)

Popular topics

[Refunds](https://support.stripe.com/topics/refunds "Refunds")

[Treasury](https://support.stripe.com/topics/treasury "Treasury")

[Payments](https://support.stripe.com/topics/payments "Payments")

[Invoice](https://support.stripe.com/topics/invoice "Invoice")

[Disputes](https://support.stripe.com/topics/disputes "Disputes")

[Billing](https://support.stripe.com/topics/billing "Billing")

[Connect Tax Reporting](https://support.stripe.com/topics/connect-tax-reporting "Connect Tax Reporting")

[Privacy](https://support.stripe.com/topics/privacy "Privacy")

[Atlas](https://support.stripe.com/topics/atlas "Atlas")

[Payouts](https://support.stripe.com/topics/payouts "Payouts")

[Verification](https://support.stripe.com/topics/verification "Verification")

[Third-party integrations](https://support.stripe.com/topics/third-party-integrations "Third-party integrations")

[Connect](https://support.stripe.com/topics/connect "Connect")

[Account](https://support.stripe.com/topics/account "Account")

[Taxes](https://support.stripe.com/topics/taxes "Taxes")

[Getting started](https://support.stripe.com/topics/getting-started "Getting started")

Contact support

24×7 help from our support staff

Contact support

Live chat in English24/7 Support Available

Get email support in English 24/7

[Sign up to get support](https://dashboard.stripe.com/register?redirect=https%3A%2F%2Fsupport.stripe.com%2Fcontact)

[What is Stripe?](https://stripe.com/)

Learn more about Stripe and our products.

[Stripe docs](https://stripe.com/docs)

Get familiar with the Stripe products and their features.

[API reference](https://stripe.com/docs/api)

Explore complete reference documentation for the Stripe API.

[Developer chat on Discord](https://stripe.com/go/developer-chat)

Chat live with other developers on the official Stripe Discord.

English (United States)

Stripe will handle your data pursuant to our [privacy policy](https://stripe.com/privacy).© Stripe

Support Conversations Widget

StripeM-Inner

StripeM-Inner
