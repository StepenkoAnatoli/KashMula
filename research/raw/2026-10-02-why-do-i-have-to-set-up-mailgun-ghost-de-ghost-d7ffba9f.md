---
url: https://ghost.org/docs/faq/mailgun-newsletters/
retrieved: 2026-10-02
command: firecrawl scrape https://ghost.org/docs/faq/mailgun-newsletters/ --only-main-content --json
statusCode: 200
transport: firecrawl-cli
completeness: full
title: Why do I have to set up Mailgun? - Ghost Developer Docs
---
> ## Documentation Index
>
> Fetch the complete documentation index at: [/llms.txt](https://docs.ghost.org/llms.txt)
>
> Use this file to discover all available pages before exploring further.

[Skip to main content](https://docs.ghost.org/faq/mailgun-newsletters/#content-area)

* * *

**Transactional** email in Ghost can be configured to send with any SMTP, or another mail service that you prefer, using Ghost’s [standard](https://docs.ghost.org/config) configuration setup.**Bulk email** delivery for newsletters is a feature which requires a bulk mail API. Currently the only bulk mail API we support is Mailgun.If you _don’t_ want to deliver posts to members by email, you do not need a Mailgun account and you can safely ignore the email newsletter settings completely.

#### [​](https://docs.ghost.org/faq/mailgun-newsletters/\#why-can%E2%80%99t-i-just-use-smtp-mail-config-to-send-email-newsletters-with-ghost)  Why can’t I just use SMTP mail config to send email newsletters with Ghost?

Sending a bulk email to many recipients using basic SMTP will result in your IP address being instantly blacklisted and marked as spam by all mail providers. You should never send bulk mail using basic SMTP, which is why Ghost does not support it.More info [here](https://serversmtp.com/smtp-server-newsletter/), and [here](https://help.campaignmonitor.com/how-why-isps-block-emails), and [here](https://www.mailgun.com/blog/email-blasts-dos-donts-mass-email-sending/), and [here](https://webmasters.stackexchange.com/questions/19168/how-to-send-mass-email-and-not-get-treated-as-spam).

#### [​](https://docs.ghost.org/faq/mailgun-newsletters/\#i-still-want-to-use-a-different-provider-to-send-email-newsletters-why-can%E2%80%99t-i-do-that)  I still want to use a different provider to send email newsletters, why can’t I do that?

You can. There is no requirement to use Ghost’s built in newsletter delivery feature. Before we released this feature, thousands of people sent their newsletter using all sorts of other services such as Mailchimp, Sendgrid, Convertkit, and many others. You can sync your members database to an external newsletter provider via [Zapier](https://ghost.org/integrations/zapier/), or by following our [detailed integration guides](https://ghost.org/integrations/?tag=email).

#### [​](https://docs.ghost.org/faq/mailgun-newsletters/\#do-you-have-any-affiliation-with-mailgun-are-you-on-their-referral-program-or-something)  Do you have any affiliation with Mailgun? Are you on their referral program or something?

No. We have no partnership with Mailgun, we are not on their referral or affiliate program, they do not provide us with free service, and we do not benefit in any way (financial or otherwise) from people using them. We pay full-price for our own Mailgun account

#### [​](https://docs.ghost.org/faq/mailgun-newsletters/\#i-still-don%E2%80%99t-want-to-use-mailgun-can-you-support-something-else)  I still don’t want to use Mailgun, can you support something else?

No. We’re a small team with limited resources, and supporting multiple bulk-mail APIs is too much overhead for us to manage. We build and support Ghost on one clear stack that we know works reliably. We would rather have a product that can only be configured one way and works reliably, than being configured lots of different ways but is unreliable.

[Suggest edits](https://github.com/tryghost/docs/edit/main/faq/mailgun-newsletters.mdx) [Raise issue](https://github.com/tryghost/docs/issues/new?title=Issue%20on%20docs&body=Path:%20/faq/mailgun-newsletters)
