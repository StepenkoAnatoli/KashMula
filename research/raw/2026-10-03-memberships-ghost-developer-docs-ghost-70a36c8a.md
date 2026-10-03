---
url: https://docs.ghost.org/members/
retrieved: 2026-10-03
command: firecrawl scrape https://docs.ghost.org/members/ --only-main-content --json
statusCode: 200
transport: firecrawl-cli
completeness: full
title: Memberships - Ghost Developer Docs
---
> ## Documentation Index
>
> Fetch the complete documentation index at: [/llms.txt](https://docs.ghost.org/llms.txt)
>
> Use this file to discover all available pages before exploring further.

[Skip to main content](https://docs.ghost.org/members/#content-area)

* * *

## [​](https://docs.ghost.org/members/\#overview)  Overview

Any publisher who wants to offer a way for their audience to support their work can use the Members feature to share content, build an audience, and generate an income from a membership business.

![](https://mintcdn.com/ghost/KePyCzI5-bxtjueF/images/aa9afb93-ghost-sites_hud78661df9259815cb29707ecbfccff73_228853_1500x0_resize_q100_h2_box_3.webp?fit=max&auto=format&n=KePyCzI5-bxtjueF&q=85&s=41c0c777a04af6d23bb538962f328d9f)

The concepts and components that enable you to turn a Ghost site into a members publication are surprisingly simple and can be broken down into two concepts:

## [​](https://docs.ghost.org/members/\#1-memberships)  1\. Memberships

A member of a Ghost site is someone who has opted to subscribe, and confirmed their subscription by clicking the link sent to their inbox. Members are stored in Ghost, to make tracking, managing and supporting an audience a breeze.

### [​](https://docs.ghost.org/members/\#secure-authentication)  Secure authentication

Ghost uses passwordless JWT email-link based logins for your members. It’s fast, reliable, and incredible for security. Secure email authentication is used for both member sign up and sign in.

### [​](https://docs.ghost.org/members/\#access-levels)  Access levels

Once a visitor has entered their email address and confirmed membership, you can share protected content with them on your Ghost publication. Logged in members are able to access any content that matches their tier.The following access levels are available to select from the post settings in the editor:

- **Public**
- **Members only**
- **Paid-members only**
- **Specific tier(s)**

Content is securely protected at server level and there is no way to circumvent gated content without being a logged-in member.

### [​](https://docs.ghost.org/members/\#managing-members)  Managing members

Members are stored in Ghost with the following attributes:

- `email` (required)
- `name`
- `note`
- `subscribed_to_emails`
- `stripe_customer_id`
- `status` (free/paid/complimentary)
- `labels`
- `created_at`

### [​](https://docs.ghost.org/members/\#imports)  Imports

It’s possible to import Members from any other platform. If you have a list of email addresses, this can be ported into Ghost via CSV, Zapier, or the API.

## [​](https://docs.ghost.org/members/\#2-subscriptions)  2\. Subscriptions

Members in Ghost can be free members, or become paid members with a direct Stripe integration for fast, global payments.

### [​](https://docs.ghost.org/members/\#connect-to-stripe)  Connect to Stripe

We’ve built a direct [integration with Stripe](https://ghost.org/integrations/stripe/) which allows publishers to connect their Ghost site to their own billing account using Stripe Connect.

![](https://mintcdn.com/ghost/aGR3I5_lq1oxakuc/images/stripe-step-1.webp?fit=max&auto=format&n=aGR3I5_lq1oxakuc&q=85&s=5031e653ac90bf72c4dd1dcbfe508a3d)

Search "Tiers" or "Stripe" in your settings to find the Connect to Stripe button.

![](https://mintcdn.com/ghost/aGR3I5_lq1oxakuc/images/stripe-step-2.webp?fit=max&auto=format&n=aGR3I5_lq1oxakuc&q=85&s=cf0b313da9a874c3612139e25b49cb99)

Make sure you're signed up for a Stripe account.

![](https://mintcdn.com/ghost/aGR3I5_lq1oxakuc/images/stripe-step-3.webp?fit=max&auto=format&n=aGR3I5_lq1oxakuc&q=85&s=c33cb5c5f0805cd48eedf73724afca3b)

Follow the instructions to connect your Stripe account and generate your secure key.

Payments are handled by Stripe and billing information is stored securely inside your own Stripe account.

### [​](https://docs.ghost.org/members/\#transaction-fees)  Transaction fees

Ghost takes **0%** of your revenue. Whatever you generate from a paid blog, newsletter or community is yours to keep. Standard Stripe processing fees still apply.

### [​](https://docs.ghost.org/members/\#portability)  Portability

All membership, customer and business data is controlled by you. Your members list can be exported any time and since subscriptions and billing takes place inside your own Stripe account, you retain full ownership of it.If you’re migrating an existing membership business from another platform, check our our [migration docs](https://docs.ghost.org/migration).

### [​](https://docs.ghost.org/members/\#alternative-payment-gateways)  Alternative payment gateways

To begin with, Stripe is the only natively supported payment provider with Ghost. We’re aware that not everyone has access to Stripe, and we plan to add further payment providers in future.In the meantime, it is possible to create new members via an external provider, such as [Patreon](https://ghost.org/integrations/patreon/) or [PayPal](https://ghost.org/integrations/paypal/). You can set up any third party payments system and create members in Ghost via API, or using automation tools like Zapier.

### [​](https://docs.ghost.org/members/\#i-have-ideas-/-suggestions-/-problems-/-feedback)  I have ideas / suggestions / problems / feedback

Great! We set up a dedicated [forum category](https://forum.ghost.org/c/members) for feedback about the members feature, we appreciate your input!We’re continuously shipping improvements and new features at Ghost which you can follow over on [GitHub](https://github.com/tryghost/ghost), or on our [Changelog](https://ghost.org/changelog/).

[Suggest edits](https://github.com/tryghost/docs/edit/main/members.mdx) [Raise issue](https://github.com/tryghost/docs/issues/new?title=Issue%20on%20docs&body=Path:%20/members)
