---
url: https://docs.apify.com/api/v2/store-get
retrieved: 2026-10-03
command: firecrawl scrape https://docs.apify.com/api/v2/store-get --only-main-content --json
statusCode: 200
transport: firecrawl-cli
completeness: full
title: Get list of Actors in Store | Apify Documentation
---
[Skip to main content](https://docs.apify.com/api/v2/store-get#__docusaurus_skipToContent_fallback)

# Get list of Actors in Store

Copy for LLM

```
GET https://api.apify.com/v2/store
```

Gets the list of public Actors in Apify Store. You can use `search`
parameter to search Actors by string in title, name, description, username
and readme.
If you need detailed info about a specific Actor, use the [Get\\
Actor](https://docs.apify.com/api/v2/store-get#/reference/actors/actor-object/get-actor) endpoint.

The endpoint supports pagination using the `limit` and `offset` parameters.
It will not return more than 1,000 records.

## Request [Direct link to request](https://docs.apify.com/api/v2/store-get\#request)

### Query Parameters

**limit** double

Maximum number of items to return. The default value as well as the maximum is `1000`.

**Example:** `1000`

**offset** double

Number of items that should be skipped at the start. The default value is `0`.

**Example:** `0`

**search** string

String to search by. The search runs on the following fields: `title`,
`name`, `description`, `username`, `readme`.

**Example:** `web scraper`

**sortBy** string

Specifies the field by which to sort the results. The supported values
are `relevance` (default), `popularity`, `newest` and `lastUpdate`.

**Example:**`'popularity'`

**category** string

Filters the results by the specified category.

**Example:**`'AI'`

**username** string

Filters the results by the specified username.

**Example:**`'apify'`

**pricingModel** string

**Possible values:** \[`FREE`, `FLAT_PRICE_PER_MONTH`, `PRICE_PER_DATASET_ITEM`, `PAY_PER_EVENT`\]

Only return Actors with the specified pricing model.

**Example:** `FREE`

**allowsAgenticUsers** boolean

If true, only return Actors that allow agentic users. If false, only
return Actors that do not allow agentic users.

**Example:** `true`

**responseFormat** string

**Possible values:** \[`full`, `agent`\]

Controls the shape of the response. Use `full` (default) for the
complete response including image URLs and all fields. Use `agent`
for a reduced field set optimized for LLM consumers, which only
includes `id`, `title`, `name`, `username`, `description`, `notice`,
`badge`, `categories`, and minimal `stats`.

**Default value:** `full`

**Example:** `agent`

**includeUnrunnableActors** boolean

By default, search results exclude Actors that are not safe to run
automatically (e.g. Actors from developers who haven't passed KYC, or
full-permission Actors without a large user base). Set to `true` to
bypass this safety filtering and include all Actors in the results.

**Default value:** `false`

**Example:** `true`

## Responses [Direct link to Responses](https://docs.apify.com/api/v2/store-get\#responses)

- 200
- 400
- 401
- 405
- 429

### Status 200

**Response Headers**

- **X-Apify-Pagination-Offset**
The offset of the first item in the current page.

- **X-Apify-Pagination-Limit**
The maximum number of items returned per page.

- **X-Apify-Pagination-Count**
The number of items returned in the current page.

- **X-Apify-Pagination-Total**
The total number of items available.

- **X-Apify-Pagination-Desc**
Whether the items are sorted in descending order.


- application/json

- Example (auto)
- Schema

```json
{

  "data": {

    "total": 100,

    "offset": 0,

    "limit": 1000,

    "desc": false,

    "count": 1,

    "items": [\
\
      {\
\
        "id": "zdc3Pyhyz3m8vjDeM",\
\
        "title": "My Public Actor",\
\
        "name": "my-public-actor",\
\
        "username": "jane35",\
\
        "userFullName": "Jane Doe",\
\
        "description": "My public Actor!",\
\
        "pictureUrl": "https://...",\
\
        "userPictureUrl": "https://...",\
\
        "url": "https://...",\
\
        "stats": {\
\
          "totalBuilds": 9,\
\
          "totalRuns": 16,\
\
          "totalUsers": 6,\
\
          "totalUsers7Days": 2,\
\
          "totalUsers30Days": 6,\
\
          "totalUsers90Days": 6,\
\
          "totalMetamorphs": 2,\
\
          "lastRunStartedAt": "2019-07-08T14:01:05.546Z"\
\
        },\
\
        "currentPricingInfo": {\
\
          "pricingModel": "FREE"\
\
        },\
\
        "isWhiteListedForAgenticPayments": true\
\
      },\
\
      {\
\
        "id": "zdc3Pyhyz3m8vjDeM",\
\
        "title": "My Public Actor",\
\
        "name": "my-public-actor",\
\
        "username": "jane35",\
\
        "userFullName": "Jane H. Doe",\
\
        "categories": [\
\
          "MARKETING",\
\
          "LEAD_GENERATION"\
\
        ],\
\
        "description": "My public Actor!",\
\
        "pictureUrl": "https://...",\
\
        "userPictureUrl": "https://...",\
\
        "url": "https://...",\
\
        "stats": {\
\
          "totalBuilds": 9,\
\
          "totalRuns": 16,\
\
          "totalUsers": 6,\
\
          "totalUsers7Days": 2,\
\
          "totalUsers30Days": 6,\
\
          "totalUsers90Days": 6,\
\
          "totalMetamorphs": 2,\
\
          "lastRunStartedAt": "2019-07-08T14:01:05.546Z"\
\
        },\
\
        "currentPricingInfo": {\
\
          "pricingModel": "FREE"\
\
        },\
\
        "isWhiteListedForAgenticPayments": false\
\
      }\
\
    ]

  }

}
```

**Schema**

- **data** objectrequired







Common pagination fields for list responses.





  - **total** integerrequired
    The total number of items available across all pages.

    **Possible values:**`>= 0`


    **Example:** `1`
  - **offset** integerrequired
    The starting position for this page of results.

    **Possible values:**`>= 0`


    **Example:** `0`
  - **limit** integerrequired
    The maximum number of items returned per page.

    **Possible values:**`>= 1`


    **Example:** `1000`
  - **desc** booleanrequired
    Whether the results are sorted in descending order.


    **Example:** `false`
  - **count** integerrequired
    The number of items returned in this response.

    **Possible values:**`>= 0`


    **Example:** `1`
  - **items** object\[\]required









    - **id** stringrequired

      **Example:** `zdc3Pyhyz3m8vjDeM`
    - **title** stringrequired

      **Example:** `My Public Actor`
    - **name** stringrequired

      **Example:** `my-public-actor`
    - **username** stringrequired

      **Example:** `jane35`
    - **userFullName** string \| nullnullable

      **Example:** `Jane H. Doe`
    - **description** string \| nullnullable

      **Example:** `My public actor!`
    - **categories** string\[\]

      **Example:**`["MARKETING","LEAD_GENERATION"]`
    - **notice** ActorNotice (string,null)nullable
      A warning displayed on the Actor's page in Apify Store and Console. Can be set by the Actor's developer or automatically by Apify's quality checks.

      **Possible values:** \[`NONE`, `RESIDENTIAL_PROXY_REQUIRED`, `UNDER_MAINTENANCE`, `null`\]


      **Example:** `UNDER_MAINTENANCE`
    - **pictureUrl** string \| nullnullable

      **Example:** `https://...`
    - **userPictureUrl** string,null<uri>nullable

      **Example:** `https://...`
    - **url** string,null<uri>nullable

      **Example:** `https://...`
    - **stats** objectrequired







      Usage statistics and Apify Store metrics for the Actor.





      - **totalBuilds** integer
        The total number of builds of the Actor.


        **Example:** `9`
      - **totalRuns** integer
        The total number of runs of the Actor.


        **Example:** `16`
      - **totalUsers** integer
        The total number of Actor users, including its owner.


        **Example:** `6`
      - **totalUsers7Days** integer
        The number of active users of the Actor in the last 7 days.


        **Example:** `2`
      - **totalUsers30Days** integer
        The number of active users of the Actor in the last 30 days.


        **Example:** `6`
      - **totalUsers90Days** integer
        The number of active users of the Actor in the last 90 days.


        **Example:** `6`
      - **totalMetamorphs** integer
        The total number of times a run of another Actor was [metamorphed](https://docs.apify.com/platform/actors/development/programming-interface/metamorph) into this Actor.


        **Example:** `2`
      - **lastRunStartedAt** string<date-time>
        The date and time the most recent run of the Actor started.


        **Example:** `2019-07-08T14:01:05.546Z`
      - **actorReviewCount** integer
        The number of reviews the Actor has received in Apify Store.


        **Example:** `69`
      - **actorReviewRating** number
        The average rating of the Actor in Apify Store.


        **Example:** `4.7`
      - **bookmarkCount** integer
        The number of users who bookmarked the Actor in Apify Store.


        **Example:** `1269`
      - **publicActorRunStats30Days** object







        Run status counts from the last 30 days. Only for public Actors.
        Excludes runs started by the Actor's owner.





        - **ABORTED** integer
          The number of runs that were aborted.


          **Example:** `2542`
        - **FAILED** integer
          The number of runs that failed.


          **Example:** `1234`
        - **SUCCEEDED** integer
          The number of runs that succeeded.


          **Example:** `732805`
        - **TIMED-OUT** integer
          The number of runs that timed out.


          **Example:** `12556`
        - **TOTAL** integer
          The total number of runs.


          **Example:** `749137`

    - **currentPricingInfo** object





      - **pricingModel** stringrequired

        **Example:** `FREE`
      - **apifyMarginPercentage** number
        Apify's share of the revenue generated under this pricing info record, as a fraction between 0 and 1. Set by the Apify platform.


        **Example:** `0.2`
      - **createdAt** string<date-time>

        **Example:** `2023-01-01T00:00:00.000Z`
      - **startedAt** string<date-time>

        **Example:** `2023-01-01T00:00:00.000Z`
      - **notifiedAboutChangeAt** string,null<date-time>nullable

        **Example:** `null`
      - **notifiedAboutFutureChangeAt** string,null<date-time>nullable

        **Example:** `null`
      - **isPriceChangeNotificationSuppressed** boolean

        **Example:** `false`
      - **forceContainsSignificantPriceChange** boolean

        **Example:** `false`
      - **isPPEPlatformUsagePaidByUser** boolean

        **Example:** `false`
      - **reasonForChange** string \| nullnullable

        **Example:** `null`
      - **trialMinutes** integer \| nullnullable

        **Example:** `null`
      - **unitName** string \| nullnullable

        **Example:** `null`
      - **pricePerUnitUsd** number \| nullnullable

        **Example:** `null`
      - **minimalMaxTotalChargeUsd** number \| nullnullable

        **Example:** `0.5`
      - **pricingPerEvent** object,null







        Per-event pricing configuration for pay-per-event Actors.





        - **property name\*** anynullable
          Per-event pricing configuration for pay-per-event Actors.


    - **isWhiteListedForAgenticPayments** boolean \| nullnullable
      Whether the Actor is whitelisted for agentic payment processing.

    - **actorReviewCount** integer

      **Example:** `69`
    - **actorReviewRating** number

      **Example:** `4.7`
    - **bookmarkCount** integer

      **Example:** `1269`
    - **badge** string \| nullnullable

      **Example:** `null`
    - **readmeSummary** string
      A brief, LLM-generated readme summary


### Status 400

Bad request - invalid input parameters or request body.

- application/json

- Example
- Schema

```json
{

  "error": {

    "type": "invalid-input",

    "message": "Invalid input: The request body contains invalid data."

  }

}
```

**Schema**

- **error** objectrequired





  - **type** ErrorType (string)
    Machine-processable error type identifier.

    **Possible values:** \[`3d-secure-auth-failed`, `access-right-already-exists`, `action-not-found`, `actor-already-rented`, `actor-can-not-be-rented`, `actor-disabled`, `actor-is-not-rented`, `actor-memory-limit-exceeded`, `actor-name-exists-new-owner`, `actor-name-not-unique`, `actor-not-found`, `actor-not-github-actor`, `actor-not-public`, `actor-permission-level-not-supported-for-agentic-payments`, `actor-review-already-exists`, `actor-run-failed`, `actor-standby-not-supported-for-agentic-payments`, `actor-task-name-not-unique`, `agentic-payment-info-retrieval-error`, `agentic-payment-information-missing`, `agentic-payment-insufficient-amount`, `agentic-payment-provider-internal-error`, `agentic-payment-provider-unauthorized`, `airtable-webhook-deprecated`, `already-subscribed-to-paid-actor`, `apify-plan-required-to-use-paid-actor`, `apify-signup-not-allowed`, `auth-method-not-supported`, `authorization-server-not-found`, `auto-issue-date-invalid`, `background-check-required`, `billing-system-error`, `black-friday-plan-expired`, `braintree-error`, `braintree-not-linked`, `braintree-operation-timed-out`, `braintree-unsupported-currency`, `build-not-found`, `build-outdated`, `cannot-add-apify-events-to-ppe-actor`, `cannot-add-multiple-pricing-infos`, `cannot-add-pricing-info-that-alters-past`, `cannot-add-second-future-pricing-info`, `cannot-build-actor-from-webhook`, `cannot-change-billing-interval`, `cannot-change-owner`, `cannot-charge-apify-event`, `cannot-charge-non-pay-per-event-actor`, `cannot-comment-as-other-user`, `cannot-copy-actor-task`, `cannot-create-payout`, `cannot-create-public-actor`, `cannot-create-tax-transaction`, `cannot-delete-critical-actor`, `cannot-delete-invoice`, `cannot-delete-paid-actor`, `cannot-disable-one-time-event-for-apify-start-event`, `cannot-disable-organization-with-enabled-members`, `cannot-disable-user-with-subscription`, `cannot-link-oauth-to-unverified-email`, `cannot-metamorph-to-pay-per-result-actor`, `cannot-modify-actor-pricing-too-frequently`, `cannot-modify-actor-pricing-with-immediate-effect`, `cannot-monetize-without-payout-billing-info`, `cannot-override-paid-actor-trial`, `cannot-permanently-delete-subscription`, `cannot-publish-actor`, `cannot-publish-actor-task`, `cannot-reduce-last-full-token`, `cannot-reimburse-more-than-original-charge`, `cannot-reimburse-non-rental-charge`, `cannot-remove-own-actor-from-recently-used`, `cannot-remove-payment-method`, `cannot-remove-pricing-info`, `cannot-remove-running-run`, `cannot-remove-user-with-public-actors`, `cannot-remove-user-with-subscription`, `cannot-remove-user-with-unpaid-invoice`, `cannot-rename-env-var`, `cannot-rent-paid-actor`, `cannot-review-own-actor`, `cannot-set-access-rights-for-owner`, `cannot-set-is-status-message-terminal`, `cannot-unpublish-critical-actor`, `cannot-unpublish-paid-actor`, `cannot-unpublish-profile`, `cannot-update-invoice-field`, `concurrent-runs-limit-exceeded`, `concurrent-update-detected`, `conference-token-not-found`, `content-encoding-forbidden-for-html`, `coupon-already-redeemed`, `coupon-expired`, `coupon-for-new-customers`, `coupon-for-subscribed-users`, `coupon-limits-are-in-conflict-with-current-limits`, `coupon-max-number-of-redemptions-reached`, `coupon-not-found`, `coupon-not-unique`, `coupons-disabled`, `create-github-issue-not-allowed`, `creator-plan-not-available`, `cron-expression-invalid`, `daily-ai-token-limit-exceeded`, `daily-publication-limit-exceeded`, `dataset-does-not-have-fields-schema`, `dataset-does-not-have-schema`, `dataset-locked`, `dataset-schema-invalid`, `dcr-not-supported`, `default-dataset-not-found`, `deleting-default-build`, `deleting-unfinished-build`, `email-already-taken`, `email-already-taken-removed-user`, `email-domain-not-allowed-for-coupon`, `email-invalid`, `email-not-allowed`, `email-not-valid`, `email-update-too-soon`, `elevated-permissions-needed`, `env-var-already-exists`, `exchange-rate-fetch-failed`, `expired-conference-token`, `failed-to-charge-user`, `final-invoice-negative`, `full-permission-actor-blocked-for-admin`, `full-permission-actor-not-approved`, `github-branch-empty`, `github-issue-already-exists`, `github-public-key-not-found`, `github-repository-not-found`, `github-signature-does-not-match-payload`, `github-user-not-authorized-for-issues`, `gmail-not-allowed`, `id-does-not-match`, `incompatible-billing-interval`, `incomplete-payout-billing-info`, `inconsistent-currencies`, `incorrect-pricing-modifier-prefix`, `input-json-invalid-characters`, `input-json-not-object`, `input-json-too-long`, `input-update-collision`, `insufficient-permissions`, `insufficient-permissions-to-change-field`, `insufficient-security-measures`, `insufficient-tax-country-evidence`, `integration-auth-error`, `internal-server-error`, `invalid-billing-info`, `invalid-billing-period-for-payout`, `invalid-build`, `invalid-client-key`, `invalid-collection`, `invalid-conference-login-password`, `invalid-content-type-header`, `invalid-credentials`, `invalid-git-auth-token`, `invalid-github-issue-url`, `invalid-header`, `invalid-id`, `invalid-idempotency-key`, `invalid-input`, `invalid-input-schema`, `invalid-invoice`, `invalid-invoice-type`, `invalid-issue-date`, `invalid-label-params`, `invalid-main-account-user-id`, `invalid-oauth-app`, `invalid-oauth-scope`, `invalid-one-time-invoice`, `invalid-parameter`, `invalid-payout-status`, `invalid-picture-url`, `invalid-record-key`, `invalid-request`, `invalid-resource-type`, `invalid-signature`, `invalid-subscription-plan`, `invalid-tax-number`, `invalid-tax-number-format`, `invalid-token`, `invalid-token-type`, `invalid-two-factor-code`, `invalid-two-factor-code-or-recovery-code`, `invalid-two-factor-recovery-code`, `invalid-username`, `invalid-value`, `invitation-invalid-resource-type`, `invitation-no-longer-valid`, `invoice-canceled`, `invoice-cannot-be-refunded-due-to-too-high-amount`, `invoice-incomplete`, `invoice-is-draft`, `invoice-locked`, `invoice-must-be-buffer`, `invoice-not-canceled`, `invoice-not-draft`, `invoice-not-found`, `invoice-outdated`, `invoice-paid-already`, `issue-already-connected-to-github`, `issue-not-found`, `issues-bad-request`, `issuer-not-registered`, `job-finished`, `label-already-linked`, `last-api-token`, `limit-reached`, `max-items-must-be-greater-than-zero`, `max-metamorphs-exceeded`, `max-total-charge-usd-below-minimum`, `max-total-charge-usd-must-be-greater-than-zero`, `method-not-allowed`, `migration-disabled`, `missing-actor-rights`, `missing-api-token`, `missing-billing-info`, `missing-line-items`, `missing-payment-date`, `missing-payout-billing-info`, `missing-proxy-password`, `missing-reporting-fields`, `missing-resource-name`, `missing-settings`, `missing-username`, `monthly-usage-limit-too-low`, `more-than-one-update-not-allowed`, `multiple-records-found`, `must-be-admin`, `name-not-unique`, `next-runtime-computation-failed`, `no-columns-in-exported-dataset`, `no-payment-attempt-for-refund-found`, `no-payment-method-available`, `no-team-account-seats-available`, `non-temporary-email`, `not-enough-usage-to-run-paid-actor`, `not-implemented`, `not-supported-currencies`, `o-auth-service-already-connected`, `o-auth-service-not-connected`, `oauth-resource-access-failed`, `one-time-invoice-already-marked-paid`, `only-drafts-can-be-deleted`, `operation-canceled`, `operation-not-allowed`, `operation-timed-out`, `organization-cannot-own-itself`, `organization-role-not-found`, `overlapping-payout-billing-periods`, `own-token-required`, `page-not-found`, `param-not-one-of`, `parameter-required`, `parameters-mismatched`, `password-reset-email-already-sent`, `password-reset-token-expired`, `pay-as-you-go-without-monthly-interval`, `payment-attempt-status-message-required`, `payout-already-paid`, `payout-canceled`, `payout-invalid-state`, `payout-must-be-approved-to-be-marked-paid`, `payout-not-found`, `payout-number-already-exists`, `phone-number-invalid`, `phone-number-landline`, `phone-number-opted-out`, `phone-verification-disabled`, `platform-feature-disabled`, `price-overrides-validation-failed`, `pricing-model-not-supported`, `promotional-plan-not-available`, `proxy-auth-ip-not-unique`, `public-actor-disabled`, `query-timeout`, `quoted-price-outdated`, `rate-limit-exceeded`, `recaptcha-invalid`, `recaptcha-required`, `record-not-found`, `record-not-public`, `record-or-token-not-found`, `record-too-large`, `redirect-uri-mismatch`, `reduced-plan-not-available`, `rental-charge-already-reimbursed`, `rental-not-allowed`, `request-aborted-prematurely`, `request-handled-or-locked`, `request-id-invalid`, `request-queue-duplicate-requests`, `request-too-large`, `requested-dataset-view-does-not-exist`, `resume-token-expired`, `run-failed`, `run-input-body-not-valid-json`, `run-timeout-exceeded`, `russia-is-evil`, `same-user`, `schedule-actor-not-found`, `schedule-actor-task-not-found`, `schedule-name-not-unique`, `schema-validation`, `schema-validation-error`, `schema-validation-failed`, `service-worker-registration-not-allowed`, `sign-up-method-not-allowed`, `slack-integration-not-custom`, `socket-closed`, `socket-destroyed`, `store-schema-invalid`, `store-terms-not-accepted`, `stripe-enabled`, `stripe-generic-decline`, `stripe-not-enabled`, `stripe-not-enabled-for-user`, `tagged-build-required`, `tax-country-invalid`, `tax-number-invalid`, `tax-number-validation-failed`, `taxamo-call-failed`, `taxamo-request-failed`, `testing-error`, `token-not-provided`, `too-few-versions`, `too-many-actor-tasks`, `too-many-actors`, `too-many-labels-on-resource`, `too-many-mcp-connectors`, `too-many-o-auth-apps`, `too-many-organizations`, `too-many-requests`, `too-many-schedules`, `too-many-ui-access-keys`, `too-many-user-labels`, `too-many-values`, `too-many-versions`, `too-many-webhooks`, `unexpected-route`, `unknown-build-tag`, `unknown-payment-provider`, `unsubscribe-token-invalid`, `unsupported-actor-pricing-model-for-agentic-payments`, `unsupported-content-encoding`, `unsupported-file-type-for-issue`, `unsupported-file-type-image-expected`, `unsupported-file-type-text-or-json-expected`, `unsupported-permission`, `upcoming-subscription-bill-not-up-to-date`, `user-already-exists`, `user-already-verified`, `user-creates-organizations-too-fast`, `user-disabled`, `user-email-is-disposable`, `user-email-not-set`, `user-email-not-verified`, `user-has-no-subscription`, `user-integration-not-found`, `user-is-already-invited`, `user-is-already-organization-member`, `user-is-not-member-of-organization`, `user-is-not-organization`, `user-is-organization`, `user-is-organization-owner`, `user-is-removed`, `user-not-found`, `user-not-logged-in`, `user-not-verified`, `user-or-token-not-found`, `user-plan-not-allowed-for-coupon`, `user-problem-with-card`, `user-record-not-found`, `username-already-taken`, `username-missing`, `username-not-allowed`, `username-removal-forbidden`, `username-required`, `verification-email-already-sent`, `verification-token-expired`, `version-already-exists`, `versions-size-exceeded`, `weak-password`, `x402-agentic-payment-already-finalized`, `x402-agentic-payment-insufficient-amount`, `x402-agentic-payment-malformed-token`, `x402-agentic-payment-settlement-failed`, `x402-agentic-payment-settlement-in-progress`, `x402-agentic-payment-settlement-stuck`, `x402-agentic-payment-unauthorized`, `x402-payment-required`, `zero-invoice`\]

  - **message** string
    Human-readable error message describing what went wrong.


### Status 401

Unauthorized - authentication required or invalid token.

- application/json

- Example
- Schema

```json
{

  "error": {

    "type": "invalid-token",

    "message": "Authentication token is not valid."

  }

}
```

**Schema**

- **error** objectrequired





  - **type** ErrorType (string)
    Machine-processable error type identifier.

    **Possible values:** \[`3d-secure-auth-failed`, `access-right-already-exists`, `action-not-found`, `actor-already-rented`, `actor-can-not-be-rented`, `actor-disabled`, `actor-is-not-rented`, `actor-memory-limit-exceeded`, `actor-name-exists-new-owner`, `actor-name-not-unique`, `actor-not-found`, `actor-not-github-actor`, `actor-not-public`, `actor-permission-level-not-supported-for-agentic-payments`, `actor-review-already-exists`, `actor-run-failed`, `actor-standby-not-supported-for-agentic-payments`, `actor-task-name-not-unique`, `agentic-payment-info-retrieval-error`, `agentic-payment-information-missing`, `agentic-payment-insufficient-amount`, `agentic-payment-provider-internal-error`, `agentic-payment-provider-unauthorized`, `airtable-webhook-deprecated`, `already-subscribed-to-paid-actor`, `apify-plan-required-to-use-paid-actor`, `apify-signup-not-allowed`, `auth-method-not-supported`, `authorization-server-not-found`, `auto-issue-date-invalid`, `background-check-required`, `billing-system-error`, `black-friday-plan-expired`, `braintree-error`, `braintree-not-linked`, `braintree-operation-timed-out`, `braintree-unsupported-currency`, `build-not-found`, `build-outdated`, `cannot-add-apify-events-to-ppe-actor`, `cannot-add-multiple-pricing-infos`, `cannot-add-pricing-info-that-alters-past`, `cannot-add-second-future-pricing-info`, `cannot-build-actor-from-webhook`, `cannot-change-billing-interval`, `cannot-change-owner`, `cannot-charge-apify-event`, `cannot-charge-non-pay-per-event-actor`, `cannot-comment-as-other-user`, `cannot-copy-actor-task`, `cannot-create-payout`, `cannot-create-public-actor`, `cannot-create-tax-transaction`, `cannot-delete-critical-actor`, `cannot-delete-invoice`, `cannot-delete-paid-actor`, `cannot-disable-one-time-event-for-apify-start-event`, `cannot-disable-organization-with-enabled-members`, `cannot-disable-user-with-subscription`, `cannot-link-oauth-to-unverified-email`, `cannot-metamorph-to-pay-per-result-actor`, `cannot-modify-actor-pricing-too-frequently`, `cannot-modify-actor-pricing-with-immediate-effect`, `cannot-monetize-without-payout-billing-info`, `cannot-override-paid-actor-trial`, `cannot-permanently-delete-subscription`, `cannot-publish-actor`, `cannot-publish-actor-task`, `cannot-reduce-last-full-token`, `cannot-reimburse-more-than-original-charge`, `cannot-reimburse-non-rental-charge`, `cannot-remove-own-actor-from-recently-used`, `cannot-remove-payment-method`, `cannot-remove-pricing-info`, `cannot-remove-running-run`, `cannot-remove-user-with-public-actors`, `cannot-remove-user-with-subscription`, `cannot-remove-user-with-unpaid-invoice`, `cannot-rename-env-var`, `cannot-rent-paid-actor`, `cannot-review-own-actor`, `cannot-set-access-rights-for-owner`, `cannot-set-is-status-message-terminal`, `cannot-unpublish-critical-actor`, `cannot-unpublish-paid-actor`, `cannot-unpublish-profile`, `cannot-update-invoice-field`, `concurrent-runs-limit-exceeded`, `concurrent-update-detected`, `conference-token-not-found`, `content-encoding-forbidden-for-html`, `coupon-already-redeemed`, `coupon-expired`, `coupon-for-new-customers`, `coupon-for-subscribed-users`, `coupon-limits-are-in-conflict-with-current-limits`, `coupon-max-number-of-redemptions-reached`, `coupon-not-found`, `coupon-not-unique`, `coupons-disabled`, `create-github-issue-not-allowed`, `creator-plan-not-available`, `cron-expression-invalid`, `daily-ai-token-limit-exceeded`, `daily-publication-limit-exceeded`, `dataset-does-not-have-fields-schema`, `dataset-does-not-have-schema`, `dataset-locked`, `dataset-schema-invalid`, `dcr-not-supported`, `default-dataset-not-found`, `deleting-default-build`, `deleting-unfinished-build`, `email-already-taken`, `email-already-taken-removed-user`, `email-domain-not-allowed-for-coupon`, `email-invalid`, `email-not-allowed`, `email-not-valid`, `email-update-too-soon`, `elevated-permissions-needed`, `env-var-already-exists`, `exchange-rate-fetch-failed`, `expired-conference-token`, `failed-to-charge-user`, `final-invoice-negative`, `full-permission-actor-blocked-for-admin`, `full-permission-actor-not-approved`, `github-branch-empty`, `github-issue-already-exists`, `github-public-key-not-found`, `github-repository-not-found`, `github-signature-does-not-match-payload`, `github-user-not-authorized-for-issues`, `gmail-not-allowed`, `id-does-not-match`, `incompatible-billing-interval`, `incomplete-payout-billing-info`, `inconsistent-currencies`, `incorrect-pricing-modifier-prefix`, `input-json-invalid-characters`, `input-json-not-object`, `input-json-too-long`, `input-update-collision`, `insufficient-permissions`, `insufficient-permissions-to-change-field`, `insufficient-security-measures`, `insufficient-tax-country-evidence`, `integration-auth-error`, `internal-server-error`, `invalid-billing-info`, `invalid-billing-period-for-payout`, `invalid-build`, `invalid-client-key`, `invalid-collection`, `invalid-conference-login-password`, `invalid-content-type-header`, `invalid-credentials`, `invalid-git-auth-token`, `invalid-github-issue-url`, `invalid-header`, `invalid-id`, `invalid-idempotency-key`, `invalid-input`, `invalid-input-schema`, `invalid-invoice`, `invalid-invoice-type`, `invalid-issue-date`, `invalid-label-params`, `invalid-main-account-user-id`, `invalid-oauth-app`, `invalid-oauth-scope`, `invalid-one-time-invoice`, `invalid-parameter`, `invalid-payout-status`, `invalid-picture-url`, `invalid-record-key`, `invalid-request`, `invalid-resource-type`, `invalid-signature`, `invalid-subscription-plan`, `invalid-tax-number`, `invalid-tax-number-format`, `invalid-token`, `invalid-token-type`, `invalid-two-factor-code`, `invalid-two-factor-code-or-recovery-code`, `invalid-two-factor-recovery-code`, `invalid-username`, `invalid-value`, `invitation-invalid-resource-type`, `invitation-no-longer-valid`, `invoice-canceled`, `invoice-cannot-be-refunded-due-to-too-high-amount`, `invoice-incomplete`, `invoice-is-draft`, `invoice-locked`, `invoice-must-be-buffer`, `invoice-not-canceled`, `invoice-not-draft`, `invoice-not-found`, `invoice-outdated`, `invoice-paid-already`, `issue-already-connected-to-github`, `issue-not-found`, `issues-bad-request`, `issuer-not-registered`, `job-finished`, `label-already-linked`, `last-api-token`, `limit-reached`, `max-items-must-be-greater-than-zero`, `max-metamorphs-exceeded`, `max-total-charge-usd-below-minimum`, `max-total-charge-usd-must-be-greater-than-zero`, `method-not-allowed`, `migration-disabled`, `missing-actor-rights`, `missing-api-token`, `missing-billing-info`, `missing-line-items`, `missing-payment-date`, `missing-payout-billing-info`, `missing-proxy-password`, `missing-reporting-fields`, `missing-resource-name`, `missing-settings`, `missing-username`, `monthly-usage-limit-too-low`, `more-than-one-update-not-allowed`, `multiple-records-found`, `must-be-admin`, `name-not-unique`, `next-runtime-computation-failed`, `no-columns-in-exported-dataset`, `no-payment-attempt-for-refund-found`, `no-payment-method-available`, `no-team-account-seats-available`, `non-temporary-email`, `not-enough-usage-to-run-paid-actor`, `not-implemented`, `not-supported-currencies`, `o-auth-service-already-connected`, `o-auth-service-not-connected`, `oauth-resource-access-failed`, `one-time-invoice-already-marked-paid`, `only-drafts-can-be-deleted`, `operation-canceled`, `operation-not-allowed`, `operation-timed-out`, `organization-cannot-own-itself`, `organization-role-not-found`, `overlapping-payout-billing-periods`, `own-token-required`, `page-not-found`, `param-not-one-of`, `parameter-required`, `parameters-mismatched`, `password-reset-email-already-sent`, `password-reset-token-expired`, `pay-as-you-go-without-monthly-interval`, `payment-attempt-status-message-required`, `payout-already-paid`, `payout-canceled`, `payout-invalid-state`, `payout-must-be-approved-to-be-marked-paid`, `payout-not-found`, `payout-number-already-exists`, `phone-number-invalid`, `phone-number-landline`, `phone-number-opted-out`, `phone-verification-disabled`, `platform-feature-disabled`, `price-overrides-validation-failed`, `pricing-model-not-supported`, `promotional-plan-not-available`, `proxy-auth-ip-not-unique`, `public-actor-disabled`, `query-timeout`, `quoted-price-outdated`, `rate-limit-exceeded`, `recaptcha-invalid`, `recaptcha-required`, `record-not-found`, `record-not-public`, `record-or-token-not-found`, `record-too-large`, `redirect-uri-mismatch`, `reduced-plan-not-available`, `rental-charge-already-reimbursed`, `rental-not-allowed`, `request-aborted-prematurely`, `request-handled-or-locked`, `request-id-invalid`, `request-queue-duplicate-requests`, `request-too-large`, `requested-dataset-view-does-not-exist`, `resume-token-expired`, `run-failed`, `run-input-body-not-valid-json`, `run-timeout-exceeded`, `russia-is-evil`, `same-user`, `schedule-actor-not-found`, `schedule-actor-task-not-found`, `schedule-name-not-unique`, `schema-validation`, `schema-validation-error`, `schema-validation-failed`, `service-worker-registration-not-allowed`, `sign-up-method-not-allowed`, `slack-integration-not-custom`, `socket-closed`, `socket-destroyed`, `store-schema-invalid`, `store-terms-not-accepted`, `stripe-enabled`, `stripe-generic-decline`, `stripe-not-enabled`, `stripe-not-enabled-for-user`, `tagged-build-required`, `tax-country-invalid`, `tax-number-invalid`, `tax-number-validation-failed`, `taxamo-call-failed`, `taxamo-request-failed`, `testing-error`, `token-not-provided`, `too-few-versions`, `too-many-actor-tasks`, `too-many-actors`, `too-many-labels-on-resource`, `too-many-mcp-connectors`, `too-many-o-auth-apps`, `too-many-organizations`, `too-many-requests`, `too-many-schedules`, `too-many-ui-access-keys`, `too-many-user-labels`, `too-many-values`, `too-many-versions`, `too-many-webhooks`, `unexpected-route`, `unknown-build-tag`, `unknown-payment-provider`, `unsubscribe-token-invalid`, `unsupported-actor-pricing-model-for-agentic-payments`, `unsupported-content-encoding`, `unsupported-file-type-for-issue`, `unsupported-file-type-image-expected`, `unsupported-file-type-text-or-json-expected`, `unsupported-permission`, `upcoming-subscription-bill-not-up-to-date`, `user-already-exists`, `user-already-verified`, `user-creates-organizations-too-fast`, `user-disabled`, `user-email-is-disposable`, `user-email-not-set`, `user-email-not-verified`, `user-has-no-subscription`, `user-integration-not-found`, `user-is-already-invited`, `user-is-already-organization-member`, `user-is-not-member-of-organization`, `user-is-not-organization`, `user-is-organization`, `user-is-organization-owner`, `user-is-removed`, `user-not-found`, `user-not-logged-in`, `user-not-verified`, `user-or-token-not-found`, `user-plan-not-allowed-for-coupon`, `user-problem-with-card`, `user-record-not-found`, `username-already-taken`, `username-missing`, `username-not-allowed`, `username-removal-forbidden`, `username-required`, `verification-email-already-sent`, `verification-token-expired`, `version-already-exists`, `versions-size-exceeded`, `weak-password`, `x402-agentic-payment-already-finalized`, `x402-agentic-payment-insufficient-amount`, `x402-agentic-payment-malformed-token`, `x402-agentic-payment-settlement-failed`, `x402-agentic-payment-settlement-in-progress`, `x402-agentic-payment-settlement-stuck`, `x402-agentic-payment-unauthorized`, `x402-payment-required`, `zero-invoice`\]

  - **message** string
    Human-readable error message describing what went wrong.


### Status 405

Method not allowed.

- application/json

- Example
- Schema

```json
{

  "error": {

    "type": "method-not-allowed",

    "message": "This API end-point can only be accessed using the following HTTP methods: OPTIONS,GET"

  }

}
```

**Schema**

- **error** objectrequired





  - **type** ErrorType (string)
    Machine-processable error type identifier.

    **Possible values:** \[`3d-secure-auth-failed`, `access-right-already-exists`, `action-not-found`, `actor-already-rented`, `actor-can-not-be-rented`, `actor-disabled`, `actor-is-not-rented`, `actor-memory-limit-exceeded`, `actor-name-exists-new-owner`, `actor-name-not-unique`, `actor-not-found`, `actor-not-github-actor`, `actor-not-public`, `actor-permission-level-not-supported-for-agentic-payments`, `actor-review-already-exists`, `actor-run-failed`, `actor-standby-not-supported-for-agentic-payments`, `actor-task-name-not-unique`, `agentic-payment-info-retrieval-error`, `agentic-payment-information-missing`, `agentic-payment-insufficient-amount`, `agentic-payment-provider-internal-error`, `agentic-payment-provider-unauthorized`, `airtable-webhook-deprecated`, `already-subscribed-to-paid-actor`, `apify-plan-required-to-use-paid-actor`, `apify-signup-not-allowed`, `auth-method-not-supported`, `authorization-server-not-found`, `auto-issue-date-invalid`, `background-check-required`, `billing-system-error`, `black-friday-plan-expired`, `braintree-error`, `braintree-not-linked`, `braintree-operation-timed-out`, `braintree-unsupported-currency`, `build-not-found`, `build-outdated`, `cannot-add-apify-events-to-ppe-actor`, `cannot-add-multiple-pricing-infos`, `cannot-add-pricing-info-that-alters-past`, `cannot-add-second-future-pricing-info`, `cannot-build-actor-from-webhook`, `cannot-change-billing-interval`, `cannot-change-owner`, `cannot-charge-apify-event`, `cannot-charge-non-pay-per-event-actor`, `cannot-comment-as-other-user`, `cannot-copy-actor-task`, `cannot-create-payout`, `cannot-create-public-actor`, `cannot-create-tax-transaction`, `cannot-delete-critical-actor`, `cannot-delete-invoice`, `cannot-delete-paid-actor`, `cannot-disable-one-time-event-for-apify-start-event`, `cannot-disable-organization-with-enabled-members`, `cannot-disable-user-with-subscription`, `cannot-link-oauth-to-unverified-email`, `cannot-metamorph-to-pay-per-result-actor`, `cannot-modify-actor-pricing-too-frequently`, `cannot-modify-actor-pricing-with-immediate-effect`, `cannot-monetize-without-payout-billing-info`, `cannot-override-paid-actor-trial`, `cannot-permanently-delete-subscription`, `cannot-publish-actor`, `cannot-publish-actor-task`, `cannot-reduce-last-full-token`, `cannot-reimburse-more-than-original-charge`, `cannot-reimburse-non-rental-charge`, `cannot-remove-own-actor-from-recently-used`, `cannot-remove-payment-method`, `cannot-remove-pricing-info`, `cannot-remove-running-run`, `cannot-remove-user-with-public-actors`, `cannot-remove-user-with-subscription`, `cannot-remove-user-with-unpaid-invoice`, `cannot-rename-env-var`, `cannot-rent-paid-actor`, `cannot-review-own-actor`, `cannot-set-access-rights-for-owner`, `cannot-set-is-status-message-terminal`, `cannot-unpublish-critical-actor`, `cannot-unpublish-paid-actor`, `cannot-unpublish-profile`, `cannot-update-invoice-field`, `concurrent-runs-limit-exceeded`, `concurrent-update-detected`, `conference-token-not-found`, `content-encoding-forbidden-for-html`, `coupon-already-redeemed`, `coupon-expired`, `coupon-for-new-customers`, `coupon-for-subscribed-users`, `coupon-limits-are-in-conflict-with-current-limits`, `coupon-max-number-of-redemptions-reached`, `coupon-not-found`, `coupon-not-unique`, `coupons-disabled`, `create-github-issue-not-allowed`, `creator-plan-not-available`, `cron-expression-invalid`, `daily-ai-token-limit-exceeded`, `daily-publication-limit-exceeded`, `dataset-does-not-have-fields-schema`, `dataset-does-not-have-schema`, `dataset-locked`, `dataset-schema-invalid`, `dcr-not-supported`, `default-dataset-not-found`, `deleting-default-build`, `deleting-unfinished-build`, `email-already-taken`, `email-already-taken-removed-user`, `email-domain-not-allowed-for-coupon`, `email-invalid`, `email-not-allowed`, `email-not-valid`, `email-update-too-soon`, `elevated-permissions-needed`, `env-var-already-exists`, `exchange-rate-fetch-failed`, `expired-conference-token`, `failed-to-charge-user`, `final-invoice-negative`, `full-permission-actor-blocked-for-admin`, `full-permission-actor-not-approved`, `github-branch-empty`, `github-issue-already-exists`, `github-public-key-not-found`, `github-repository-not-found`, `github-signature-does-not-match-payload`, `github-user-not-authorized-for-issues`, `gmail-not-allowed`, `id-does-not-match`, `incompatible-billing-interval`, `incomplete-payout-billing-info`, `inconsistent-currencies`, `incorrect-pricing-modifier-prefix`, `input-json-invalid-characters`, `input-json-not-object`, `input-json-too-long`, `input-update-collision`, `insufficient-permissions`, `insufficient-permissions-to-change-field`, `insufficient-security-measures`, `insufficient-tax-country-evidence`, `integration-auth-error`, `internal-server-error`, `invalid-billing-info`, `invalid-billing-period-for-payout`, `invalid-build`, `invalid-client-key`, `invalid-collection`, `invalid-conference-login-password`, `invalid-content-type-header`, `invalid-credentials`, `invalid-git-auth-token`, `invalid-github-issue-url`, `invalid-header`, `invalid-id`, `invalid-idempotency-key`, `invalid-input`, `invalid-input-schema`, `invalid-invoice`, `invalid-invoice-type`, `invalid-issue-date`, `invalid-label-params`, `invalid-main-account-user-id`, `invalid-oauth-app`, `invalid-oauth-scope`, `invalid-one-time-invoice`, `invalid-parameter`, `invalid-payout-status`, `invalid-picture-url`, `invalid-record-key`, `invalid-request`, `invalid-resource-type`, `invalid-signature`, `invalid-subscription-plan`, `invalid-tax-number`, `invalid-tax-number-format`, `invalid-token`, `invalid-token-type`, `invalid-two-factor-code`, `invalid-two-factor-code-or-recovery-code`, `invalid-two-factor-recovery-code`, `invalid-username`, `invalid-value`, `invitation-invalid-resource-type`, `invitation-no-longer-valid`, `invoice-canceled`, `invoice-cannot-be-refunded-due-to-too-high-amount`, `invoice-incomplete`, `invoice-is-draft`, `invoice-locked`, `invoice-must-be-buffer`, `invoice-not-canceled`, `invoice-not-draft`, `invoice-not-found`, `invoice-outdated`, `invoice-paid-already`, `issue-already-connected-to-github`, `issue-not-found`, `issues-bad-request`, `issuer-not-registered`, `job-finished`, `label-already-linked`, `last-api-token`, `limit-reached`, `max-items-must-be-greater-than-zero`, `max-metamorphs-exceeded`, `max-total-charge-usd-below-minimum`, `max-total-charge-usd-must-be-greater-than-zero`, `method-not-allowed`, `migration-disabled`, `missing-actor-rights`, `missing-api-token`, `missing-billing-info`, `missing-line-items`, `missing-payment-date`, `missing-payout-billing-info`, `missing-proxy-password`, `missing-reporting-fields`, `missing-resource-name`, `missing-settings`, `missing-username`, `monthly-usage-limit-too-low`, `more-than-one-update-not-allowed`, `multiple-records-found`, `must-be-admin`, `name-not-unique`, `next-runtime-computation-failed`, `no-columns-in-exported-dataset`, `no-payment-attempt-for-refund-found`, `no-payment-method-available`, `no-team-account-seats-available`, `non-temporary-email`, `not-enough-usage-to-run-paid-actor`, `not-implemented`, `not-supported-currencies`, `o-auth-service-already-connected`, `o-auth-service-not-connected`, `oauth-resource-access-failed`, `one-time-invoice-already-marked-paid`, `only-drafts-can-be-deleted`, `operation-canceled`, `operation-not-allowed`, `operation-timed-out`, `organization-cannot-own-itself`, `organization-role-not-found`, `overlapping-payout-billing-periods`, `own-token-required`, `page-not-found`, `param-not-one-of`, `parameter-required`, `parameters-mismatched`, `password-reset-email-already-sent`, `password-reset-token-expired`, `pay-as-you-go-without-monthly-interval`, `payment-attempt-status-message-required`, `payout-already-paid`, `payout-canceled`, `payout-invalid-state`, `payout-must-be-approved-to-be-marked-paid`, `payout-not-found`, `payout-number-already-exists`, `phone-number-invalid`, `phone-number-landline`, `phone-number-opted-out`, `phone-verification-disabled`, `platform-feature-disabled`, `price-overrides-validation-failed`, `pricing-model-not-supported`, `promotional-plan-not-available`, `proxy-auth-ip-not-unique`, `public-actor-disabled`, `query-timeout`, `quoted-price-outdated`, `rate-limit-exceeded`, `recaptcha-invalid`, `recaptcha-required`, `record-not-found`, `record-not-public`, `record-or-token-not-found`, `record-too-large`, `redirect-uri-mismatch`, `reduced-plan-not-available`, `rental-charge-already-reimbursed`, `rental-not-allowed`, `request-aborted-prematurely`, `request-handled-or-locked`, `request-id-invalid`, `request-queue-duplicate-requests`, `request-too-large`, `requested-dataset-view-does-not-exist`, `resume-token-expired`, `run-failed`, `run-input-body-not-valid-json`, `run-timeout-exceeded`, `russia-is-evil`, `same-user`, `schedule-actor-not-found`, `schedule-actor-task-not-found`, `schedule-name-not-unique`, `schema-validation`, `schema-validation-error`, `schema-validation-failed`, `service-worker-registration-not-allowed`, `sign-up-method-not-allowed`, `slack-integration-not-custom`, `socket-closed`, `socket-destroyed`, `store-schema-invalid`, `store-terms-not-accepted`, `stripe-enabled`, `stripe-generic-decline`, `stripe-not-enabled`, `stripe-not-enabled-for-user`, `tagged-build-required`, `tax-country-invalid`, `tax-number-invalid`, `tax-number-validation-failed`, `taxamo-call-failed`, `taxamo-request-failed`, `testing-error`, `token-not-provided`, `too-few-versions`, `too-many-actor-tasks`, `too-many-actors`, `too-many-labels-on-resource`, `too-many-mcp-connectors`, `too-many-o-auth-apps`, `too-many-organizations`, `too-many-requests`, `too-many-schedules`, `too-many-ui-access-keys`, `too-many-user-labels`, `too-many-values`, `too-many-versions`, `too-many-webhooks`, `unexpected-route`, `unknown-build-tag`, `unknown-payment-provider`, `unsubscribe-token-invalid`, `unsupported-actor-pricing-model-for-agentic-payments`, `unsupported-content-encoding`, `unsupported-file-type-for-issue`, `unsupported-file-type-image-expected`, `unsupported-file-type-text-or-json-expected`, `unsupported-permission`, `upcoming-subscription-bill-not-up-to-date`, `user-already-exists`, `user-already-verified`, `user-creates-organizations-too-fast`, `user-disabled`, `user-email-is-disposable`, `user-email-not-set`, `user-email-not-verified`, `user-has-no-subscription`, `user-integration-not-found`, `user-is-already-invited`, `user-is-already-organization-member`, `user-is-not-member-of-organization`, `user-is-not-organization`, `user-is-organization`, `user-is-organization-owner`, `user-is-removed`, `user-not-found`, `user-not-logged-in`, `user-not-verified`, `user-or-token-not-found`, `user-plan-not-allowed-for-coupon`, `user-problem-with-card`, `user-record-not-found`, `username-already-taken`, `username-missing`, `username-not-allowed`, `username-removal-forbidden`, `username-required`, `verification-email-already-sent`, `verification-token-expired`, `version-already-exists`, `versions-size-exceeded`, `weak-password`, `x402-agentic-payment-already-finalized`, `x402-agentic-payment-insufficient-amount`, `x402-agentic-payment-malformed-token`, `x402-agentic-payment-settlement-failed`, `x402-agentic-payment-settlement-in-progress`, `x402-agentic-payment-settlement-stuck`, `x402-agentic-payment-unauthorized`, `x402-payment-required`, `zero-invoice`\]

  - **message** string
    Human-readable error message describing what went wrong.


### Status 429

Too many requests - rate limit exceeded.

- application/json

- Example
- Schema

```json
{

  "error": {

    "type": "rate-limit-exceeded",

    "message": "You have exceeded the rate limit. Please try again later."

  }

}
```

**Schema**

- **error** objectrequired





  - **type** ErrorType (string)
    Machine-processable error type identifier.

    **Possible values:** \[`3d-secure-auth-failed`, `access-right-already-exists`, `action-not-found`, `actor-already-rented`, `actor-can-not-be-rented`, `actor-disabled`, `actor-is-not-rented`, `actor-memory-limit-exceeded`, `actor-name-exists-new-owner`, `actor-name-not-unique`, `actor-not-found`, `actor-not-github-actor`, `actor-not-public`, `actor-permission-level-not-supported-for-agentic-payments`, `actor-review-already-exists`, `actor-run-failed`, `actor-standby-not-supported-for-agentic-payments`, `actor-task-name-not-unique`, `agentic-payment-info-retrieval-error`, `agentic-payment-information-missing`, `agentic-payment-insufficient-amount`, `agentic-payment-provider-internal-error`, `agentic-payment-provider-unauthorized`, `airtable-webhook-deprecated`, `already-subscribed-to-paid-actor`, `apify-plan-required-to-use-paid-actor`, `apify-signup-not-allowed`, `auth-method-not-supported`, `authorization-server-not-found`, `auto-issue-date-invalid`, `background-check-required`, `billing-system-error`, `black-friday-plan-expired`, `braintree-error`, `braintree-not-linked`, `braintree-operation-timed-out`, `braintree-unsupported-currency`, `build-not-found`, `build-outdated`, `cannot-add-apify-events-to-ppe-actor`, `cannot-add-multiple-pricing-infos`, `cannot-add-pricing-info-that-alters-past`, `cannot-add-second-future-pricing-info`, `cannot-build-actor-from-webhook`, `cannot-change-billing-interval`, `cannot-change-owner`, `cannot-charge-apify-event`, `cannot-charge-non-pay-per-event-actor`, `cannot-comment-as-other-user`, `cannot-copy-actor-task`, `cannot-create-payout`, `cannot-create-public-actor`, `cannot-create-tax-transaction`, `cannot-delete-critical-actor`, `cannot-delete-invoice`, `cannot-delete-paid-actor`, `cannot-disable-one-time-event-for-apify-start-event`, `cannot-disable-organization-with-enabled-members`, `cannot-disable-user-with-subscription`, `cannot-link-oauth-to-unverified-email`, `cannot-metamorph-to-pay-per-result-actor`, `cannot-modify-actor-pricing-too-frequently`, `cannot-modify-actor-pricing-with-immediate-effect`, `cannot-monetize-without-payout-billing-info`, `cannot-override-paid-actor-trial`, `cannot-permanently-delete-subscription`, `cannot-publish-actor`, `cannot-publish-actor-task`, `cannot-reduce-last-full-token`, `cannot-reimburse-more-than-original-charge`, `cannot-reimburse-non-rental-charge`, `cannot-remove-own-actor-from-recently-used`, `cannot-remove-payment-method`, `cannot-remove-pricing-info`, `cannot-remove-running-run`, `cannot-remove-user-with-public-actors`, `cannot-remove-user-with-subscription`, `cannot-remove-user-with-unpaid-invoice`, `cannot-rename-env-var`, `cannot-rent-paid-actor`, `cannot-review-own-actor`, `cannot-set-access-rights-for-owner`, `cannot-set-is-status-message-terminal`, `cannot-unpublish-critical-actor`, `cannot-unpublish-paid-actor`, `cannot-unpublish-profile`, `cannot-update-invoice-field`, `concurrent-runs-limit-exceeded`, `concurrent-update-detected`, `conference-token-not-found`, `content-encoding-forbidden-for-html`, `coupon-already-redeemed`, `coupon-expired`, `coupon-for-new-customers`, `coupon-for-subscribed-users`, `coupon-limits-are-in-conflict-with-current-limits`, `coupon-max-number-of-redemptions-reached`, `coupon-not-found`, `coupon-not-unique`, `coupons-disabled`, `create-github-issue-not-allowed`, `creator-plan-not-available`, `cron-expression-invalid`, `daily-ai-token-limit-exceeded`, `daily-publication-limit-exceeded`, `dataset-does-not-have-fields-schema`, `dataset-does-not-have-schema`, `dataset-locked`, `dataset-schema-invalid`, `dcr-not-supported`, `default-dataset-not-found`, `deleting-default-build`, `deleting-unfinished-build`, `email-already-taken`, `email-already-taken-removed-user`, `email-domain-not-allowed-for-coupon`, `email-invalid`, `email-not-allowed`, `email-not-valid`, `email-update-too-soon`, `elevated-permissions-needed`, `env-var-already-exists`, `exchange-rate-fetch-failed`, `expired-conference-token`, `failed-to-charge-user`, `final-invoice-negative`, `full-permission-actor-blocked-for-admin`, `full-permission-actor-not-approved`, `github-branch-empty`, `github-issue-already-exists`, `github-public-key-not-found`, `github-repository-not-found`, `github-signature-does-not-match-payload`, `github-user-not-authorized-for-issues`, `gmail-not-allowed`, `id-does-not-match`, `incompatible-billing-interval`, `incomplete-payout-billing-info`, `inconsistent-currencies`, `incorrect-pricing-modifier-prefix`, `input-json-invalid-characters`, `input-json-not-object`, `input-json-too-long`, `input-update-collision`, `insufficient-permissions`, `insufficient-permissions-to-change-field`, `insufficient-security-measures`, `insufficient-tax-country-evidence`, `integration-auth-error`, `internal-server-error`, `invalid-billing-info`, `invalid-billing-period-for-payout`, `invalid-build`, `invalid-client-key`, `invalid-collection`, `invalid-conference-login-password`, `invalid-content-type-header`, `invalid-credentials`, `invalid-git-auth-token`, `invalid-github-issue-url`, `invalid-header`, `invalid-id`, `invalid-idempotency-key`, `invalid-input`, `invalid-input-schema`, `invalid-invoice`, `invalid-invoice-type`, `invalid-issue-date`, `invalid-label-params`, `invalid-main-account-user-id`, `invalid-oauth-app`, `invalid-oauth-scope`, `invalid-one-time-invoice`, `invalid-parameter`, `invalid-payout-status`, `invalid-picture-url`, `invalid-record-key`, `invalid-request`, `invalid-resource-type`, `invalid-signature`, `invalid-subscription-plan`, `invalid-tax-number`, `invalid-tax-number-format`, `invalid-token`, `invalid-token-type`, `invalid-two-factor-code`, `invalid-two-factor-code-or-recovery-code`, `invalid-two-factor-recovery-code`, `invalid-username`, `invalid-value`, `invitation-invalid-resource-type`, `invitation-no-longer-valid`, `invoice-canceled`, `invoice-cannot-be-refunded-due-to-too-high-amount`, `invoice-incomplete`, `invoice-is-draft`, `invoice-locked`, `invoice-must-be-buffer`, `invoice-not-canceled`, `invoice-not-draft`, `invoice-not-found`, `invoice-outdated`, `invoice-paid-already`, `issue-already-connected-to-github`, `issue-not-found`, `issues-bad-request`, `issuer-not-registered`, `job-finished`, `label-already-linked`, `last-api-token`, `limit-reached`, `max-items-must-be-greater-than-zero`, `max-metamorphs-exceeded`, `max-total-charge-usd-below-minimum`, `max-total-charge-usd-must-be-greater-than-zero`, `method-not-allowed`, `migration-disabled`, `missing-actor-rights`, `missing-api-token`, `missing-billing-info`, `missing-line-items`, `missing-payment-date`, `missing-payout-billing-info`, `missing-proxy-password`, `missing-reporting-fields`, `missing-resource-name`, `missing-settings`, `missing-username`, `monthly-usage-limit-too-low`, `more-than-one-update-not-allowed`, `multiple-records-found`, `must-be-admin`, `name-not-unique`, `next-runtime-computation-failed`, `no-columns-in-exported-dataset`, `no-payment-attempt-for-refund-found`, `no-payment-method-available`, `no-team-account-seats-available`, `non-temporary-email`, `not-enough-usage-to-run-paid-actor`, `not-implemented`, `not-supported-currencies`, `o-auth-service-already-connected`, `o-auth-service-not-connected`, `oauth-resource-access-failed`, `one-time-invoice-already-marked-paid`, `only-drafts-can-be-deleted`, `operation-canceled`, `operation-not-allowed`, `operation-timed-out`, `organization-cannot-own-itself`, `organization-role-not-found`, `overlapping-payout-billing-periods`, `own-token-required`, `page-not-found`, `param-not-one-of`, `parameter-required`, `parameters-mismatched`, `password-reset-email-already-sent`, `password-reset-token-expired`, `pay-as-you-go-without-monthly-interval`, `payment-attempt-status-message-required`, `payout-already-paid`, `payout-canceled`, `payout-invalid-state`, `payout-must-be-approved-to-be-marked-paid`, `payout-not-found`, `payout-number-already-exists`, `phone-number-invalid`, `phone-number-landline`, `phone-number-opted-out`, `phone-verification-disabled`, `platform-feature-disabled`, `price-overrides-validation-failed`, `pricing-model-not-supported`, `promotional-plan-not-available`, `proxy-auth-ip-not-unique`, `public-actor-disabled`, `query-timeout`, `quoted-price-outdated`, `rate-limit-exceeded`, `recaptcha-invalid`, `recaptcha-required`, `record-not-found`, `record-not-public`, `record-or-token-not-found`, `record-too-large`, `redirect-uri-mismatch`, `reduced-plan-not-available`, `rental-charge-already-reimbursed`, `rental-not-allowed`, `request-aborted-prematurely`, `request-handled-or-locked`, `request-id-invalid`, `request-queue-duplicate-requests`, `request-too-large`, `requested-dataset-view-does-not-exist`, `resume-token-expired`, `run-failed`, `run-input-body-not-valid-json`, `run-timeout-exceeded`, `russia-is-evil`, `same-user`, `schedule-actor-not-found`, `schedule-actor-task-not-found`, `schedule-name-not-unique`, `schema-validation`, `schema-validation-error`, `schema-validation-failed`, `service-worker-registration-not-allowed`, `sign-up-method-not-allowed`, `slack-integration-not-custom`, `socket-closed`, `socket-destroyed`, `store-schema-invalid`, `store-terms-not-accepted`, `stripe-enabled`, `stripe-generic-decline`, `stripe-not-enabled`, `stripe-not-enabled-for-user`, `tagged-build-required`, `tax-country-invalid`, `tax-number-invalid`, `tax-number-validation-failed`, `taxamo-call-failed`, `taxamo-request-failed`, `testing-error`, `token-not-provided`, `too-few-versions`, `too-many-actor-tasks`, `too-many-actors`, `too-many-labels-on-resource`, `too-many-mcp-connectors`, `too-many-o-auth-apps`, `too-many-organizations`, `too-many-requests`, `too-many-schedules`, `too-many-ui-access-keys`, `too-many-user-labels`, `too-many-values`, `too-many-versions`, `too-many-webhooks`, `unexpected-route`, `unknown-build-tag`, `unknown-payment-provider`, `unsubscribe-token-invalid`, `unsupported-actor-pricing-model-for-agentic-payments`, `unsupported-content-encoding`, `unsupported-file-type-for-issue`, `unsupported-file-type-image-expected`, `unsupported-file-type-text-or-json-expected`, `unsupported-permission`, `upcoming-subscription-bill-not-up-to-date`, `user-already-exists`, `user-already-verified`, `user-creates-organizations-too-fast`, `user-disabled`, `user-email-is-disposable`, `user-email-not-set`, `user-email-not-verified`, `user-has-no-subscription`, `user-integration-not-found`, `user-is-already-invited`, `user-is-already-organization-member`, `user-is-not-member-of-organization`, `user-is-not-organization`, `user-is-organization`, `user-is-organization-owner`, `user-is-removed`, `user-not-found`, `user-not-logged-in`, `user-not-verified`, `user-or-token-not-found`, `user-plan-not-allowed-for-coupon`, `user-problem-with-card`, `user-record-not-found`, `username-already-taken`, `username-missing`, `username-not-allowed`, `username-removal-forbidden`, `username-required`, `verification-email-already-sent`, `verification-token-expired`, `version-already-exists`, `versions-size-exceeded`, `weak-password`, `x402-agentic-payment-already-finalized`, `x402-agentic-payment-insufficient-amount`, `x402-agentic-payment-malformed-token`, `x402-agentic-payment-settlement-failed`, `x402-agentic-payment-settlement-in-progress`, `x402-agentic-payment-settlement-stuck`, `x402-agentic-payment-unauthorized`, `x402-payment-required`, `zero-invoice`\]

  - **message** string
    Human-readable error message describing what went wrong.


#### Authorization: http

```
name: httpBearertype: httpscheme: bearerdescription: Bearer token provided in the `Authorization` header (e.g., `Authorization: Bearer your_token`—recommended). [More info](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Authorization).

Use your API token to authenticate requests. You can find it on the [Integrations page](https://console.apify.com/account#/integrations) in Apify Console. This method is more secure than query parameters, as headers are not logged in browser history or server logs.

:::danger Security

Do not share your API token (or account password) with untrusted parties.

:::

_When is authentication required?_
- _Required_ for private Actors, tasks, or resources (e.g., builds of private Actors).
- _Required_ when using named formats for IDs (e.g., `username~store-name` for stores or `username~queue-name` for queues).
- _Optional_ for public Actors or resources (e.g., builds of public Actors can be queried without a token).

For more information, see our [integrations documentation](https://docs.apify.com/platform/integrations).
```

- CLI
- JavaScript
- Python
- PHP
- Java
- C
- C#
- Go
- Rust
- Node.js
- Ruby
- PowerShell
- Dart
- Objective-C
- OCaml
- R
- Swift
- Kotlin

- CURL

```bash
curl -L 'https://api.apify.com/v2/store' \
-H 'Accept: application/json' \
-H 'Authorization: Bearer <token>'
```

RequestCollapse all

Base URL

Edit

https://api.apify.com

Auth

Bearer Token

Parameters

Show optional parameters

limit — query

offset — query

search — query

sortBy — query

category — query

username — query

pricingModel — query

\-\-\-FREEFLAT\_PRICE\_PER\_MONTHPRICE\_PER\_DATASET\_ITEMPAY\_PER\_EVENT

allowsAgenticUsers — query

\-\-\-truefalse

responseFormat — query

\-\-\-fullagent

includeUnrunnableActors — query

\-\-\-truefalse

Send API Request

ResponseClear

Click the `Send API Request` button above and see the response here!

reCAPTCHA

Recaptcha requires verification.

protected by **reCAPTCHA**
