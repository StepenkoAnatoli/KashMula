---
url: https://docs.apify.com/api/v2/actor-put.md
retrieved: 2026-10-04
command: firecrawl scrape https://docs.apify.com/api/v2/actor-put.md --only-main-content --json
statusCode: 200
transport: firecrawl-cli
completeness: full
---
---
title: Update Actor
url: https://docs.apify.com/api/v2/actor-put.md
parents:
  - [Apify documentation](https://docs.apify.com/llms.txt)
  - [Apify API documentation](https://docs.apify.com/api.md)
  - [Apify API](https://docs.apify.com/api/v2.md)
  - [Actors](https://docs.apify.com/api/v2/actors.md)
previous: [Get Actor](https://docs.apify.com/api/v2/actor-get.md)
next: [Delete Actor](https://docs.apify.com/api/v2/actor-delete.md)
---

> ## Documentation index
> Fetch the complete documentation index at: https://docs.apify.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Update Actor


```
PUT 
https://api.apify.com/v2/actors/:actorId
```


Updates an Actor's settings with the values specified in an `Actor` object passed as JSON in the POST payload. Only the fields specified in the request body are updated.

Returns the full `Actor` object, the same as the [Get Actor](https://docs.apify.com/api/v2/actor-get.md) endpoint.

In the HTTP request, set the `Content-Type` header to `application/json`.

### Authentication

To provide the authentication token, we recommend using the request's `Authorization` header, rather than the URL. For details, see [Authentication](https://docs.apify.com/api/v2/getting-started.md#authentication).

### Make an Actor public

To make your Actor [public](https://docs.apify.com/platform/actors/publishing):

* Set `isPublic` to `true`.
* Provide `title` and `categories`. For reference, see [constants from the apify-shared-js package](https://github.com/apify/apify-shared-js/blob/2d43ebc41ece9ad31cd6525bd523fb86939bf860/packages/consts/src/consts.ts#L452-L471)

### Update build tags

To change tags assigned to Actor builds, use the `taggedBuilds` object. It's a dictionary that maps tag names to specific builds, where:

* the key is the tag name, for example `latest` or `beta`
* the value is either `null` or an object with a build ID

Changing tags is a patch operation. Only the tags that you provide in this object are updated.

Note that you can assign multiple tags to a single build, but you can't assign the same tag to multiple builds.

* To create or reassign a tag, provide the tag name with a build ID. For example, to assign the `latest` tag to a build, use:


```json
{

  "latest": { "buildId": "z2EryhbfhgSyqj6Hn" }

}
```


* To remove a tag from a build, provide the tag name with a `null` value. For example, to remove the `beta` tag, use:


```json
{

  "beta": null

}
```


* You can perform multiple actions at once. The following example reassigns `latest` and removes `beta`, while preserving other existing tags:


```json
{

  "latest": { "buildId": "z2EryhbfhgSyqj6Hn" },

  "beta": null

}
```


## Request

### Path Parameters

* **actorId** string required

  Actor ID or the username of the Actor owner and the Actor name, separated by a tilde (`~`).

  **Example:** `compass~google-maps-extractor`

**ActorPermissionLevel**

### Body**required**

* **name** string

  The identifier of the Actor. Use lowercase letters, numbers, and hyphens. Spaces or special characters aren't allowed. Must be unique across your account.

  **Example:** `instagram-scraper`

* **description** string | null nullable

  Short description of the Actor, displayed in Apify Store and Console.

  **Example:** `This scraper extracts posts and comments from Instagram.`

* **isPublic** boolean

  Whether the Actor is available to users in Apify Store. If `false`, the Actor is private and only visible to you.

  **Example:** `false`

* **actorPermissionLevel** object

  * anyOf

    * ActorPermissionLevel
    * null

    ActorPermissionLevel (string)

    Determines the permission level that the Actor requires to run. For details, see [Actor permissions](https://docs.apify.com/platform/actors/development/permissions).

    **Possible values:** \[`LIMITED_PERMISSIONS`, `FULL_PERMISSIONS`]

    **Example:** `LIMITED_PERMISSIONS`

* **seoTitle** string | null nullable

  Name of the Actor to display by search engines such as Google. Can be different from the Actor's name displayed in Apify Store and Console. Recommended length is 40-50 characters.

  **Example:** `Free Instagram scraper`

* **seoDescription** string | null nullable

  Description of the Actor to display by search engines such as Google. Recommended length is 140-156 characters.

  **Example:** `The best scraper for Instagram`

* **title** string | null nullable

  Human-readable name of the Actor, displayed in Apify Store and Console. Can contain spaces and capital letters. Recommended length is 40-50 characters. You can change this title without affecting the Actor's URL or SEO.

  **Example:** `Instagram scraper`

* **restartOnError** boolean deprecated\
  **Example:** `false`

* **versions** object\[]

  An array of `Version` objects. Each object represents a specific version of the Actor's source code: its location, builds, and environment configuration.

  * **versionNumber** string | null nullable

    The version number of the Actor. Two numbers separated by a dot, that represent the `MAJOR.MINOR` part of the semantic versioning.

    **Possible values:** Value must match regular expression `^([0-9]|[1-9][0-9])\.([0-9]|[1-9][0-9])$`

    **Example:** `1.6`

  * **sourceType** object

    Where the source code of the version lives.

    * anyOf

      * VersionSourceType
      * null

      VersionSourceType (string)

      **Possible values:** \[`SOURCE_FILES`, `GIT_REPO`, `TARBALL`, `GITHUB_GIST`, `SOURCE_CODE`]

  * **envVars** object

    Environment variables for the version.

    * anyOf

      * object\[]
      * null

      **name** string required

      The name of the environment variable.

      **Example:** `MY_ENV_VAR`

    * **value** string

      The value of the environment variable. If `isSecret` is `true`, this value isn't returned by the API.

      **Example:** `my-value`

    * **isSecret** boolean | null nullable

      Whether the environment variable is encrypted. Secret values aren't returned by the API.

      **Example:** `false`

  * **applyEnvVarsToBuild** boolean | null nullable

    Whether to inject the environment variables at build time.

    **Example:** `false`

  * **buildTag** string | null nullable

    The tag name to apply to a successful build of this version. Can be `null` when the version has no build tag.

    **Example:** `latest`

  * **sourceFiles** object\[]

    Applies when the `sourceType` is `SOURCE_FILES`. Represents the Actor's file structure as an array of files and folders.

    * anyOf

      * SourceCodeFile
      * SourceCodeFolder

      **format** SourceCodeFileFormat (string)

      Format of the file's content, `TEXT` for plain text and `BASE64` for encoded content.

      **Possible values:** \[`BASE64`, `TEXT`]

      **Example:** `TEXT`

    * **content** string

      The contents of the file. Interpreted based on the value of `format`.

      **Example:** `console.log('This is the main.js file');`

    * **name** string required

      The path of the file relative to the Actor's root directory.

      **Example:** `src/main.js`

  * **gitRepoUrl** string | null nullable

    URL of the Git repository to clone the source code from. Applies when the `sourceType` is `GIT_REPO`.

  * **tarballUrl** string | null nullable

    URL of the tarball to download the source code from. Applies when the `sourceType` is `TARBALL`.

  * **gitHubGistUrl** string | null nullable

    URL of the GitHub Gist to clone the source code from. Applies when the `sourceType` is `GITHUB_GIST`.

* **pricingInfos** object\[]

  * oneOf

    * PayPerEventActorPricingInfo
    * PricePerDatasetItemActorPricingInfo
    * FlatPricePerMonthActorPricingInfo
    * FreeActorPricingInfo

    **apifyMarginPercentage** number required

    Apify's share of the revenue generated under this pricing info record, as a fraction between 0 and 1. Set by the Apify platform.

    **Example:** `0.2`

  * **createdAt** string\<date-time> required

    When this pricing info record has been created

  * **startedAt** string\<date-time> required

    Since when is this pricing info record effective for a given Actor

  * **notifiedAboutFutureChangeAt** string,null\<date-time> nullable

  * **notifiedAboutChangeAt** string,null\<date-time> nullable

  * **reasonForChange** string | null nullable

  * **isPriceChangeNotificationSuppressed** boolean

  * **forceContainsSignificantPriceChange** boolean

  * **pricingModel** string required\
    **Constant value:** `PAY_PER_EVENT`

  * **pricingPerEvent** object required

    * **actorChargeEvents** object

      * **property name\*** ActorChargeEvent

        Definition of a single chargeable event for a pay-per-event Actor. Each event is either flat-priced (`eventPriceUsd` is set) or tier-priced (`eventTieredPricingUsd` is set); the two are mutually exclusive.

        * **eventTitle** string required

          Human-readable title shown to users in the billing UI.

        * **eventDescription** string required

          Human-readable description of what triggers this event.

        * **eventPriceUsd** number

          Flat price per event in USD. Present only for non-tiered events. Mutually exclusive with `eventTieredPricingUsd`.

        * **eventTieredPricingUsd** object

          Tiered price-per-event pricing for a single charge event, keyed by subscription tier (e.g. `FREE`, `BRONZE`, `SILVER`, `GOLD`, `PLATINUM`, `DIAMOND`). The actual price applied is resolved from the user's tier.

          * **property name\*** TieredPricingPerEventEntry

            A single tier's price-per-event entry.

            * **tieredEventPriceUsd** number required

              Price per event in USD for this tier.

        * **isPrimaryEvent** boolean

          Whether this event is the Actor's primary chargeable event.

        * **isOneTimeEvent** boolean

          Whether this event can only be charged once per Actor run.

  * **minimalMaxTotalChargeUsd** number | null nullable

* **categories** string\[] nullable

  A list of categories that best define the Actor. Reflected in Apify Store's search and filtering options.

  **Example:** `["SOCIAL_MEDIA"]`

* **defaultRunOptions** object

  The default settings applied to an Actor run. Can be overridden by the user.

  * anyOf

    * DefaultRunOptions
    * null

    **build** string

    Which build to run. Either a build tag or a version number.

    **Example:** `latest`

  * **timeoutSecs** integer

    Timeout in seconds. 0 if no timeout.

    **Example:** `3600`

  * **memoryMbytes** integer

    In MB, the amount of memory allocated to the run.

    **Example:** `2048`

  * **restartOnError** boolean

    Whether to automatically restart the run if it fails.

    **Example:** `false`

  * **maxItems** integer | null nullable

    Maximum number of items the run might produce.

  * **forcePermissionLevel** object

    * anyOf

      * ActorPermissionLevel
      * null

      ActorPermissionLevel (string)

      Determines the permission level that the Actor requires to run. For details, see [Actor permissions](https://docs.apify.com/platform/actors/development/permissions).

      **Possible values:** \[`LIMITED_PERMISSIONS`, `FULL_PERMISSIONS`]

      **Example:** `LIMITED_PERMISSIONS`

* **taggedBuilds** object,null

  A dictionary that maps tag names to specific builds. For details, see Update build tags.

  * **property name\*** BuildTag

    The name of the build tag.

    * **buildId** string required

      The ID of the build to assign to the tag.

* **actorStandby** object

  The configuration of the Actor's standby mode. For details, see [Standby mode](https://docs.apify.com/platform/actors/development/programming-interface/standby).

  * anyOf

    * ActorStandby
    * null

    **isEnabled** boolean | null nullable

    Whether standby mode is enabled for the Actor.

  * **desiredRequestsPerActorRun** integer | null nullable

    Target number of concurrent HTTP requests a single run is configured to handle.

  * **maxRequestsPerActorRun** integer | null nullable

    Maximum number of concurrent HTTP requests that can be routed to a single run.

  * **idleTimeoutSecs** integer | null nullable

    In seconds, how long a run can stay idle without incoming requests before it's terminated.

  * **build** string | null nullable

    Which build to run in standby mode. Either a build tag or a version number.

  * **memoryMbytes** integer | null nullable

    In MB, the amount of memory allocated to the run.

  * **disableStandbyFieldsOverride** boolean | null nullable

    If `true`, prevents the standby mode configuration from being overridden elsewhere.

  * **shouldPassActorInput** boolean | null nullable

    Whether to pass the Actor's input to the standby run. If `false`, the standby runs start with no input.

* **exampleRunInput** object

  Sample input payload that demonstrates what a typical run input for an Actor looks like. Used when no explicit input for a run is provided.

  * anyOf

    * ExampleRunInput
    * null

    **body** string

    Sample input, serialized as a string.

    **Example:** `{ "helloWorld": 123 }`

  * **contentType** string

    MIME type of `body`.

    **Example:** `application/json; charset=utf-8`

* **isDeprecated** boolean | null nullable

  Whether the Actor is deprecated.

**null**

* ActorPermissionLevel (string)

  Determines the permission level that the Actor requires to run. For details, see [Actor permissions](https://docs.apify.com/platform/actors/development/permissions).

  **Possible values:** \[`LIMITED_PERMISSIONS`, `FULL_PERMISSIONS`]

  **Example:** `LIMITED_PERMISSIONS`

**VersionSourceType**

* VersionSourceType (string)

  **Possible values:** \[`SOURCE_FILES`, `GIT_REPO`, `TARBALL`, `GITHUB_GIST`, `SOURCE_CODE`]

**null**

* **name** string required

  The name of the environment variable.

  **Example:** `MY_ENV_VAR`

* **value** string

  The value of the environment variable. If `isSecret` is `true`, this value isn't returned by the API.

  **Example:** `my-value`

* **isSecret** boolean | null nullable

  Whether the environment variable is encrypted. Secret values aren't returned by the API.

  **Example:** `false`

**object\[]**

* **format** SourceCodeFileFormat (string)

  Format of the file's content, `TEXT` for plain text and `BASE64` for encoded content.

  **Possible values:** \[`BASE64`, `TEXT`]

  **Example:** `TEXT`

* **content** string

  The contents of the file. Interpreted based on the value of `format`.

  **Example:** `console.log('This is the main.js file');`

* **name** string required

  The path of the file relative to the Actor's root directory.

  **Example:** `src/main.js`

**null**

* **apifyMarginPercentage** number required

  Apify's share of the revenue generated under this pricing info record, as a fraction between 0 and 1. Set by the Apify platform.

  **Example:** `0.2`

* **createdAt** string\<date-time> required

  When this pricing info record has been created

* **startedAt** string\<date-time> required

  Since when is this pricing info record effective for a given Actor

* **notifiedAboutFutureChangeAt** string,null\<date-time> nullable

* **notifiedAboutChangeAt** string,null\<date-time> nullable

* **reasonForChange** string | null nullable

* **isPriceChangeNotificationSuppressed** boolean

* **forceContainsSignificantPriceChange** boolean

* **pricingModel** string required\
  **Constant value:** `PAY_PER_EVENT`

* **pricingPerEvent** object required

  * **actorChargeEvents** object

    * **property name\*** ActorChargeEvent

      Definition of a single chargeable event for a pay-per-event Actor. Each event is either flat-priced (`eventPriceUsd` is set) or tier-priced (`eventTieredPricingUsd` is set); the two are mutually exclusive.

      * **eventTitle** string required

        Human-readable title shown to users in the billing UI.

      * **eventDescription** string required

        Human-readable description of what triggers this event.

      * **eventPriceUsd** number

        Flat price per event in USD. Present only for non-tiered events. Mutually exclusive with `eventTieredPricingUsd`.

      * **eventTieredPricingUsd** object

        Tiered price-per-event pricing for a single charge event, keyed by subscription tier (e.g. `FREE`, `BRONZE`, `SILVER`, `GOLD`, `PLATINUM`, `DIAMOND`). The actual price applied is resolved from the user's tier.

        * **property name\*** TieredPricingPerEventEntry

          A single tier's price-per-event entry.

          * **tieredEventPriceUsd** number required

            Price per event in USD for this tier.

      * **isPrimaryEvent** boolean

        Whether this event is the Actor's primary chargeable event.

      * **isOneTimeEvent** boolean

        Whether this event can only be charged once per Actor run.

* **minimalMaxTotalChargeUsd** number | null nullable

**SourceCodeFile**

* **build** string

  Which build to run. Either a build tag or a version number.

  **Example:** `latest`

* **timeoutSecs** integer

  Timeout in seconds. 0 if no timeout.

  **Example:** `3600`

* **memoryMbytes** integer

  In MB, the amount of memory allocated to the run.

  **Example:** `2048`

* **restartOnError** boolean

  Whether to automatically restart the run if it fails.

  **Example:** `false`

* **maxItems** integer | null nullable

  Maximum number of items the run might produce.

* **forcePermissionLevel** object

  * anyOf

    * ActorPermissionLevel
    * null

    ActorPermissionLevel (string)

    Determines the permission level that the Actor requires to run. For details, see [Actor permissions](https://docs.apify.com/platform/actors/development/permissions).

    **Possible values:** \[`LIMITED_PERMISSIONS`, `FULL_PERMISSIONS`]

    **Example:** `LIMITED_PERMISSIONS`

**SourceCodeFolder**

* ActorPermissionLevel (string)

  Determines the permission level that the Actor requires to run. For details, see [Actor permissions](https://docs.apify.com/platform/actors/development/permissions).

  **Possible values:** \[`LIMITED_PERMISSIONS`, `FULL_PERMISSIONS`]

  **Example:** `LIMITED_PERMISSIONS`

**PayPerEventActorPricingInfo**

* **isEnabled** boolean | null nullable

  Whether standby mode is enabled for the Actor.

* **desiredRequestsPerActorRun** integer | null nullable

  Target number of concurrent HTTP requests a single run is configured to handle.

* **maxRequestsPerActorRun** integer | null nullable

  Maximum number of concurrent HTTP requests that can be routed to a single run.

* **idleTimeoutSecs** integer | null nullable

  In seconds, how long a run can stay idle without incoming requests before it's terminated.

* **build** string | null nullable

  Which build to run in standby mode. Either a build tag or a version number.

* **memoryMbytes** integer | null nullable

  In MB, the amount of memory allocated to the run.

* **disableStandbyFieldsOverride** boolean | null nullable

  If `true`, prevents the standby mode configuration from being overridden elsewhere.

* **shouldPassActorInput** boolean | null nullable

  Whether to pass the Actor's input to the standby run. If `false`, the standby runs start with no input.

**PricePerDatasetItemActorPricingInfo**

* **body** string

  Sample input, serialized as a string.

  **Example:** `{ "helloWorld": 123 }`

* **contentType** string

  MIME type of `body`.

  **Example:** `application/json; charset=utf-8`

### Status 200

**Response Headers**



**VersionSourceType**


```json
{

  "data": {

    "id": "zdc3Pyhyz3m8vjDeM",

    "userId": "wRsJZtadYvn4mBZmm",

    "name": "MyActor",

    "username": "jane35",

    "description": "My favourite Actor!",

    "isPublic": false,

    "actorPermissionLevel": "LIMITED_PERMISSIONS",

    "createdAt": "2019-07-08T11:27:57.401Z",

    "modifiedAt": "2019-07-08T14:01:05.546Z",

    "stats": {

      "totalBuilds": 9,

      "totalRuns": 16,

      "totalUsers": 6,

      "totalUsers7Days": 2,

      "totalUsers30Days": 6,

      "totalUsers90Days": 6,

      "totalMetamorphs": 2,

      "lastRunStartedAt": "2019-07-08T14:01:05.546Z"

    },

    "versions": [

      {

        "versionNumber": "0.1",

        "envVars": null,

        "sourceType": "SOURCE_FILES",

        "applyEnvVarsToBuild": false,

        "buildTag": "latest",

        "sourceFiles": []

      },

      {

        "versionNumber": "0.2",

        "sourceType": "GIT_REPO",

        "envVars": null,

        "applyEnvVarsToBuild": false,

        "buildTag": "latest",

        "gitRepoUrl": "https://github.com/jane35/my-actor"

      },

      {

        "versionNumber": "0.3",

        "sourceType": "TARBALL",

        "envVars": null,

        "applyEnvVarsToBuild": false,

        "buildTag": "latest",

        "tarballUrl": "https://github.com/jane35/my-actor/archive/master.zip"

      },

      {

        "versionNumber": "0.4",

        "sourceType": "GITHUB_GIST",

        "envVars": null,

        "applyEnvVarsToBuild": false,

        "buildTag": "latest",

        "gitHubGistUrl": "https://gist.github.com/jane35/e51feb784yu89"

      }

    ],

    "defaultRunOptions": {

      "build": "latest",

      "timeoutSecs": 3600,

      "memoryMbytes": 2048,

      "restartOnError": false

    },

    "exampleRunInput": {

      "body": "{ \"helloWorld\": 123 }",

      "contentType": "application/json; charset=utf-8"

    },

    "isDeprecated": false,

    "deploymentKey": "ssh-rsa AAAA ...",

    "title": "My Actor",

    "taggedBuilds": {

      "latest": {

        "buildId": "z2EryhbfhgSyqj6Hn",

        "buildNumber": "0.0.2",

        "finishedAt": "2019-06-10T11:15:49.286Z"

      }

    }

  }

}
```


**Schema**

* **data** object required

  * **id** string required

    The ID of the Actor.

    **Example:** `zdc3Pyhyz3m8vjDeM`

  * **userId** string required

    The ID of the user who owns the Actor.

    **Example:** `wRsJZtadYvn4mBZmm`

  * **name** string required

    The name of the Actor.

    **Example:** `google-search-extractor`

  * **username** string required

    The username of the Actor owner.

    **Example:** `compass`

  * **description** string | null nullable

    Short description of the Actor, displayed in Apify Store and Console.

    **Example:** `Extract data from hundreds of places fast.`

  * **restartOnError** boolean deprecated\
    **Example:** `false`

  * **isPublic** boolean required

    Whether the Actor is available to users in Apify Store.

    **Example:** `false`

  * **actorPermissionLevel** ActorPermissionLevel (string)

    Determines the permission level that the Actor requires to run. For details, see [Actor permissions](https://docs.apify.com/platform/actors/development/permissions).

    **Possible values:** \[`LIMITED_PERMISSIONS`, `FULL_PERMISSIONS`]

    **Example:** `LIMITED_PERMISSIONS`

  * **createdAt** string\<date-time> required

    The date and time the Actor was created. Follows the ISO 8601 format.

    **Example:** `2019-07-08T11:27:57.401Z`

  * **modifiedAt** string\<date-time> required

    The date and time the Actor was last modified. Follows the ISO 8601 format.

    **Example:** `2019-07-08T14:01:05.546Z`

  * **stats** object required

    Usage statistics and Apify Store metrics for the Actor.

    * **totalBuilds** integer

      The total number of builds of the Actor.

      **Example:** `9`

    * **totalRuns** integer

      The total number of runs of the Actor.

      **Example:** `16`

    * **totalUsers** integer

      The total number of Actor users, including its owner.

      **Example:** `6`

    * **totalUsers7Days** integer

      The number of active users of the Actor in the last 7 days.

      **Example:** `2`

    * **totalUsers30Days** integer

      The number of active users of the Actor in the last 30 days.

      **Example:** `6`

    * **totalUsers90Days** integer

      The number of active users of the Actor in the last 90 days.

      **Example:** `6`

    * **totalMetamorphs** integer

      The total number of times a run of another Actor was [metamorphed](https://docs.apify.com/platform/actors/development/programming-interface/metamorph) into this Actor.

      **Example:** `2`

    * **lastRunStartedAt** string\<date-time>

      The date and time the most recent run of the Actor started.

      **Example:** `2019-07-08T14:01:05.546Z`

    * **actorReviewCount** integer

      The number of reviews the Actor has received in Apify Store.

      **Example:** `69`

    * **actorReviewRating** number

      The average rating of the Actor in Apify Store.

      **Example:** `4.7`

    * **bookmarkCount** integer

      The number of users who bookmarked the Actor in Apify Store.

      **Example:** `1269`

    * **publicActorRunStats30Days** object

      Run status counts from the last 30 days. Only for public Actors. Excludes runs started by the Actor's owner.

      * **ABORTED** integer

        The number of runs that were aborted.

        **Example:** `2542`

      * **FAILED** integer

        The number of runs that failed.

        **Example:** `1234`

      * **SUCCEEDED** integer

        The number of runs that succeeded.

        **Example:** `732805`

      * **TIMED-OUT** integer

        The number of runs that timed out.

        **Example:** `12556`

      * **TOTAL** integer

        The total number of runs.

        **Example:** `749137`

  * **versions** object\[] required

    An array of `Version` objects. Each object represents a specific version of the Actor's source code: its location, builds, and environment configuration.

    * **versionNumber** string required

      The version number of the Actor. Two numbers separated by a dot, that represent the `MAJOR.MINOR` part of the semantic versioning.

      **Possible values:** Value must match regular expression `^([0-9]|[1-9][0-9])\.([0-9]|[1-9][0-9])$`

      **Example:** `0.0`

    * **sourceType** object required

      Where the source code of the version lives.

      * anyOf

        * VersionSourceType
        * null

        VersionSourceType (string)

        **Possible values:** \[`SOURCE_FILES`, `GIT_REPO`, `TARBALL`, `GITHUB_GIST`, `SOURCE_CODE`]

    * **envVars** object

      Environment variables for the version.

      * anyOf

        * object\[]
        * null

        **name** string required

        The name of the environment variable.

        **Example:** `MY_ENV_VAR`

      * **value** string

        The value of the environment variable. If `isSecret` is `true`, this value isn't returned by the API.

        **Example:** `my-value`

      * **isSecret** boolean | null nullable

        Whether the environment variable is encrypted. Secret values aren't returned by the API.

        **Example:** `false`

    * **applyEnvVarsToBuild** boolean | null nullable

      Whether to inject the environment variables at build time.

      **Example:** `false`

    * **buildTag** string | null nullable

      The tag name to apply to a successful build of this version. Can be `null` when the version has no build tag.

      **Example:** `latest`

    * **sourceFiles** object\[]

      Applies when the `sourceType` is `SOURCE_FILES`. Represents the Actor's file structure as an array of files and folders.

      * anyOf

        * SourceCodeFile
        * SourceCodeFolder

        **format** SourceCodeFileFormat (string)

        Format of the file's content, `TEXT` for plain text and `BASE64` for encoded content.

        **Possible values:** \[`BASE64`, `TEXT`]

        **Example:** `TEXT`

      * **content** string

        The contents of the file. Interpreted based on the value of `format`.

        **Example:** `console.log('This is the main.js file');`

      * **name** string required

        The path of the file relative to the Actor's root directory.

        **Example:** `src/main.js`

    * **gitRepoUrl** string | null nullable

      URL of the Git repository to clone the source code from. Applies when the `sourceType` is `GIT_REPO`.

    * **tarballUrl** string | null nullable

      URL to download the source code from as a tarball or ZIP file. Applies when the `sourceType` is `TARBALL`.

    * **gitHubGistUrl** string | null nullable

      URL of the GitHub Gist to clone the source code from. Applies when the `sourceType` is `GITHUB_GIST`.

  * **pricingInfos** object\[]

    * oneOf

      * PayPerEventActorPricingInfo
      * PricePerDatasetItemActorPricingInfo
      * FlatPricePerMonthActorPricingInfo
      * FreeActorPricingInfo

      **apifyMarginPercentage** number required

      Apify's share of the revenue generated under this pricing info record, as a fraction between 0 and 1. Set by the Apify platform.

      **Example:** `0.2`

    * **createdAt** string\<date-time> required

      When this pricing info record has been created

    * **startedAt** string\<date-time> required

      Since when is this pricing info record effective for a given Actor

    * **notifiedAboutFutureChangeAt** string,null\<date-time> nullable

    * **notifiedAboutChangeAt** string,null\<date-time> nullable

    * **reasonForChange** string | null nullable

    * **isPriceChangeNotificationSuppressed** boolean

    * **forceContainsSignificantPriceChange** boolean

    * **pricingModel** string required\
      **Constant value:** `PAY_PER_EVENT`

    * **pricingPerEvent** object required

      * **actorChargeEvents** object

        * **property name\*** ActorChargeEvent

          Definition of a single chargeable event for a pay-per-event Actor. Each event is either flat-priced (`eventPriceUsd` is set) or tier-priced (`eventTieredPricingUsd` is set); the two are mutually exclusive.

          * **eventTitle** string required

            Human-readable title shown to users in the billing UI.

          * **eventDescription** string required

            Human-readable description of what triggers this event.

          * **eventPriceUsd** number

            Flat price per event in USD. Present only for non-tiered events. Mutually exclusive with `eventTieredPricingUsd`.

          * **eventTieredPricingUsd** object

            Tiered price-per-event pricing for a single charge event, keyed by subscription tier (e.g. `FREE`, `BRONZE`, `SILVER`, `GOLD`, `PLATINUM`, `DIAMOND`). The actual price applied is resolved from the user's tier.

            * **property name\*** TieredPricingPerEventEntry

              A single tier's price-per-event entry.

              * **tieredEventPriceUsd** number required

                Price per event in USD for this tier.

          * **isPrimaryEvent** boolean

            Whether this event is the Actor's primary chargeable event.

          * **isOneTimeEvent** boolean

            Whether this event can only be charged once per Actor run.

    * **minimalMaxTotalChargeUsd** number | null nullable

  * **defaultRunOptions** object required

    The default settings applied to an Actor run. Can be overridden elsewhere.

    * **build** string

      Which build to run. Either a build tag or a version number.

      **Example:** `latest`

    * **timeoutSecs** integer

      Timeout in seconds. 0 if no timeout.

      **Example:** `3600`

    * **memoryMbytes** integer

      In MB, the amount of memory allocated to the run.

      **Example:** `2048`

    * **restartOnError** boolean

      Whether to automatically restart the run if it fails.

      **Example:** `false`

    * **maxItems** integer | null nullable

      Maximum number of items the run might produce.

    * **forcePermissionLevel** object

      * anyOf

        * ActorPermissionLevel
        * null

        ActorPermissionLevel (string)

        Determines the permission level that the Actor requires to run. For details, see [Actor permissions](https://docs.apify.com/platform/actors/development/permissions).

        **Possible values:** \[`LIMITED_PERMISSIONS`, `FULL_PERMISSIONS`]

        **Example:** `LIMITED_PERMISSIONS`

  * **exampleRunInput** object

    * anyOf

      * ExampleRunInput
      * null

      **body** string

      Sample input, serialized as a string.

      **Example:** `{ "helloWorld": 123 }`

    * **contentType** string

      MIME type of `body`.

      **Example:** `application/json; charset=utf-8`

  * **isDeprecated** boolean | null nullable

    Whether the Actor is deprecated.

    **Example:** `false`

  * **deploymentKey** string

    The Actor's public SSH key, used as a deployment key for private Git repositories.

    **Example:** `ssh-rsa AAAA ...`

  * **title** string | null nullable

    Human-readable name of the Actor, displayed in Apify Store and Console.

    **Example:** `Google Search Extractor`

  * **taggedBuilds** object

    * anyOf

      * TaggedBuilds
      * null

      object

      A dictionary mapping build tag names (e.g., "latest", "beta") to their build information.

      **Example:** `{"latest":{"buildId":"z2EryhbfhgSyqj6Hn","buildNumber":"0.0.2","finishedAt":"2019-06-10T11:15:49.286Z"},"beta":{"buildId":"abc123def456","buildNumber":"1.0.5","finishedAt":"2019-07-15T14:30:00.000Z"}}`

  * **actorStandby** object

    * anyOf

      * ActorStandby
      * null

      **isEnabled** boolean | null nullable

      Whether standby mode is enabled for the Actor.

    * **desiredRequestsPerActorRun** integer | null nullable

      Target number of concurrent HTTP requests a single run is configured to handle.

    * **maxRequestsPerActorRun** integer | null nullable

      Maximum number of concurrent HTTP requests that can be routed to a single run.

    * **idleTimeoutSecs** integer | null nullable

      In seconds, how long a run can stay idle without incoming requests before it's terminated.

    * **build** string | null nullable

      Which build to run in standby mode. Either a build tag or a version number.

    * **memoryMbytes** integer | null nullable

      In MB, the amount of memory allocated to the run.

    * **disableStandbyFieldsOverride** boolean | null nullable

      If `true`, prevents the standby mode configuration from being overridden elsewhere.

    * **shouldPassActorInput** boolean | null nullable

      Whether to pass the Actor's input to the standby run. If `false`, the standby runs start with no input.

  * **readmeSummary** string

    An AI-generated Markdown summary of the Actor's README, optimized for search and AI agents. Contains an overview and a list of use cases. Generated only for public Actors.

  * **seoTitle** string | null nullable

    Name of the Actor to display by search engines such as Google. Can be different from the Actor's name displayed in Apify Store and Console.

    **Example:** `Web Scraper`

  * **seoDescription** string | null nullable

    Description of the Actor to display by search engines such as Google.

    **Example:** `Crawls websites using Chrome and extracts data from pages using JavaScript.`

  * **pictureUrl** string | null nullable

    URL of the Actor's icon, displayed on the Actor's page in Apify Store and Console.

    **Example:** `https://apify-image-uploads-prod.s3.amazonaws.com/.../actor-picture.png`

  * **standbyUrl** string | null nullable

    URL for sending requests to the Actor in Standby mode. `null` if the Standby mode isn't enabled.

    **Example:** `https://jane35--my-actor.apify.actor`

  * **notice** ActorNotice (string,null) nullable

    A warning displayed on the Actor's page in Apify Store and Console. Can be set by the Actor's developer or automatically by Apify's quality checks.

    **Possible values:** \[`NONE`, `RESIDENTIAL_PROXY_REQUIRED`, `UNDER_MAINTENANCE`, `null`]

    **Example:** `UNDER_MAINTENANCE`

  * **categories** string\[]

    A list of categories that best define the Actor. Reflected in Apify Store's search and filtering options.

    **Example:** `["DEVELOPER_TOOLS","OPEN_SOURCE"]`

  * **isCritical** boolean

    Whether the Actor is maintained by Apify.

    **Example:** `false`

  * **isGeneric** boolean

    Whether the Actor is intended for developers. Set by Apify.

    **Example:** `false`

  * **isSourceCodeHidden** boolean

    Whether the Actor's source files are hidden on its detail page.

    **Default value:** `true`\
    **Example:** `true`

  * **hasNoDataset** boolean

    Whether the Actor stores results in a dataset. Set by Apify.

    **Example:** `false`

**null**


```json
{

  "data": {

    "id": "zdc3Pyhyz3m8vjDeM",

    "userId": "wRsJZtadYvn4mBZmm",

    "name": "MyActor",

    "username": "jane35",

    "description": "My favourite Actor!",

    "isPublic": false,

    "actorPermissionLevel": "LIMITED_PERMISSIONS",

    "createdAt": "2019-07-08T11:27:57.401Z",

    "modifiedAt": "2019-07-08T14:01:05.546Z",

    "stats": {

      "totalBuilds": 9,

      "totalRuns": 16,

      "totalUsers": 6,

      "totalUsers7Days": 2,

      "totalUsers30Days": 6,

      "totalUsers90Days": 6,

      "totalMetamorphs": 2,

      "lastRunStartedAt": "2019-07-08T14:01:05.546Z"

    },

    "versions": [

      {

        "versionNumber": "0.1",

        "envVars": null,

        "sourceType": "SOURCE_FILES",

        "applyEnvVarsToBuild": false,

        "buildTag": "latest",

        "sourceFiles": []

      },

      {

        "versionNumber": "0.2",

        "sourceType": "GIT_REPO",

        "envVars": null,

        "applyEnvVarsToBuild": false,

        "buildTag": "latest",

        "gitRepoUrl": "https://github.com/jane35/my-actor"

      },

      {

        "versionNumber": "0.3",

        "sourceType": "TARBALL",

        "envVars": null,

        "applyEnvVarsToBuild": false,

        "buildTag": "latest",

        "tarballUrl": "https://github.com/jane35/my-actor/archive/master.zip"

      },

      {

        "versionNumber": "0.4",

        "sourceType": "GITHUB_GIST",

        "envVars": null,

        "applyEnvVarsToBuild": false,

        "buildTag": "latest",

        "gitHubGistUrl": "https://gist.github.com/jane35/e51feb784yu89"

      }

    ],

    "defaultRunOptions": {

      "build": "latest",

      "timeoutSecs": 3600,

      "memoryMbytes": 2048,

      "restartOnError": false

    },

    "exampleRunInput": {

      "body": "{ \"helloWorld\": 123 }",

      "contentType": "application/json; charset=utf-8"

    },

    "isDeprecated": false,

    "deploymentKey": "ssh-rsa AAAA ...",

    "title": "My Actor",

    "taggedBuilds": {

      "latest": {

        "buildId": "z2EryhbfhgSyqj6Hn",

        "buildNumber": "0.0.2",

        "finishedAt": "2019-06-10T11:15:49.286Z"

      }

    }

  }

}
```


**object\[]**

**Schema**

* **data** object required

  * **id** string required

    The ID of the Actor.

    **Example:** `zdc3Pyhyz3m8vjDeM`

  * **userId** string required

    The ID of the user who owns the Actor.

    **Example:** `wRsJZtadYvn4mBZmm`

  * **name** string required

    The name of the Actor.

    **Example:** `google-search-extractor`

  * **username** string required

    The username of the Actor owner.

    **Example:** `compass`

  * **description** string | null nullable

    Short description of the Actor, displayed in Apify Store and Console.

    **Example:** `Extract data from hundreds of places fast.`

  * **restartOnError** boolean deprecated\
    **Example:** `false`

  * **isPublic** boolean required

    Whether the Actor is available to users in Apify Store.

    **Example:** `false`

  * **actorPermissionLevel** ActorPermissionLevel (string)

    Determines the permission level that the Actor requires to run. For details, see [Actor permissions](https://docs.apify.com/platform/actors/development/permissions).

    **Possible values:** \[`LIMITED_PERMISSIONS`, `FULL_PERMISSIONS`]

    **Example:** `LIMITED_PERMISSIONS`

  * **createdAt** string\<date-time> required

    The date and time the Actor was created. Follows the ISO 8601 format.

    **Example:** `2019-07-08T11:27:57.401Z`

  * **modifiedAt** string\<date-time> required

    The date and time the Actor was last modified. Follows the ISO 8601 format.

    **Example:** `2019-07-08T14:01:05.546Z`

  * **stats** object required

    Usage statistics and Apify Store metrics for the Actor.

    * **totalBuilds** integer

      The total number of builds of the Actor.

      **Example:** `9`

    * **totalRuns** integer

      The total number of runs of the Actor.

      **Example:** `16`

    * **totalUsers** integer

      The total number of Actor users, including its owner.

      **Example:** `6`

    * **totalUsers7Days** integer

      The number of active users of the Actor in the last 7 days.

      **Example:** `2`

    * **totalUsers30Days** integer

      The number of active users of the Actor in the last 30 days.

      **Example:** `6`

    * **totalUsers90Days** integer

      The number of active users of the Actor in the last 90 days.

      **Example:** `6`

    * **totalMetamorphs** integer

      The total number of times a run of another Actor was [metamorphed](https://docs.apify.com/platform/actors/development/programming-interface/metamorph) into this Actor.

      **Example:** `2`

    * **lastRunStartedAt** string\<date-time>

      The date and time the most recent run of the Actor started.

      **Example:** `2019-07-08T14:01:05.546Z`

    * **actorReviewCount** integer

      The number of reviews the Actor has received in Apify Store.

      **Example:** `69`

    * **actorReviewRating** number

      The average rating of the Actor in Apify Store.

      **Example:** `4.7`

    * **bookmarkCount** integer

      The number of users who bookmarked the Actor in Apify Store.

      **Example:** `1269`

    * **publicActorRunStats30Days** object

      Run status counts from the last 30 days. Only for public Actors. Excludes runs started by the Actor's owner.

      * **ABORTED** integer

        The number of runs that were aborted.

        **Example:** `2542`

      * **FAILED** integer

        The number of runs that failed.

        **Example:** `1234`

      * **SUCCEEDED** integer

        The number of runs that succeeded.

        **Example:** `732805`

      * **TIMED-OUT** integer

        The number of runs that timed out.

        **Example:** `12556`

      * **TOTAL** integer

        The total number of runs.

        **Example:** `749137`

  * **versions** object\[] required

    An array of `Version` objects. Each object represents a specific version of the Actor's source code: its location, builds, and environment configuration.

    * **versionNumber** string required

      The version number of the Actor. Two numbers separated by a dot, that represent the `MAJOR.MINOR` part of the semantic versioning.

      **Possible values:** Value must match regular expression `^([0-9]|[1-9][0-9])\.([0-9]|[1-9][0-9])$`

      **Example:** `0.0`

    * **sourceType** object required

      Where the source code of the version lives.

      * anyOf

        * VersionSourceType
        * null

        VersionSourceType (string)

        **Possible values:** \[`SOURCE_FILES`, `GIT_REPO`, `TARBALL`, `GITHUB_GIST`, `SOURCE_CODE`]

    * **envVars** object

      Environment variables for the version.

      * anyOf

        * object\[]
        * null

        **name** string required

        The name of the environment variable.

        **Example:** `MY_ENV_VAR`

      * **value** string

        The value of the environment variable. If `isSecret` is `true`, this value isn't returned by the API.

        **Example:** `my-value`

      * **isSecret** boolean | null nullable

        Whether the environment variable is encrypted. Secret values aren't returned by the API.

        **Example:** `false`

    * **applyEnvVarsToBuild** boolean | null nullable

      Whether to inject the environment variables at build time.

      **Example:** `false`

    * **buildTag** string | null nullable

      The tag name to apply to a successful build of this version. Can be `null` when the version has no build tag.

      **Example:** `latest`

    * **sourceFiles** object\[]

      Applies when the `sourceType` is `SOURCE_FILES`. Represents the Actor's file structure as an array of files and folders.

      * anyOf

        * SourceCodeFile
        * SourceCodeFolder

        **format** SourceCodeFileFormat (string)

        Format of the file's content, `TEXT` for plain text and `BASE64` for encoded content.

        **Possible values:** \[`BASE64`, `TEXT`]

        **Example:** `TEXT`

      * **content** string

        The contents of the file. Interpreted based on the value of `format`.

        **Example:** `console.log('This is the main.js file');`

      * **name** string required

        The path of the file relative to the Actor's root directory.

        **Example:** `src/main.js`

    * **gitRepoUrl** string | null nullable

      URL of the Git repository to clone the source code from. Applies when the `sourceType` is `GIT_REPO`.

    * **tarballUrl** string | null nullable

      URL to download the source code from as a tarball or ZIP file. Applies when the `sourceType` is `TARBALL`.

    * **gitHubGistUrl** string | null nullable

      URL of the GitHub Gist to clone the source code from. Applies when the `sourceType` is `GITHUB_GIST`.

  * **pricingInfos** object\[]

    * oneOf

      * PayPerEventActorPricingInfo
      * PricePerDatasetItemActorPricingInfo
      * FlatPricePerMonthActorPricingInfo
      * FreeActorPricingInfo

      **apifyMarginPercentage** number required

      Apify's share of the revenue generated under this pricing info record, as a fraction between 0 and 1. Set by the Apify platform.

      **Example:** `0.2`

    * **createdAt** string\<date-time> required

      When this pricing info record has been created

    * **startedAt** string\<date-time> required

      Since when is this pricing info record effective for a given Actor

    * **notifiedAboutFutureChangeAt** string,null\<date-time> nullable

    * **notifiedAboutChangeAt** string,null\<date-time> nullable

    * **reasonForChange** string | null nullable

    * **isPriceChangeNotificationSuppressed** boolean

    * **forceContainsSignificantPriceChange** boolean

    * **pricingModel** string required\
      **Constant value:** `PAY_PER_EVENT`

    * **pricingPerEvent** object required

      * **actorChargeEvents** object

        * **property name\*** ActorChargeEvent

          Definition of a single chargeable event for a pay-per-event Actor. Each event is either flat-priced (`eventPriceUsd` is set) or tier-priced (`eventTieredPricingUsd` is set); the two are mutually exclusive.

          * **eventTitle** string required

            Human-readable title shown to users in the billing UI.

          * **eventDescription** string required

            Human-readable description of what triggers this event.

          * **eventPriceUsd** number

            Flat price per event in USD. Present only for non-tiered events. Mutually exclusive with `eventTieredPricingUsd`.

          * **eventTieredPricingUsd** object

            Tiered price-per-event pricing for a single charge event, keyed by subscription tier (e.g. `FREE`, `BRONZE`, `SILVER`, `GOLD`, `PLATINUM`, `DIAMOND`). The actual price applied is resolved from the user's tier.

            * **property name\*** TieredPricingPerEventEntry

              A single tier's price-per-event entry.

              * **tieredEventPriceUsd** number required

                Price per event in USD for this tier.

          * **isPrimaryEvent** boolean

            Whether this event is the Actor's primary chargeable event.

          * **isOneTimeEvent** boolean

            Whether this event can only be charged once per Actor run.

    * **minimalMaxTotalChargeUsd** number | null nullable

  * **defaultRunOptions** object required

    The default settings applied to an Actor run. Can be overridden elsewhere.

    * **build** string

      Which build to run. Either a build tag or a version number.

      **Example:** `latest`

    * **timeoutSecs** integer

      Timeout in seconds. 0 if no timeout.

      **Example:** `3600`

    * **memoryMbytes** integer

      In MB, the amount of memory allocated to the run.

      **Example:** `2048`

    * **restartOnError** boolean

      Whether to automatically restart the run if it fails.

      **Example:** `false`

    * **maxItems** integer | null nullable

      Maximum number of items the run might produce.

    * **forcePermissionLevel** object

      * anyOf

        * ActorPermissionLevel
        * null

        ActorPermissionLevel (string)

        Determines the permission level that the Actor requires to run. For details, see [Actor permissions](https://docs.apify.com/platform/actors/development/permissions).

        **Possible values:** \[`LIMITED_PERMISSIONS`, `FULL_PERMISSIONS`]

        **Example:** `LIMITED_PERMISSIONS`

  * **exampleRunInput** object

    * anyOf

      * ExampleRunInput
      * null

      **body** string

      Sample input, serialized as a string.

      **Example:** `{ "helloWorld": 123 }`

    * **contentType** string

      MIME type of `body`.

      **Example:** `application/json; charset=utf-8`

  * **isDeprecated** boolean | null nullable

    Whether the Actor is deprecated.

    **Example:** `false`

  * **deploymentKey** string

    The Actor's public SSH key, used as a deployment key for private Git repositories.

    **Example:** `ssh-rsa AAAA ...`

  * **title** string | null nullable

    Human-readable name of the Actor, displayed in Apify Store and Console.

    **Example:** `Google Search Extractor`

  * **taggedBuilds** object

    * anyOf

      * TaggedBuilds
      * null

      object

      A dictionary mapping build tag names (e.g., "latest", "beta") to their build information.

      **Example:** `{"latest":{"buildId":"z2EryhbfhgSyqj6Hn","buildNumber":"0.0.2","finishedAt":"2019-06-10T11:15:49.286Z"},"beta":{"buildId":"abc123def456","buildNumber":"1.0.5","finishedAt":"2019-07-15T14:30:00.000Z"}}`

  * **actorStandby** object

    * anyOf

      * ActorStandby
      * null

      **isEnabled** boolean | null nullable

      Whether standby mode is enabled for the Actor.

    * **desiredRequestsPerActorRun** integer | null nullable

      Target number of concurrent HTTP requests a single run is configured to handle.

    * **maxRequestsPerActorRun** integer | null nullable

      Maximum number of concurrent HTTP requests that can be routed to a single run.

    * **idleTimeoutSecs** integer | null nullable

      In seconds, how long a run can stay idle without incoming requests before it's terminated.

    * **build** string | null nullable

      Which build to run in standby mode. Either a build tag or a version number.

    * **memoryMbytes** integer | null nullable

      In MB, the amount of memory allocated to the run.

    * **disableStandbyFieldsOverride** boolean | null nullable

      If `true`, prevents the standby mode configuration from being overridden elsewhere.

    * **shouldPassActorInput** boolean | null nullable

      Whether to pass the Actor's input to the standby run. If `false`, the standby runs start with no input.

  * **readmeSummary** string

    An AI-generated Markdown summary of the Actor's README, optimized for search and AI agents. Contains an overview and a list of use cases. Generated only for public Actors.

  * **seoTitle** string | null nullable

    Name of the Actor to display by search engines such as Google. Can be different from the Actor's name displayed in Apify Store and Console.

    **Example:** `Web Scraper`

  * **seoDescription** string | null nullable

    Description of the Actor to display by search engines such as Google.

    **Example:** `Crawls websites using Chrome and extracts data from pages using JavaScript.`

  * **pictureUrl** string | null nullable

    URL of the Actor's icon, displayed on the Actor's page in Apify Store and Console.

    **Example:** `https://apify-image-uploads-prod.s3.amazonaws.com/.../actor-picture.png`

  * **standbyUrl** string | null nullable

    URL for sending requests to the Actor in Standby mode. `null` if the Standby mode isn't enabled.

    **Example:** `https://jane35--my-actor.apify.actor`

  * **notice** ActorNotice (string,null) nullable

    A warning displayed on the Actor's page in Apify Store and Console. Can be set by the Actor's developer or automatically by Apify's quality checks.

    **Possible values:** \[`NONE`, `RESIDENTIAL_PROXY_REQUIRED`, `UNDER_MAINTENANCE`, `null`]

    **Example:** `UNDER_MAINTENANCE`

  * **categories** string\[]

    A list of categories that best define the Actor. Reflected in Apify Store's search and filtering options.

    **Example:** `["DEVELOPER_TOOLS","OPEN_SOURCE"]`

  * **isCritical** boolean

    Whether the Actor is maintained by Apify.

    **Example:** `false`

  * **isGeneric** boolean

    Whether the Actor is intended for developers. Set by Apify.

    **Example:** `false`

  * **isSourceCodeHidden** boolean

    Whether the Actor's source files are hidden on its detail page.

    **Default value:** `true`\
    **Example:** `true`

  * **hasNoDataset** boolean

    Whether the Actor stores results in a dataset. Set by Apify.

    **Example:** `false`

**null**

* VersionSourceType (string)

  **Possible values:** \[`SOURCE_FILES`, `GIT_REPO`, `TARBALL`, `GITHUB_GIST`, `SOURCE_CODE`]

**SourceCodeFile**

* **name** string required

  The name of the environment variable.

  **Example:** `MY_ENV_VAR`

* **value** string

  The value of the environment variable. If `isSecret` is `true`, this value isn't returned by the API.

  **Example:** `my-value`

* **isSecret** boolean | null nullable

  Whether the environment variable is encrypted. Secret values aren't returned by the API.

  **Example:** `false`

**SourceCodeFolder**

* **format** SourceCodeFileFormat (string)

  Format of the file's content, `TEXT` for plain text and `BASE64` for encoded content.

  **Possible values:** \[`BASE64`, `TEXT`]

  **Example:** `TEXT`

* **content** string

  The contents of the file. Interpreted based on the value of `format`.

  **Example:** `console.log('This is the main.js file');`

* **name** string required

  The path of the file relative to the Actor's root directory.

  **Example:** `src/main.js`

**PayPerEventActorPricingInfo**

* **apifyMarginPercentage** number required

  Apify's share of the revenue generated under this pricing info record, as a fraction between 0 and 1. Set by the Apify platform.

  **Example:** `0.2`

* **createdAt** string\<date-time> required

  When this pricing info record has been created

* **startedAt** string\<date-time> required

  Since when is this pricing info record effective for a given Actor

* **notifiedAboutFutureChangeAt** string,null\<date-time> nullable

* **notifiedAboutChangeAt** string,null\<date-time> nullable

* **reasonForChange** string | null nullable

* **isPriceChangeNotificationSuppressed** boolean

* **forceContainsSignificantPriceChange** boolean

* **pricingModel** string required\
  **Constant value:** `PAY_PER_EVENT`

* **pricingPerEvent** object required

  * **actorChargeEvents** object

    * **property name\*** ActorChargeEvent

      Definition of a single chargeable event for a pay-per-event Actor. Each event is either flat-priced (`eventPriceUsd` is set) or tier-priced (`eventTieredPricingUsd` is set); the two are mutually exclusive.

      * **eventTitle** string required

        Human-readable title shown to users in the billing UI.

      * **eventDescription** string required

        Human-readable description of what triggers this event.

      * **eventPriceUsd** number

        Flat price per event in USD. Present only for non-tiered events. Mutually exclusive with `eventTieredPricingUsd`.

      * **eventTieredPricingUsd** object

        Tiered price-per-event pricing for a single charge event, keyed by subscription tier (e.g. `FREE`, `BRONZE`, `SILVER`, `GOLD`, `PLATINUM`, `DIAMOND`). The actual price applied is resolved from the user's tier.

        * **property name\*** TieredPricingPerEventEntry

          A single tier's price-per-event entry.

          * **tieredEventPriceUsd** number required

            Price per event in USD for this tier.

      * **isPrimaryEvent** boolean

        Whether this event is the Actor's primary chargeable event.

      * **isOneTimeEvent** boolean

        Whether this event can only be charged once per Actor run.

* **minimalMaxTotalChargeUsd** number | null nullable

**PricePerDatasetItemActorPricingInfo**

* ActorPermissionLevel (string)

  Determines the permission level that the Actor requires to run. For details, see [Actor permissions](https://docs.apify.com/platform/actors/development/permissions).

  **Possible values:** \[`LIMITED_PERMISSIONS`, `FULL_PERMISSIONS`]

  **Example:** `LIMITED_PERMISSIONS`

**FlatPricePerMonthActorPricingInfo**

* **body** string

  Sample input, serialized as a string.

  **Example:** `{ "helloWorld": 123 }`

* **contentType** string

  MIME type of `body`.

  **Example:** `application/json; charset=utf-8`

**FreeActorPricingInfo**

* object

  A dictionary mapping build tag names (e.g., "latest", "beta") to their build information.

  **Example:** `{"latest":{"buildId":"z2EryhbfhgSyqj6Hn","buildNumber":"0.0.2","finishedAt":"2019-06-10T11:15:49.286Z"},"beta":{"buildId":"abc123def456","buildNumber":"1.0.5","finishedAt":"2019-07-15T14:30:00.000Z"}}`

**ActorPermissionLevel**

* **isEnabled** boolean | null nullable

  Whether standby mode is enabled for the Actor.

* **desiredRequestsPerActorRun** integer | null nullable

  Target number of concurrent HTTP requests a single run is configured to handle.

* **maxRequestsPerActorRun** integer | null nullable

  Maximum number of concurrent HTTP requests that can be routed to a single run.

* **idleTimeoutSecs** integer | null nullable

  In seconds, how long a run can stay idle without incoming requests before it's terminated.

* **build** string | null nullable

  Which build to run in standby mode. Either a build tag or a version number.

* **memoryMbytes** integer | null nullable

  In MB, the amount of memory allocated to the run.

* **disableStandbyFieldsOverride** boolean | null nullable

  If `true`, prevents the standby mode configuration from being overridden elsewhere.

* **shouldPassActorInput** boolean | null nullable

  Whether to pass the Actor's input to the standby run. If `false`, the standby runs start with no input.

### Status 400

Bad request - invalid input parameters or request body.


```json
{

  "error": {

    "type": "invalid-input",

    "message": "Invalid input: The request body contains invalid data."

  }

}
```


**Schema**

* **error** object required

  * **type** ErrorType (string)

    Machine-processable error type identifier.

    **Possible values:** \[`3d-secure-auth-failed`, `access-right-already-exists`, `action-not-found`, `actor-already-rented`, `actor-can-not-be-rented`, `actor-disabled`, `actor-is-not-rented`, `actor-memory-limit-exceeded`, `actor-name-exists-new-owner`, `actor-name-not-unique`, `actor-not-found`, `actor-not-github-actor`, `actor-not-public`, `actor-permission-level-not-supported-for-agentic-payments`, `actor-review-already-exists`, `actor-run-failed`, `actor-standby-not-supported-for-agentic-payments`, `actor-task-name-not-unique`, `agentic-payment-info-retrieval-error`, `agentic-payment-information-missing`, `agentic-payment-insufficient-amount`, `agentic-payment-provider-internal-error`, `agentic-payment-provider-unauthorized`, `airtable-webhook-deprecated`, `already-subscribed-to-paid-actor`, `apify-plan-required-to-use-paid-actor`, `apify-signup-not-allowed`, `auth-method-not-supported`, `authorization-server-not-found`, `auto-issue-date-invalid`, `background-check-required`, `billing-system-error`, `black-friday-plan-expired`, `braintree-error`, `braintree-not-linked`, `braintree-operation-timed-out`, `braintree-unsupported-currency`, `build-not-found`, `build-outdated`, `cannot-add-apify-events-to-ppe-actor`, `cannot-add-multiple-pricing-infos`, `cannot-add-pricing-info-that-alters-past`, `cannot-add-second-future-pricing-info`, `cannot-build-actor-from-webhook`, `cannot-change-billing-interval`, `cannot-change-owner`, `cannot-charge-apify-event`, `cannot-charge-non-pay-per-event-actor`, `cannot-comment-as-other-user`, `cannot-copy-actor-task`, `cannot-create-payout`, `cannot-create-public-actor`, `cannot-create-tax-transaction`, `cannot-delete-critical-actor`, `cannot-delete-invoice`, `cannot-delete-paid-actor`, `cannot-disable-one-time-event-for-apify-start-event`, `cannot-disable-organization-with-enabled-members`, `cannot-disable-user-with-subscription`, `cannot-link-oauth-to-unverified-email`, `cannot-metamorph-to-pay-per-result-actor`, `cannot-modify-actor-pricing-too-frequently`, `cannot-modify-actor-pricing-with-immediate-effect`, `cannot-monetize-without-payout-billing-info`, `cannot-override-paid-actor-trial`, `cannot-permanently-delete-subscription`, `cannot-publish-actor`, `cannot-publish-actor-task`, `cannot-reduce-last-full-token`, `cannot-reimburse-more-than-original-charge`, `cannot-reimburse-non-rental-charge`, `cannot-remove-own-actor-from-recently-used`, `cannot-remove-payment-method`, `cannot-remove-pricing-info`, `cannot-remove-running-run`, `cannot-remove-user-with-public-actors`, `cannot-remove-user-with-subscription`, `cannot-remove-user-with-unpaid-invoice`, `cannot-rename-env-var`, `cannot-rent-paid-actor`, `cannot-review-own-actor`, `cannot-set-access-rights-for-owner`, `cannot-set-is-status-message-terminal`, `cannot-unpublish-critical-actor`, `cannot-unpublish-paid-actor`, `cannot-unpublish-profile`, `cannot-update-invoice-field`, `concurrent-runs-limit-exceeded`, `concurrent-update-detected`, `conference-token-not-found`, `content-encoding-forbidden-for-html`, `coupon-already-redeemed`, `coupon-expired`, `coupon-for-new-customers`, `coupon-for-subscribed-users`, `coupon-limits-are-in-conflict-with-current-limits`, `coupon-max-number-of-redemptions-reached`, `coupon-not-found`, `coupon-not-unique`, `coupons-disabled`, `create-github-issue-not-allowed`, `creator-plan-not-available`, `cron-expression-invalid`, `daily-ai-token-limit-exceeded`, `daily-publication-limit-exceeded`, `dataset-does-not-have-fields-schema`, `dataset-does-not-have-schema`, `dataset-locked`, `dataset-schema-invalid`, `dcr-not-supported`, `default-dataset-not-found`, `deleting-default-build`, `deleting-unfinished-build`, `email-already-taken`, `email-already-taken-removed-user`, `email-domain-not-allowed-for-coupon`, `email-invalid`, `email-not-allowed`, `email-not-valid`, `email-update-too-soon`, `elevated-permissions-needed`, `env-var-already-exists`, `exchange-rate-fetch-failed`, `expired-conference-token`, `failed-to-charge-user`, `final-invoice-negative`, `full-permission-actor-blocked-for-admin`, `full-permission-actor-not-approved`, `github-branch-empty`, `github-issue-already-exists`, `github-public-key-not-found`, `github-repository-not-found`, `github-signature-does-not-match-payload`, `github-user-not-authorized-for-issues`, `gmail-not-allowed`, `id-does-not-match`, `incompatible-billing-interval`, `incomplete-payout-billing-info`, `inconsistent-currencies`, `incorrect-pricing-modifier-prefix`, `input-json-invalid-characters`, `input-json-not-object`, `input-json-too-long`, `input-update-collision`, `insufficient-permissions`, `insufficient-permissions-to-change-field`, `insufficient-security-measures`, `insufficient-tax-country-evidence`, `integration-auth-error`, `internal-server-error`, `invalid-billing-info`, `invalid-billing-period-for-payout`, `invalid-build`, `invalid-client-key`, `invalid-collection`, `invalid-conference-login-password`, `invalid-content-type-header`, `invalid-credentials`, `invalid-git-auth-token`, `invalid-github-issue-url`, `invalid-header`, `invalid-id`, `invalid-idempotency-key`, `invalid-input`, `invalid-input-schema`, `invalid-invoice`, `invalid-invoice-type`, `invalid-issue-date`, `invalid-label-params`, `invalid-main-account-user-id`, `invalid-oauth-app`, `invalid-oauth-scope`, `invalid-one-time-invoice`, `invalid-parameter`, `invalid-payout-status`, `invalid-picture-url`, `invalid-record-key`, `invalid-request`, `invalid-resource-type`, `invalid-signature`, `invalid-subscription-plan`, `invalid-tax-number`, `invalid-tax-number-format`, `invalid-token`, `invalid-token-type`, `invalid-two-factor-code`, `invalid-two-factor-code-or-recovery-code`, `invalid-two-factor-recovery-code`, `invalid-username`, `invalid-value`, `invitation-invalid-resource-type`, `invitation-no-longer-valid`, `invoice-canceled`, `invoice-cannot-be-refunded-due-to-too-high-amount`, `invoice-incomplete`, `invoice-is-draft`, `invoice-locked`, `invoice-must-be-buffer`, `invoice-not-canceled`, `invoice-not-draft`, `invoice-not-found`, `invoice-outdated`, `invoice-paid-already`, `issue-already-connected-to-github`, `issue-not-found`, `issues-bad-request`, `issuer-not-registered`, `job-finished`, `label-already-linked`, `last-api-token`, `limit-reached`, `max-items-must-be-greater-than-zero`, `max-metamorphs-exceeded`, `max-total-charge-usd-below-minimum`, `max-total-charge-usd-must-be-greater-than-zero`, `method-not-allowed`, `migration-disabled`, `missing-actor-rights`, `missing-api-token`, `missing-billing-info`, `missing-line-items`, `missing-payment-date`, `missing-payout-billing-info`, `missing-proxy-password`, `missing-reporting-fields`, `missing-resource-name`, `missing-settings`, `missing-username`, `monthly-usage-limit-too-low`, `more-than-one-update-not-allowed`, `multiple-records-found`, `must-be-admin`, `name-not-unique`, `next-runtime-computation-failed`, `no-columns-in-exported-dataset`, `no-payment-attempt-for-refund-found`, `no-payment-method-available`, `no-team-account-seats-available`, `non-temporary-email`, `not-enough-usage-to-run-paid-actor`, `not-implemented`, `not-supported-currencies`, `o-auth-service-already-connected`, `o-auth-service-not-connected`, `oauth-resource-access-failed`, `one-time-invoice-already-marked-paid`, `only-drafts-can-be-deleted`, `operation-canceled`, `operation-not-allowed`, `operation-timed-out`, `organization-cannot-own-itself`, `organization-role-not-found`, `overlapping-payout-billing-periods`, `own-token-required`, `page-not-found`, `param-not-one-of`, `parameter-required`, `parameters-mismatched`, `password-reset-email-already-sent`, `password-reset-token-expired`, `pay-as-you-go-without-monthly-interval`, `payment-attempt-status-message-required`, `payout-already-paid`, `payout-canceled`, `payout-invalid-state`, `payout-must-be-approved-to-be-marked-paid`, `payout-not-found`, `payout-number-already-exists`, `phone-number-invalid`, `phone-number-landline`, `phone-number-opted-out`, `phone-verification-disabled`, `platform-feature-disabled`, `price-overrides-validation-failed`, `pricing-model-not-supported`, `promotional-plan-not-available`, `proxy-auth-ip-not-unique`, `public-actor-disabled`, `query-timeout`, `quoted-price-outdated`, `rate-limit-exceeded`, `recaptcha-invalid`, `recaptcha-required`, `record-not-found`, `record-not-public`, `record-or-token-not-found`, `record-too-large`, `redirect-uri-mismatch`, `reduced-plan-not-available`, `rental-charge-already-reimbursed`, `rental-not-allowed`, `request-aborted-prematurely`, `request-handled-or-locked`, `request-id-invalid`, `request-queue-duplicate-requests`, `request-too-large`, `requested-dataset-view-does-not-exist`, `resume-token-expired`, `run-failed`, `run-input-body-not-valid-json`, `run-timeout-exceeded`, `russia-is-evil`, `same-user`, `schedule-actor-not-found`, `schedule-actor-task-not-found`, `schedule-name-not-unique`, `schema-validation`, `schema-validation-error`, `schema-validation-failed`, `service-worker-registration-not-allowed`, `sign-up-method-not-allowed`, `slack-integration-not-custom`, `socket-closed`, `socket-destroyed`, `store-schema-invalid`, `store-terms-not-accepted`, `stripe-enabled`, `stripe-generic-decline`, `stripe-not-enabled`, `stripe-not-enabled-for-user`, `tagged-build-required`, `tax-country-invalid`, `tax-number-invalid`, `tax-number-validation-failed`, `taxamo-call-failed`, `taxamo-request-failed`, `testing-error`, `token-not-provided`, `too-few-versions`, `too-many-actor-tasks`, `too-many-actors`, `too-many-labels-on-resource`, `too-many-mcp-connectors`, `too-many-o-auth-apps`, `too-many-organizations`, `too-many-requests`, `too-many-schedules`, `too-many-ui-access-keys`, `too-many-user-labels`, `too-many-values`, `too-many-versions`, `too-many-webhooks`, `unexpected-route`, `unknown-build-tag`, `unknown-payment-provider`, `unsubscribe-token-invalid`, `unsupported-actor-pricing-model-for-agentic-payments`, `unsupported-content-encoding`, `unsupported-file-type-for-issue`, `unsupported-file-type-image-expected`, `unsupported-file-type-text-or-json-expected`, `unsupported-permission`, `upcoming-subscription-bill-not-up-to-date`, `user-already-exists`, `user-already-verified`, `user-creates-organizations-too-fast`, `user-disabled`, `user-email-is-disposable`, `user-email-not-set`, `user-email-not-verified`, `user-has-no-subscription`, `user-integration-not-found`, `user-is-already-invited`, `user-is-already-organization-member`, `user-is-not-member-of-organization`, `user-is-not-organization`, `user-is-organization`, `user-is-organization-owner`, `user-is-removed`, `user-not-found`, `user-not-logged-in`, `user-not-verified`, `user-or-token-not-found`, `user-plan-not-allowed-for-coupon`, `user-problem-with-card`, `user-record-not-found`, `username-already-taken`, `username-missing`, `username-not-allowed`, `username-removal-forbidden`, `username-required`, `verification-email-already-sent`, `verification-token-expired`, `version-already-exists`, `versions-size-exceeded`, `weak-password`, `x402-agentic-payment-already-finalized`, `x402-agentic-payment-insufficient-amount`, `x402-agentic-payment-malformed-token`, `x402-agentic-payment-settlement-failed`, `x402-agentic-payment-settlement-in-progress`, `x402-agentic-payment-settlement-stuck`, `x402-agentic-payment-unauthorized`, `x402-payment-required`, `zero-invoice`]

  * **message** string

    Human-readable error message describing what went wrong.


```json
{

  "error": {

    "type": "invalid-input",

    "message": "Invalid input: The request body contains invalid data."

  }

}
```


**Schema**

* **error** object required

  * **type** ErrorType (string)

    Machine-processable error type identifier.

    **Possible values:** \[`3d-secure-auth-failed`, `access-right-already-exists`, `action-not-found`, `actor-already-rented`, `actor-can-not-be-rented`, `actor-disabled`, `actor-is-not-rented`, `actor-memory-limit-exceeded`, `actor-name-exists-new-owner`, `actor-name-not-unique`, `actor-not-found`, `actor-not-github-actor`, `actor-not-public`, `actor-permission-level-not-supported-for-agentic-payments`, `actor-review-already-exists`, `actor-run-failed`, `actor-standby-not-supported-for-agentic-payments`, `actor-task-name-not-unique`, `agentic-payment-info-retrieval-error`, `agentic-payment-information-missing`, `agentic-payment-insufficient-amount`, `agentic-payment-provider-internal-error`, `agentic-payment-provider-unauthorized`, `airtable-webhook-deprecated`, `already-subscribed-to-paid-actor`, `apify-plan-required-to-use-paid-actor`, `apify-signup-not-allowed`, `auth-method-not-supported`, `authorization-server-not-found`, `auto-issue-date-invalid`, `background-check-required`, `billing-system-error`, `black-friday-plan-expired`, `braintree-error`, `braintree-not-linked`, `braintree-operation-timed-out`, `braintree-unsupported-currency`, `build-not-found`, `build-outdated`, `cannot-add-apify-events-to-ppe-actor`, `cannot-add-multiple-pricing-infos`, `cannot-add-pricing-info-that-alters-past`, `cannot-add-second-future-pricing-info`, `cannot-build-actor-from-webhook`, `cannot-change-billing-interval`, `cannot-change-owner`, `cannot-charge-apify-event`, `cannot-charge-non-pay-per-event-actor`, `cannot-comment-as-other-user`, `cannot-copy-actor-task`, `cannot-create-payout`, `cannot-create-public-actor`, `cannot-create-tax-transaction`, `cannot-delete-critical-actor`, `cannot-delete-invoice`, `cannot-delete-paid-actor`, `cannot-disable-one-time-event-for-apify-start-event`, `cannot-disable-organization-with-enabled-members`, `cannot-disable-user-with-subscription`, `cannot-link-oauth-to-unverified-email`, `cannot-metamorph-to-pay-per-result-actor`, `cannot-modify-actor-pricing-too-frequently`, `cannot-modify-actor-pricing-with-immediate-effect`, `cannot-monetize-without-payout-billing-info`, `cannot-override-paid-actor-trial`, `cannot-permanently-delete-subscription`, `cannot-publish-actor`, `cannot-publish-actor-task`, `cannot-reduce-last-full-token`, `cannot-reimburse-more-than-original-charge`, `cannot-reimburse-non-rental-charge`, `cannot-remove-own-actor-from-recently-used`, `cannot-remove-payment-method`, `cannot-remove-pricing-info`, `cannot-remove-running-run`, `cannot-remove-user-with-public-actors`, `cannot-remove-user-with-subscription`, `cannot-remove-user-with-unpaid-invoice`, `cannot-rename-env-var`, `cannot-rent-paid-actor`, `cannot-review-own-actor`, `cannot-set-access-rights-for-owner`, `cannot-set-is-status-message-terminal`, `cannot-unpublish-critical-actor`, `cannot-unpublish-paid-actor`, `cannot-unpublish-profile`, `cannot-update-invoice-field`, `concurrent-runs-limit-exceeded`, `concurrent-update-detected`, `conference-token-not-found`, `content-encoding-forbidden-for-html`, `coupon-already-redeemed`, `coupon-expired`, `coupon-for-new-customers`, `coupon-for-subscribed-users`, `coupon-limits-are-in-conflict-with-current-limits`, `coupon-max-number-of-redemptions-reached`, `coupon-not-found`, `coupon-not-unique`, `coupons-disabled`, `create-github-issue-not-allowed`, `creator-plan-not-available`, `cron-expression-invalid`, `daily-ai-token-limit-exceeded`, `daily-publication-limit-exceeded`, `dataset-does-not-have-fields-schema`, `dataset-does-not-have-schema`, `dataset-locked`, `dataset-schema-invalid`, `dcr-not-supported`, `default-dataset-not-found`, `deleting-default-build`, `deleting-unfinished-build`, `email-already-taken`, `email-already-taken-removed-user`, `email-domain-not-allowed-for-coupon`, `email-invalid`, `email-not-allowed`, `email-not-valid`, `email-update-too-soon`, `elevated-permissions-needed`, `env-var-already-exists`, `exchange-rate-fetch-failed`, `expired-conference-token`, `failed-to-charge-user`, `final-invoice-negative`, `full-permission-actor-blocked-for-admin`, `full-permission-actor-not-approved`, `github-branch-empty`, `github-issue-already-exists`, `github-public-key-not-found`, `github-repository-not-found`, `github-signature-does-not-match-payload`, `github-user-not-authorized-for-issues`, `gmail-not-allowed`, `id-does-not-match`, `incompatible-billing-interval`, `incomplete-payout-billing-info`, `inconsistent-currencies`, `incorrect-pricing-modifier-prefix`, `input-json-invalid-characters`, `input-json-not-object`, `input-json-too-long`, `input-update-collision`, `insufficient-permissions`, `insufficient-permissions-to-change-field`, `insufficient-security-measures`, `insufficient-tax-country-evidence`, `integration-auth-error`, `internal-server-error`, `invalid-billing-info`, `invalid-billing-period-for-payout`, `invalid-build`, `invalid-client-key`, `invalid-collection`, `invalid-conference-login-password`, `invalid-content-type-header`, `invalid-credentials`, `invalid-git-auth-token`, `invalid-github-issue-url`, `invalid-header`, `invalid-id`, `invalid-idempotency-key`, `invalid-input`, `invalid-input-schema`, `invalid-invoice`, `invalid-invoice-type`, `invalid-issue-date`, `invalid-label-params`, `invalid-main-account-user-id`, `invalid-oauth-app`, `invalid-oauth-scope`, `invalid-one-time-invoice`, `invalid-parameter`, `invalid-payout-status`, `invalid-picture-url`, `invalid-record-key`, `invalid-request`, `invalid-resource-type`, `invalid-signature`, `invalid-subscription-plan`, `invalid-tax-number`, `invalid-tax-number-format`, `invalid-token`, `invalid-token-type`, `invalid-two-factor-code`, `invalid-two-factor-code-or-recovery-code`, `invalid-two-factor-recovery-code`, `invalid-username`, `invalid-value`, `invitation-invalid-resource-type`, `invitation-no-longer-valid`, `invoice-canceled`, `invoice-cannot-be-refunded-due-to-too-high-amount`, `invoice-incomplete`, `invoice-is-draft`, `invoice-locked`, `invoice-must-be-buffer`, `invoice-not-canceled`, `invoice-not-draft`, `invoice-not-found`, `invoice-outdated`, `invoice-paid-already`, `issue-already-connected-to-github`, `issue-not-found`, `issues-bad-request`, `issuer-not-registered`, `job-finished`, `label-already-linked`, `last-api-token`, `limit-reached`, `max-items-must-be-greater-than-zero`, `max-metamorphs-exceeded`, `max-total-charge-usd-below-minimum`, `max-total-charge-usd-must-be-greater-than-zero`, `method-not-allowed`, `migration-disabled`, `missing-actor-rights`, `missing-api-token`, `missing-billing-info`, `missing-line-items`, `missing-payment-date`, `missing-payout-billing-info`, `missing-proxy-password`, `missing-reporting-fields`, `missing-resource-name`, `missing-settings`, `missing-username`, `monthly-usage-limit-too-low`, `more-than-one-update-not-allowed`, `multiple-records-found`, `must-be-admin`, `name-not-unique`, `next-runtime-computation-failed`, `no-columns-in-exported-dataset`, `no-payment-attempt-for-refund-found`, `no-payment-method-available`, `no-team-account-seats-available`, `non-temporary-email`, `not-enough-usage-to-run-paid-actor`, `not-implemented`, `not-supported-currencies`, `o-auth-service-already-connected`, `o-auth-service-not-connected`, `oauth-resource-access-failed`, `one-time-invoice-already-marked-paid`, `only-drafts-can-be-deleted`, `operation-canceled`, `operation-not-allowed`, `operation-timed-out`, `organization-cannot-own-itself`, `organization-role-not-found`, `overlapping-payout-billing-periods`, `own-token-required`, `page-not-found`, `param-not-one-of`, `parameter-required`, `parameters-mismatched`, `password-reset-email-already-sent`, `password-reset-token-expired`, `pay-as-you-go-without-monthly-interval`, `payment-attempt-status-message-required`, `payout-already-paid`, `payout-canceled`, `payout-invalid-state`, `payout-must-be-approved-to-be-marked-paid`, `payout-not-found`, `payout-number-already-exists`, `phone-number-invalid`, `phone-number-landline`, `phone-number-opted-out`, `phone-verification-disabled`, `platform-feature-disabled`, `price-overrides-validation-failed`, `pricing-model-not-supported`, `promotional-plan-not-available`, `proxy-auth-ip-not-unique`, `public-actor-disabled`, `query-timeout`, `quoted-price-outdated`, `rate-limit-exceeded`, `recaptcha-invalid`, `recaptcha-required`, `record-not-found`, `record-not-public`, `record-or-token-not-found`, `record-too-large`, `redirect-uri-mismatch`, `reduced-plan-not-available`, `rental-charge-already-reimbursed`, `rental-not-allowed`, `request-aborted-prematurely`, `request-handled-or-locked`, `request-id-invalid`, `request-queue-duplicate-requests`, `request-too-large`, `requested-dataset-view-does-not-exist`, `resume-token-expired`, `run-failed`, `run-input-body-not-valid-json`, `run-timeout-exceeded`, `russia-is-evil`, `same-user`, `schedule-actor-not-found`, `schedule-actor-task-not-found`, `schedule-name-not-unique`, `schema-validation`, `schema-validation-error`, `schema-validation-failed`, `service-worker-registration-not-allowed`, `sign-up-method-not-allowed`, `slack-integration-not-custom`, `socket-closed`, `socket-destroyed`, `store-schema-invalid`, `store-terms-not-accepted`, `stripe-enabled`, `stripe-generic-decline`, `stripe-not-enabled`, `stripe-not-enabled-for-user`, `tagged-build-required`, `tax-country-invalid`, `tax-number-invalid`, `tax-number-validation-failed`, `taxamo-call-failed`, `taxamo-request-failed`, `testing-error`, `token-not-provided`, `too-few-versions`, `too-many-actor-tasks`, `too-many-actors`, `too-many-labels-on-resource`, `too-many-mcp-connectors`, `too-many-o-auth-apps`, `too-many-organizations`, `too-many-requests`, `too-many-schedules`, `too-many-ui-access-keys`, `too-many-user-labels`, `too-many-values`, `too-many-versions`, `too-many-webhooks`, `unexpected-route`, `unknown-build-tag`, `unknown-payment-provider`, `unsubscribe-token-invalid`, `unsupported-actor-pricing-model-for-agentic-payments`, `unsupported-content-encoding`, `unsupported-file-type-for-issue`, `unsupported-file-type-image-expected`, `unsupported-file-type-text-or-json-expected`, `unsupported-permission`, `upcoming-subscription-bill-not-up-to-date`, `user-already-exists`, `user-already-verified`, `user-creates-organizations-too-fast`, `user-disabled`, `user-email-is-disposable`, `user-email-not-set`, `user-email-not-verified`, `user-has-no-subscription`, `user-integration-not-found`, `user-is-already-invited`, `user-is-already-organization-member`, `user-is-not-member-of-organization`, `user-is-not-organization`, `user-is-organization`, `user-is-organization-owner`, `user-is-removed`, `user-not-found`, `user-not-logged-in`, `user-not-verified`, `user-or-token-not-found`, `user-plan-not-allowed-for-coupon`, `user-problem-with-card`, `user-record-not-found`, `username-already-taken`, `username-missing`, `username-not-allowed`, `username-removal-forbidden`, `username-required`, `verification-email-already-sent`, `verification-token-expired`, `version-already-exists`, `versions-size-exceeded`, `weak-password`, `x402-agentic-payment-already-finalized`, `x402-agentic-payment-insufficient-amount`, `x402-agentic-payment-malformed-token`, `x402-agentic-payment-settlement-failed`, `x402-agentic-payment-settlement-in-progress`, `x402-agentic-payment-settlement-stuck`, `x402-agentic-payment-unauthorized`, `x402-payment-required`, `zero-invoice`]

  * **message** string

    Human-readable error message describing what went wrong.

### Status 401

Unauthorized - authentication required or invalid token.


```json
{

  "error": {

    "type": "invalid-token",

    "message": "Authentication token is not valid."

  }

}
```


**Schema**

* **error** object required

  * **type** ErrorType (string)

    Machine-processable error type identifier.

    **Possible values:** \[`3d-secure-auth-failed`, `access-right-already-exists`, `action-not-found`, `actor-already-rented`, `actor-can-not-be-rented`, `actor-disabled`, `actor-is-not-rented`, `actor-memory-limit-exceeded`, `actor-name-exists-new-owner`, `actor-name-not-unique`, `actor-not-found`, `actor-not-github-actor`, `actor-not-public`, `actor-permission-level-not-supported-for-agentic-payments`, `actor-review-already-exists`, `actor-run-failed`, `actor-standby-not-supported-for-agentic-payments`, `actor-task-name-not-unique`, `agentic-payment-info-retrieval-error`, `agentic-payment-information-missing`, `agentic-payment-insufficient-amount`, `agentic-payment-provider-internal-error`, `agentic-payment-provider-unauthorized`, `airtable-webhook-deprecated`, `already-subscribed-to-paid-actor`, `apify-plan-required-to-use-paid-actor`, `apify-signup-not-allowed`, `auth-method-not-supported`, `authorization-server-not-found`, `auto-issue-date-invalid`, `background-check-required`, `billing-system-error`, `black-friday-plan-expired`, `braintree-error`, `braintree-not-linked`, `braintree-operation-timed-out`, `braintree-unsupported-currency`, `build-not-found`, `build-outdated`, `cannot-add-apify-events-to-ppe-actor`, `cannot-add-multiple-pricing-infos`, `cannot-add-pricing-info-that-alters-past`, `cannot-add-second-future-pricing-info`, `cannot-build-actor-from-webhook`, `cannot-change-billing-interval`, `cannot-change-owner`, `cannot-charge-apify-event`, `cannot-charge-non-pay-per-event-actor`, `cannot-comment-as-other-user`, `cannot-copy-actor-task`, `cannot-create-payout`, `cannot-create-public-actor`, `cannot-create-tax-transaction`, `cannot-delete-critical-actor`, `cannot-delete-invoice`, `cannot-delete-paid-actor`, `cannot-disable-one-time-event-for-apify-start-event`, `cannot-disable-organization-with-enabled-members`, `cannot-disable-user-with-subscription`, `cannot-link-oauth-to-unverified-email`, `cannot-metamorph-to-pay-per-result-actor`, `cannot-modify-actor-pricing-too-frequently`, `cannot-modify-actor-pricing-with-immediate-effect`, `cannot-monetize-without-payout-billing-info`, `cannot-override-paid-actor-trial`, `cannot-permanently-delete-subscription`, `cannot-publish-actor`, `cannot-publish-actor-task`, `cannot-reduce-last-full-token`, `cannot-reimburse-more-than-original-charge`, `cannot-reimburse-non-rental-charge`, `cannot-remove-own-actor-from-recently-used`, `cannot-remove-payment-method`, `cannot-remove-pricing-info`, `cannot-remove-running-run`, `cannot-remove-user-with-public-actors`, `cannot-remove-user-with-subscription`, `cannot-remove-user-with-unpaid-invoice`, `cannot-rename-env-var`, `cannot-rent-paid-actor`, `cannot-review-own-actor`, `cannot-set-access-rights-for-owner`, `cannot-set-is-status-message-terminal`, `cannot-unpublish-critical-actor`, `cannot-unpublish-paid-actor`, `cannot-unpublish-profile`, `cannot-update-invoice-field`, `concurrent-runs-limit-exceeded`, `concurrent-update-detected`, `conference-token-not-found`, `content-encoding-forbidden-for-html`, `coupon-already-redeemed`, `coupon-expired`, `coupon-for-new-customers`, `coupon-for-subscribed-users`, `coupon-limits-are-in-conflict-with-current-limits`, `coupon-max-number-of-redemptions-reached`, `coupon-not-found`, `coupon-not-unique`, `coupons-disabled`, `create-github-issue-not-allowed`, `creator-plan-not-available`, `cron-expression-invalid`, `daily-ai-token-limit-exceeded`, `daily-publication-limit-exceeded`, `dataset-does-not-have-fields-schema`, `dataset-does-not-have-schema`, `dataset-locked`, `dataset-schema-invalid`, `dcr-not-supported`, `default-dataset-not-found`, `deleting-default-build`, `deleting-unfinished-build`, `email-already-taken`, `email-already-taken-removed-user`, `email-domain-not-allowed-for-coupon`, `email-invalid`, `email-not-allowed`, `email-not-valid`, `email-update-too-soon`, `elevated-permissions-needed`, `env-var-already-exists`, `exchange-rate-fetch-failed`, `expired-conference-token`, `failed-to-charge-user`, `final-invoice-negative`, `full-permission-actor-blocked-for-admin`, `full-permission-actor-not-approved`, `github-branch-empty`, `github-issue-already-exists`, `github-public-key-not-found`, `github-repository-not-found`, `github-signature-does-not-match-payload`, `github-user-not-authorized-for-issues`, `gmail-not-allowed`, `id-does-not-match`, `incompatible-billing-interval`, `incomplete-payout-billing-info`, `inconsistent-currencies`, `incorrect-pricing-modifier-prefix`, `input-json-invalid-characters`, `input-json-not-object`, `input-json-too-long`, `input-update-collision`, `insufficient-permissions`, `insufficient-permissions-to-change-field`, `insufficient-security-measures`, `insufficient-tax-country-evidence`, `integration-auth-error`, `internal-server-error`, `invalid-billing-info`, `invalid-billing-period-for-payout`, `invalid-build`, `invalid-client-key`, `invalid-collection`, `invalid-conference-login-password`, `invalid-content-type-header`, `invalid-credentials`, `invalid-git-auth-token`, `invalid-github-issue-url`, `invalid-header`, `invalid-id`, `invalid-idempotency-key`, `invalid-input`, `invalid-input-schema`, `invalid-invoice`, `invalid-invoice-type`, `invalid-issue-date`, `invalid-label-params`, `invalid-main-account-user-id`, `invalid-oauth-app`, `invalid-oauth-scope`, `invalid-one-time-invoice`, `invalid-parameter`, `invalid-payout-status`, `invalid-picture-url`, `invalid-record-key`, `invalid-request`, `invalid-resource-type`, `invalid-signature`, `invalid-subscription-plan`, `invalid-tax-number`, `invalid-tax-number-format`, `invalid-token`, `invalid-token-type`, `invalid-two-factor-code`, `invalid-two-factor-code-or-recovery-code`, `invalid-two-factor-recovery-code`, `invalid-username`, `invalid-value`, `invitation-invalid-resource-type`, `invitation-no-longer-valid`, `invoice-canceled`, `invoice-cannot-be-refunded-due-to-too-high-amount`, `invoice-incomplete`, `invoice-is-draft`, `invoice-locked`, `invoice-must-be-buffer`, `invoice-not-canceled`, `invoice-not-draft`, `invoice-not-found`, `invoice-outdated`, `invoice-paid-already`, `issue-already-connected-to-github`, `issue-not-found`, `issues-bad-request`, `issuer-not-registered`, `job-finished`, `label-already-linked`, `last-api-token`, `limit-reached`, `max-items-must-be-greater-than-zero`, `max-metamorphs-exceeded`, `max-total-charge-usd-below-minimum`, `max-total-charge-usd-must-be-greater-than-zero`, `method-not-allowed`, `migration-disabled`, `missing-actor-rights`, `missing-api-token`, `missing-billing-info`, `missing-line-items`, `missing-payment-date`, `missing-payout-billing-info`, `missing-proxy-password`, `missing-reporting-fields`, `missing-resource-name`, `missing-settings`, `missing-username`, `monthly-usage-limit-too-low`, `more-than-one-update-not-allowed`, `multiple-records-found`, `must-be-admin`, `name-not-unique`, `next-runtime-computation-failed`, `no-columns-in-exported-dataset`, `no-payment-attempt-for-refund-found`, `no-payment-method-available`, `no-team-account-seats-available`, `non-temporary-email`, `not-enough-usage-to-run-paid-actor`, `not-implemented`, `not-supported-currencies`, `o-auth-service-already-connected`, `o-auth-service-not-connected`, `oauth-resource-access-failed`, `one-time-invoice-already-marked-paid`, `only-drafts-can-be-deleted`, `operation-canceled`, `operation-not-allowed`, `operation-timed-out`, `organization-cannot-own-itself`, `organization-role-not-found`, `overlapping-payout-billing-periods`, `own-token-required`, `page-not-found`, `param-not-one-of`, `parameter-required`, `parameters-mismatched`, `password-reset-email-already-sent`, `password-reset-token-expired`, `pay-as-you-go-without-monthly-interval`, `payment-attempt-status-message-required`, `payout-already-paid`, `payout-canceled`, `payout-invalid-state`, `payout-must-be-approved-to-be-marked-paid`, `payout-not-found`, `payout-number-already-exists`, `phone-number-invalid`, `phone-number-landline`, `phone-number-opted-out`, `phone-verification-disabled`, `platform-feature-disabled`, `price-overrides-validation-failed`, `pricing-model-not-supported`, `promotional-plan-not-available`, `proxy-auth-ip-not-unique`, `public-actor-disabled`, `query-timeout`, `quoted-price-outdated`, `rate-limit-exceeded`, `recaptcha-invalid`, `recaptcha-required`, `record-not-found`, `record-not-public`, `record-or-token-not-found`, `record-too-large`, `redirect-uri-mismatch`, `reduced-plan-not-available`, `rental-charge-already-reimbursed`, `rental-not-allowed`, `request-aborted-prematurely`, `request-handled-or-locked`, `request-id-invalid`, `request-queue-duplicate-requests`, `request-too-large`, `requested-dataset-view-does-not-exist`, `resume-token-expired`, `run-failed`, `run-input-body-not-valid-json`, `run-timeout-exceeded`, `russia-is-evil`, `same-user`, `schedule-actor-not-found`, `schedule-actor-task-not-found`, `schedule-name-not-unique`, `schema-validation`, `schema-validation-error`, `schema-validation-failed`, `service-worker-registration-not-allowed`, `sign-up-method-not-allowed`, `slack-integration-not-custom`, `socket-closed`, `socket-destroyed`, `store-schema-invalid`, `store-terms-not-accepted`, `stripe-enabled`, `stripe-generic-decline`, `stripe-not-enabled`, `stripe-not-enabled-for-user`, `tagged-build-required`, `tax-country-invalid`, `tax-number-invalid`, `tax-number-validation-failed`, `taxamo-call-failed`, `taxamo-request-failed`, `testing-error`, `token-not-provided`, `too-few-versions`, `too-many-actor-tasks`, `too-many-actors`, `too-many-labels-on-resource`, `too-many-mcp-connectors`, `too-many-o-auth-apps`, `too-many-organizations`, `too-many-requests`, `too-many-schedules`, `too-many-ui-access-keys`, `too-many-user-labels`, `too-many-values`, `too-many-versions`, `too-many-webhooks`, `unexpected-route`, `unknown-build-tag`, `unknown-payment-provider`, `unsubscribe-token-invalid`, `unsupported-actor-pricing-model-for-agentic-payments`, `unsupported-content-encoding`, `unsupported-file-type-for-issue`, `unsupported-file-type-image-expected`, `unsupported-file-type-text-or-json-expected`, `unsupported-permission`, `upcoming-subscription-bill-not-up-to-date`, `user-already-exists`, `user-already-verified`, `user-creates-organizations-too-fast`, `user-disabled`, `user-email-is-disposable`, `user-email-not-set`, `user-email-not-verified`, `user-has-no-subscription`, `user-integration-not-found`, `user-is-already-invited`, `user-is-already-organization-member`, `user-is-not-member-of-organization`, `user-is-not-organization`, `user-is-organization`, `user-is-organization-owner`, `user-is-removed`, `user-not-found`, `user-not-logged-in`, `user-not-verified`, `user-or-token-not-found`, `user-plan-not-allowed-for-coupon`, `user-problem-with-card`, `user-record-not-found`, `username-already-taken`, `username-missing`, `username-not-allowed`, `username-removal-forbidden`, `username-required`, `verification-email-already-sent`, `verification-token-expired`, `version-already-exists`, `versions-size-exceeded`, `weak-password`, `x402-agentic-payment-already-finalized`, `x402-agentic-payment-insufficient-amount`, `x402-agentic-payment-malformed-token`, `x402-agentic-payment-settlement-failed`, `x402-agentic-payment-settlement-in-progress`, `x402-agentic-payment-settlement-stuck`, `x402-agentic-payment-unauthorized`, `x402-payment-required`, `zero-invoice`]

  * **message** string

    Human-readable error message describing what went wrong.


```json
{

  "error": {

    "type": "invalid-token",

    "message": "Authentication token is not valid."

  }

}
```


**Schema**

* **error** object required

  * **type** ErrorType (string)

    Machine-processable error type identifier.

    **Possible values:** \[`3d-secure-auth-failed`, `access-right-already-exists`, `action-not-found`, `actor-already-rented`, `actor-can-not-be-rented`, `actor-disabled`, `actor-is-not-rented`, `actor-memory-limit-exceeded`, `actor-name-exists-new-owner`, `actor-name-not-unique`, `actor-not-found`, `actor-not-github-actor`, `actor-not-public`, `actor-permission-level-not-supported-for-agentic-payments`, `actor-review-already-exists`, `actor-run-failed`, `actor-standby-not-supported-for-agentic-payments`, `actor-task-name-not-unique`, `agentic-payment-info-retrieval-error`, `agentic-payment-information-missing`, `agentic-payment-insufficient-amount`, `agentic-payment-provider-internal-error`, `agentic-payment-provider-unauthorized`, `airtable-webhook-deprecated`, `already-subscribed-to-paid-actor`, `apify-plan-required-to-use-paid-actor`, `apify-signup-not-allowed`, `auth-method-not-supported`, `authorization-server-not-found`, `auto-issue-date-invalid`, `background-check-required`, `billing-system-error`, `black-friday-plan-expired`, `braintree-error`, `braintree-not-linked`, `braintree-operation-timed-out`, `braintree-unsupported-currency`, `build-not-found`, `build-outdated`, `cannot-add-apify-events-to-ppe-actor`, `cannot-add-multiple-pricing-infos`, `cannot-add-pricing-info-that-alters-past`, `cannot-add-second-future-pricing-info`, `cannot-build-actor-from-webhook`, `cannot-change-billing-interval`, `cannot-change-owner`, `cannot-charge-apify-event`, `cannot-charge-non-pay-per-event-actor`, `cannot-comment-as-other-user`, `cannot-copy-actor-task`, `cannot-create-payout`, `cannot-create-public-actor`, `cannot-create-tax-transaction`, `cannot-delete-critical-actor`, `cannot-delete-invoice`, `cannot-delete-paid-actor`, `cannot-disable-one-time-event-for-apify-start-event`, `cannot-disable-organization-with-enabled-members`, `cannot-disable-user-with-subscription`, `cannot-link-oauth-to-unverified-email`, `cannot-metamorph-to-pay-per-result-actor`, `cannot-modify-actor-pricing-too-frequently`, `cannot-modify-actor-pricing-with-immediate-effect`, `cannot-monetize-without-payout-billing-info`, `cannot-override-paid-actor-trial`, `cannot-permanently-delete-subscription`, `cannot-publish-actor`, `cannot-publish-actor-task`, `cannot-reduce-last-full-token`, `cannot-reimburse-more-than-original-charge`, `cannot-reimburse-non-rental-charge`, `cannot-remove-own-actor-from-recently-used`, `cannot-remove-payment-method`, `cannot-remove-pricing-info`, `cannot-remove-running-run`, `cannot-remove-user-with-public-actors`, `cannot-remove-user-with-subscription`, `cannot-remove-user-with-unpaid-invoice`, `cannot-rename-env-var`, `cannot-rent-paid-actor`, `cannot-review-own-actor`, `cannot-set-access-rights-for-owner`, `cannot-set-is-status-message-terminal`, `cannot-unpublish-critical-actor`, `cannot-unpublish-paid-actor`, `cannot-unpublish-profile`, `cannot-update-invoice-field`, `concurrent-runs-limit-exceeded`, `concurrent-update-detected`, `conference-token-not-found`, `content-encoding-forbidden-for-html`, `coupon-already-redeemed`, `coupon-expired`, `coupon-for-new-customers`, `coupon-for-subscribed-users`, `coupon-limits-are-in-conflict-with-current-limits`, `coupon-max-number-of-redemptions-reached`, `coupon-not-found`, `coupon-not-unique`, `coupons-disabled`, `create-github-issue-not-allowed`, `creator-plan-not-available`, `cron-expression-invalid`, `daily-ai-token-limit-exceeded`, `daily-publication-limit-exceeded`, `dataset-does-not-have-fields-schema`, `dataset-does-not-have-schema`, `dataset-locked`, `dataset-schema-invalid`, `dcr-not-supported`, `default-dataset-not-found`, `deleting-default-build`, `deleting-unfinished-build`, `email-already-taken`, `email-already-taken-removed-user`, `email-domain-not-allowed-for-coupon`, `email-invalid`, `email-not-allowed`, `email-not-valid`, `email-update-too-soon`, `elevated-permissions-needed`, `env-var-already-exists`, `exchange-rate-fetch-failed`, `expired-conference-token`, `failed-to-charge-user`, `final-invoice-negative`, `full-permission-actor-blocked-for-admin`, `full-permission-actor-not-approved`, `github-branch-empty`, `github-issue-already-exists`, `github-public-key-not-found`, `github-repository-not-found`, `github-signature-does-not-match-payload`, `github-user-not-authorized-for-issues`, `gmail-not-allowed`, `id-does-not-match`, `incompatible-billing-interval`, `incomplete-payout-billing-info`, `inconsistent-currencies`, `incorrect-pricing-modifier-prefix`, `input-json-invalid-characters`, `input-json-not-object`, `input-json-too-long`, `input-update-collision`, `insufficient-permissions`, `insufficient-permissions-to-change-field`, `insufficient-security-measures`, `insufficient-tax-country-evidence`, `integration-auth-error`, `internal-server-error`, `invalid-billing-info`, `invalid-billing-period-for-payout`, `invalid-build`, `invalid-client-key`, `invalid-collection`, `invalid-conference-login-password`, `invalid-content-type-header`, `invalid-credentials`, `invalid-git-auth-token`, `invalid-github-issue-url`, `invalid-header`, `invalid-id`, `invalid-idempotency-key`, `invalid-input`, `invalid-input-schema`, `invalid-invoice`, `invalid-invoice-type`, `invalid-issue-date`, `invalid-label-params`, `invalid-main-account-user-id`, `invalid-oauth-app`, `invalid-oauth-scope`, `invalid-one-time-invoice`, `invalid-parameter`, `invalid-payout-status`, `invalid-picture-url`, `invalid-record-key`, `invalid-request`, `invalid-resource-type`, `invalid-signature`, `invalid-subscription-plan`, `invalid-tax-number`, `invalid-tax-number-format`, `invalid-token`, `invalid-token-type`, `invalid-two-factor-code`, `invalid-two-factor-code-or-recovery-code`, `invalid-two-factor-recovery-code`, `invalid-username`, `invalid-value`, `invitation-invalid-resource-type`, `invitation-no-longer-valid`, `invoice-canceled`, `invoice-cannot-be-refunded-due-to-too-high-amount`, `invoice-incomplete`, `invoice-is-draft`, `invoice-locked`, `invoice-must-be-buffer`, `invoice-not-canceled`, `invoice-not-draft`, `invoice-not-found`, `invoice-outdated`, `invoice-paid-already`, `issue-already-connected-to-github`, `issue-not-found`, `issues-bad-request`, `issuer-not-registered`, `job-finished`, `label-already-linked`, `last-api-token`, `limit-reached`, `max-items-must-be-greater-than-zero`, `max-metamorphs-exceeded`, `max-total-charge-usd-below-minimum`, `max-total-charge-usd-must-be-greater-than-zero`, `method-not-allowed`, `migration-disabled`, `missing-actor-rights`, `missing-api-token`, `missing-billing-info`, `missing-line-items`, `missing-payment-date`, `missing-payout-billing-info`, `missing-proxy-password`, `missing-reporting-fields`, `missing-resource-name`, `missing-settings`, `missing-username`, `monthly-usage-limit-too-low`, `more-than-one-update-not-allowed`, `multiple-records-found`, `must-be-admin`, `name-not-unique`, `next-runtime-computation-failed`, `no-columns-in-exported-dataset`, `no-payment-attempt-for-refund-found`, `no-payment-method-available`, `no-team-account-seats-available`, `non-temporary-email`, `not-enough-usage-to-run-paid-actor`, `not-implemented`, `not-supported-currencies`, `o-auth-service-already-connected`, `o-auth-service-not-connected`, `oauth-resource-access-failed`, `one-time-invoice-already-marked-paid`, `only-drafts-can-be-deleted`, `operation-canceled`, `operation-not-allowed`, `operation-timed-out`, `organization-cannot-own-itself`, `organization-role-not-found`, `overlapping-payout-billing-periods`, `own-token-required`, `page-not-found`, `param-not-one-of`, `parameter-required`, `parameters-mismatched`, `password-reset-email-already-sent`, `password-reset-token-expired`, `pay-as-you-go-without-monthly-interval`, `payment-attempt-status-message-required`, `payout-already-paid`, `payout-canceled`, `payout-invalid-state`, `payout-must-be-approved-to-be-marked-paid`, `payout-not-found`, `payout-number-already-exists`, `phone-number-invalid`, `phone-number-landline`, `phone-number-opted-out`, `phone-verification-disabled`, `platform-feature-disabled`, `price-overrides-validation-failed`, `pricing-model-not-supported`, `promotional-plan-not-available`, `proxy-auth-ip-not-unique`, `public-actor-disabled`, `query-timeout`, `quoted-price-outdated`, `rate-limit-exceeded`, `recaptcha-invalid`, `recaptcha-required`, `record-not-found`, `record-not-public`, `record-or-token-not-found`, `record-too-large`, `redirect-uri-mismatch`, `reduced-plan-not-available`, `rental-charge-already-reimbursed`, `rental-not-allowed`, `request-aborted-prematurely`, `request-handled-or-locked`, `request-id-invalid`, `request-queue-duplicate-requests`, `request-too-large`, `requested-dataset-view-does-not-exist`, `resume-token-expired`, `run-failed`, `run-input-body-not-valid-json`, `run-timeout-exceeded`, `russia-is-evil`, `same-user`, `schedule-actor-not-found`, `schedule-actor-task-not-found`, `schedule-name-not-unique`, `schema-validation`, `schema-validation-error`, `schema-validation-failed`, `service-worker-registration-not-allowed`, `sign-up-method-not-allowed`, `slack-integration-not-custom`, `socket-closed`, `socket-destroyed`, `store-schema-invalid`, `store-terms-not-accepted`, `stripe-enabled`, `stripe-generic-decline`, `stripe-not-enabled`, `stripe-not-enabled-for-user`, `tagged-build-required`, `tax-country-invalid`, `tax-number-invalid`, `tax-number-validation-failed`, `taxamo-call-failed`, `taxamo-request-failed`, `testing-error`, `token-not-provided`, `too-few-versions`, `too-many-actor-tasks`, `too-many-actors`, `too-many-labels-on-resource`, `too-many-mcp-connectors`, `too-many-o-auth-apps`, `too-many-organizations`, `too-many-requests`, `too-many-schedules`, `too-many-ui-access-keys`, `too-many-user-labels`, `too-many-values`, `too-many-versions`, `too-many-webhooks`, `unexpected-route`, `unknown-build-tag`, `unknown-payment-provider`, `unsubscribe-token-invalid`, `unsupported-actor-pricing-model-for-agentic-payments`, `unsupported-content-encoding`, `unsupported-file-type-for-issue`, `unsupported-file-type-image-expected`, `unsupported-file-type-text-or-json-expected`, `unsupported-permission`, `upcoming-subscription-bill-not-up-to-date`, `user-already-exists`, `user-already-verified`, `user-creates-organizations-too-fast`, `user-disabled`, `user-email-is-disposable`, `user-email-not-set`, `user-email-not-verified`, `user-has-no-subscription`, `user-integration-not-found`, `user-is-already-invited`, `user-is-already-organization-member`, `user-is-not-member-of-organization`, `user-is-not-organization`, `user-is-organization`, `user-is-organization-owner`, `user-is-removed`, `user-not-found`, `user-not-logged-in`, `user-not-verified`, `user-or-token-not-found`, `user-plan-not-allowed-for-coupon`, `user-problem-with-card`, `user-record-not-found`, `username-already-taken`, `username-missing`, `username-not-allowed`, `username-removal-forbidden`, `username-required`, `verification-email-already-sent`, `verification-token-expired`, `version-already-exists`, `versions-size-exceeded`, `weak-password`, `x402-agentic-payment-already-finalized`, `x402-agentic-payment-insufficient-amount`, `x402-agentic-payment-malformed-token`, `x402-agentic-payment-settlement-failed`, `x402-agentic-payment-settlement-in-progress`, `x402-agentic-payment-settlement-stuck`, `x402-agentic-payment-unauthorized`, `x402-payment-required`, `zero-invoice`]

  * **message** string

    Human-readable error message describing what went wrong.

### Status 403

Forbidden - insufficient permissions to perform this action.


```json
{

  "error": {

    "type": "insufficient-permissions",

    "message": "You do not have permission to perform this action."

  }

}
```


**Schema**

* **error** object required

  * **type** ErrorType (string)

    Machine-processable error type identifier.

    **Possible values:** \[`3d-secure-auth-failed`, `access-right-already-exists`, `action-not-found`, `actor-already-rented`, `actor-can-not-be-rented`, `actor-disabled`, `actor-is-not-rented`, `actor-memory-limit-exceeded`, `actor-name-exists-new-owner`, `actor-name-not-unique`, `actor-not-found`, `actor-not-github-actor`, `actor-not-public`, `actor-permission-level-not-supported-for-agentic-payments`, `actor-review-already-exists`, `actor-run-failed`, `actor-standby-not-supported-for-agentic-payments`, `actor-task-name-not-unique`, `agentic-payment-info-retrieval-error`, `agentic-payment-information-missing`, `agentic-payment-insufficient-amount`, `agentic-payment-provider-internal-error`, `agentic-payment-provider-unauthorized`, `airtable-webhook-deprecated`, `already-subscribed-to-paid-actor`, `apify-plan-required-to-use-paid-actor`, `apify-signup-not-allowed`, `auth-method-not-supported`, `authorization-server-not-found`, `auto-issue-date-invalid`, `background-check-required`, `billing-system-error`, `black-friday-plan-expired`, `braintree-error`, `braintree-not-linked`, `braintree-operation-timed-out`, `braintree-unsupported-currency`, `build-not-found`, `build-outdated`, `cannot-add-apify-events-to-ppe-actor`, `cannot-add-multiple-pricing-infos`, `cannot-add-pricing-info-that-alters-past`, `cannot-add-second-future-pricing-info`, `cannot-build-actor-from-webhook`, `cannot-change-billing-interval`, `cannot-change-owner`, `cannot-charge-apify-event`, `cannot-charge-non-pay-per-event-actor`, `cannot-comment-as-other-user`, `cannot-copy-actor-task`, `cannot-create-payout`, `cannot-create-public-actor`, `cannot-create-tax-transaction`, `cannot-delete-critical-actor`, `cannot-delete-invoice`, `cannot-delete-paid-actor`, `cannot-disable-one-time-event-for-apify-start-event`, `cannot-disable-organization-with-enabled-members`, `cannot-disable-user-with-subscription`, `cannot-link-oauth-to-unverified-email`, `cannot-metamorph-to-pay-per-result-actor`, `cannot-modify-actor-pricing-too-frequently`, `cannot-modify-actor-pricing-with-immediate-effect`, `cannot-monetize-without-payout-billing-info`, `cannot-override-paid-actor-trial`, `cannot-permanently-delete-subscription`, `cannot-publish-actor`, `cannot-publish-actor-task`, `cannot-reduce-last-full-token`, `cannot-reimburse-more-than-original-charge`, `cannot-reimburse-non-rental-charge`, `cannot-remove-own-actor-from-recently-used`, `cannot-remove-payment-method`, `cannot-remove-pricing-info`, `cannot-remove-running-run`, `cannot-remove-user-with-public-actors`, `cannot-remove-user-with-subscription`, `cannot-remove-user-with-unpaid-invoice`, `cannot-rename-env-var`, `cannot-rent-paid-actor`, `cannot-review-own-actor`, `cannot-set-access-rights-for-owner`, `cannot-set-is-status-message-terminal`, `cannot-unpublish-critical-actor`, `cannot-unpublish-paid-actor`, `cannot-unpublish-profile`, `cannot-update-invoice-field`, `concurrent-runs-limit-exceeded`, `concurrent-update-detected`, `conference-token-not-found`, `content-encoding-forbidden-for-html`, `coupon-already-redeemed`, `coupon-expired`, `coupon-for-new-customers`, `coupon-for-subscribed-users`, `coupon-limits-are-in-conflict-with-current-limits`, `coupon-max-number-of-redemptions-reached`, `coupon-not-found`, `coupon-not-unique`, `coupons-disabled`, `create-github-issue-not-allowed`, `creator-plan-not-available`, `cron-expression-invalid`, `daily-ai-token-limit-exceeded`, `daily-publication-limit-exceeded`, `dataset-does-not-have-fields-schema`, `dataset-does-not-have-schema`, `dataset-locked`, `dataset-schema-invalid`, `dcr-not-supported`, `default-dataset-not-found`, `deleting-default-build`, `deleting-unfinished-build`, `email-already-taken`, `email-already-taken-removed-user`, `email-domain-not-allowed-for-coupon`, `email-invalid`, `email-not-allowed`, `email-not-valid`, `email-update-too-soon`, `elevated-permissions-needed`, `env-var-already-exists`, `exchange-rate-fetch-failed`, `expired-conference-token`, `failed-to-charge-user`, `final-invoice-negative`, `full-permission-actor-blocked-for-admin`, `full-permission-actor-not-approved`, `github-branch-empty`, `github-issue-already-exists`, `github-public-key-not-found`, `github-repository-not-found`, `github-signature-does-not-match-payload`, `github-user-not-authorized-for-issues`, `gmail-not-allowed`, `id-does-not-match`, `incompatible-billing-interval`, `incomplete-payout-billing-info`, `inconsistent-currencies`, `incorrect-pricing-modifier-prefix`, `input-json-invalid-characters`, `input-json-not-object`, `input-json-too-long`, `input-update-collision`, `insufficient-permissions`, `insufficient-permissions-to-change-field`, `insufficient-security-measures`, `insufficient-tax-country-evidence`, `integration-auth-error`, `internal-server-error`, `invalid-billing-info`, `invalid-billing-period-for-payout`, `invalid-build`, `invalid-client-key`, `invalid-collection`, `invalid-conference-login-password`, `invalid-content-type-header`, `invalid-credentials`, `invalid-git-auth-token`, `invalid-github-issue-url`, `invalid-header`, `invalid-id`, `invalid-idempotency-key`, `invalid-input`, `invalid-input-schema`, `invalid-invoice`, `invalid-invoice-type`, `invalid-issue-date`, `invalid-label-params`, `invalid-main-account-user-id`, `invalid-oauth-app`, `invalid-oauth-scope`, `invalid-one-time-invoice`, `invalid-parameter`, `invalid-payout-status`, `invalid-picture-url`, `invalid-record-key`, `invalid-request`, `invalid-resource-type`, `invalid-signature`, `invalid-subscription-plan`, `invalid-tax-number`, `invalid-tax-number-format`, `invalid-token`, `invalid-token-type`, `invalid-two-factor-code`, `invalid-two-factor-code-or-recovery-code`, `invalid-two-factor-recovery-code`, `invalid-username`, `invalid-value`, `invitation-invalid-resource-type`, `invitation-no-longer-valid`, `invoice-canceled`, `invoice-cannot-be-refunded-due-to-too-high-amount`, `invoice-incomplete`, `invoice-is-draft`, `invoice-locked`, `invoice-must-be-buffer`, `invoice-not-canceled`, `invoice-not-draft`, `invoice-not-found`, `invoice-outdated`, `invoice-paid-already`, `issue-already-connected-to-github`, `issue-not-found`, `issues-bad-request`, `issuer-not-registered`, `job-finished`, `label-already-linked`, `last-api-token`, `limit-reached`, `max-items-must-be-greater-than-zero`, `max-metamorphs-exceeded`, `max-total-charge-usd-below-minimum`, `max-total-charge-usd-must-be-greater-than-zero`, `method-not-allowed`, `migration-disabled`, `missing-actor-rights`, `missing-api-token`, `missing-billing-info`, `missing-line-items`, `missing-payment-date`, `missing-payout-billing-info`, `missing-proxy-password`, `missing-reporting-fields`, `missing-resource-name`, `missing-settings`, `missing-username`, `monthly-usage-limit-too-low`, `more-than-one-update-not-allowed`, `multiple-records-found`, `must-be-admin`, `name-not-unique`, `next-runtime-computation-failed`, `no-columns-in-exported-dataset`, `no-payment-attempt-for-refund-found`, `no-payment-method-available`, `no-team-account-seats-available`, `non-temporary-email`, `not-enough-usage-to-run-paid-actor`, `not-implemented`, `not-supported-currencies`, `o-auth-service-already-connected`, `o-auth-service-not-connected`, `oauth-resource-access-failed`, `one-time-invoice-already-marked-paid`, `only-drafts-can-be-deleted`, `operation-canceled`, `operation-not-allowed`, `operation-timed-out`, `organization-cannot-own-itself`, `organization-role-not-found`, `overlapping-payout-billing-periods`, `own-token-required`, `page-not-found`, `param-not-one-of`, `parameter-required`, `parameters-mismatched`, `password-reset-email-already-sent`, `password-reset-token-expired`, `pay-as-you-go-without-monthly-interval`, `payment-attempt-status-message-required`, `payout-already-paid`, `payout-canceled`, `payout-invalid-state`, `payout-must-be-approved-to-be-marked-paid`, `payout-not-found`, `payout-number-already-exists`, `phone-number-invalid`, `phone-number-landline`, `phone-number-opted-out`, `phone-verification-disabled`, `platform-feature-disabled`, `price-overrides-validation-failed`, `pricing-model-not-supported`, `promotional-plan-not-available`, `proxy-auth-ip-not-unique`, `public-actor-disabled`, `query-timeout`, `quoted-price-outdated`, `rate-limit-exceeded`, `recaptcha-invalid`, `recaptcha-required`, `record-not-found`, `record-not-public`, `record-or-token-not-found`, `record-too-large`, `redirect-uri-mismatch`, `reduced-plan-not-available`, `rental-charge-already-reimbursed`, `rental-not-allowed`, `request-aborted-prematurely`, `request-handled-or-locked`, `request-id-invalid`, `request-queue-duplicate-requests`, `request-too-large`, `requested-dataset-view-does-not-exist`, `resume-token-expired`, `run-failed`, `run-input-body-not-valid-json`, `run-timeout-exceeded`, `russia-is-evil`, `same-user`, `schedule-actor-not-found`, `schedule-actor-task-not-found`, `schedule-name-not-unique`, `schema-validation`, `schema-validation-error`, `schema-validation-failed`, `service-worker-registration-not-allowed`, `sign-up-method-not-allowed`, `slack-integration-not-custom`, `socket-closed`, `socket-destroyed`, `store-schema-invalid`, `store-terms-not-accepted`, `stripe-enabled`, `stripe-generic-decline`, `stripe-not-enabled`, `stripe-not-enabled-for-user`, `tagged-build-required`, `tax-country-invalid`, `tax-number-invalid`, `tax-number-validation-failed`, `taxamo-call-failed`, `taxamo-request-failed`, `testing-error`, `token-not-provided`, `too-few-versions`, `too-many-actor-tasks`, `too-many-actors`, `too-many-labels-on-resource`, `too-many-mcp-connectors`, `too-many-o-auth-apps`, `too-many-organizations`, `too-many-requests`, `too-many-schedules`, `too-many-ui-access-keys`, `too-many-user-labels`, `too-many-values`, `too-many-versions`, `too-many-webhooks`, `unexpected-route`, `unknown-build-tag`, `unknown-payment-provider`, `unsubscribe-token-invalid`, `unsupported-actor-pricing-model-for-agentic-payments`, `unsupported-content-encoding`, `unsupported-file-type-for-issue`, `unsupported-file-type-image-expected`, `unsupported-file-type-text-or-json-expected`, `unsupported-permission`, `upcoming-subscription-bill-not-up-to-date`, `user-already-exists`, `user-already-verified`, `user-creates-organizations-too-fast`, `user-disabled`, `user-email-is-disposable`, `user-email-not-set`, `user-email-not-verified`, `user-has-no-subscription`, `user-integration-not-found`, `user-is-already-invited`, `user-is-already-organization-member`, `user-is-not-member-of-organization`, `user-is-not-organization`, `user-is-organization`, `user-is-organization-owner`, `user-is-removed`, `user-not-found`, `user-not-logged-in`, `user-not-verified`, `user-or-token-not-found`, `user-plan-not-allowed-for-coupon`, `user-problem-with-card`, `user-record-not-found`, `username-already-taken`, `username-missing`, `username-not-allowed`, `username-removal-forbidden`, `username-required`, `verification-email-already-sent`, `verification-token-expired`, `version-already-exists`, `versions-size-exceeded`, `weak-password`, `x402-agentic-payment-already-finalized`, `x402-agentic-payment-insufficient-amount`, `x402-agentic-payment-malformed-token`, `x402-agentic-payment-settlement-failed`, `x402-agentic-payment-settlement-in-progress`, `x402-agentic-payment-settlement-stuck`, `x402-agentic-payment-unauthorized`, `x402-payment-required`, `zero-invoice`]

  * **message** string

    Human-readable error message describing what went wrong.


```json
{

  "error": {

    "type": "insufficient-permissions",

    "message": "You do not have permission to perform this action."

  }

}
```


**Schema**

* **error** object required

  * **type** ErrorType (string)

    Machine-processable error type identifier.

    **Possible values:** \[`3d-secure-auth-failed`, `access-right-already-exists`, `action-not-found`, `actor-already-rented`, `actor-can-not-be-rented`, `actor-disabled`, `actor-is-not-rented`, `actor-memory-limit-exceeded`, `actor-name-exists-new-owner`, `actor-name-not-unique`, `actor-not-found`, `actor-not-github-actor`, `actor-not-public`, `actor-permission-level-not-supported-for-agentic-payments`, `actor-review-already-exists`, `actor-run-failed`, `actor-standby-not-supported-for-agentic-payments`, `actor-task-name-not-unique`, `agentic-payment-info-retrieval-error`, `agentic-payment-information-missing`, `agentic-payment-insufficient-amount`, `agentic-payment-provider-internal-error`, `agentic-payment-provider-unauthorized`, `airtable-webhook-deprecated`, `already-subscribed-to-paid-actor`, `apify-plan-required-to-use-paid-actor`, `apify-signup-not-allowed`, `auth-method-not-supported`, `authorization-server-not-found`, `auto-issue-date-invalid`, `background-check-required`, `billing-system-error`, `black-friday-plan-expired`, `braintree-error`, `braintree-not-linked`, `braintree-operation-timed-out`, `braintree-unsupported-currency`, `build-not-found`, `build-outdated`, `cannot-add-apify-events-to-ppe-actor`, `cannot-add-multiple-pricing-infos`, `cannot-add-pricing-info-that-alters-past`, `cannot-add-second-future-pricing-info`, `cannot-build-actor-from-webhook`, `cannot-change-billing-interval`, `cannot-change-owner`, `cannot-charge-apify-event`, `cannot-charge-non-pay-per-event-actor`, `cannot-comment-as-other-user`, `cannot-copy-actor-task`, `cannot-create-payout`, `cannot-create-public-actor`, `cannot-create-tax-transaction`, `cannot-delete-critical-actor`, `cannot-delete-invoice`, `cannot-delete-paid-actor`, `cannot-disable-one-time-event-for-apify-start-event`, `cannot-disable-organization-with-enabled-members`, `cannot-disable-user-with-subscription`, `cannot-link-oauth-to-unverified-email`, `cannot-metamorph-to-pay-per-result-actor`, `cannot-modify-actor-pricing-too-frequently`, `cannot-modify-actor-pricing-with-immediate-effect`, `cannot-monetize-without-payout-billing-info`, `cannot-override-paid-actor-trial`, `cannot-permanently-delete-subscription`, `cannot-publish-actor`, `cannot-publish-actor-task`, `cannot-reduce-last-full-token`, `cannot-reimburse-more-than-original-charge`, `cannot-reimburse-non-rental-charge`, `cannot-remove-own-actor-from-recently-used`, `cannot-remove-payment-method`, `cannot-remove-pricing-info`, `cannot-remove-running-run`, `cannot-remove-user-with-public-actors`, `cannot-remove-user-with-subscription`, `cannot-remove-user-with-unpaid-invoice`, `cannot-rename-env-var`, `cannot-rent-paid-actor`, `cannot-review-own-actor`, `cannot-set-access-rights-for-owner`, `cannot-set-is-status-message-terminal`, `cannot-unpublish-critical-actor`, `cannot-unpublish-paid-actor`, `cannot-unpublish-profile`, `cannot-update-invoice-field`, `concurrent-runs-limit-exceeded`, `concurrent-update-detected`, `conference-token-not-found`, `content-encoding-forbidden-for-html`, `coupon-already-redeemed`, `coupon-expired`, `coupon-for-new-customers`, `coupon-for-subscribed-users`, `coupon-limits-are-in-conflict-with-current-limits`, `coupon-max-number-of-redemptions-reached`, `coupon-not-found`, `coupon-not-unique`, `coupons-disabled`, `create-github-issue-not-allowed`, `creator-plan-not-available`, `cron-expression-invalid`, `daily-ai-token-limit-exceeded`, `daily-publication-limit-exceeded`, `dataset-does-not-have-fields-schema`, `dataset-does-not-have-schema`, `dataset-locked`, `dataset-schema-invalid`, `dcr-not-supported`, `default-dataset-not-found`, `deleting-default-build`, `deleting-unfinished-build`, `email-already-taken`, `email-already-taken-removed-user`, `email-domain-not-allowed-for-coupon`, `email-invalid`, `email-not-allowed`, `email-not-valid`, `email-update-too-soon`, `elevated-permissions-needed`, `env-var-already-exists`, `exchange-rate-fetch-failed`, `expired-conference-token`, `failed-to-charge-user`, `final-invoice-negative`, `full-permission-actor-blocked-for-admin`, `full-permission-actor-not-approved`, `github-branch-empty`, `github-issue-already-exists`, `github-public-key-not-found`, `github-repository-not-found`, `github-signature-does-not-match-payload`, `github-user-not-authorized-for-issues`, `gmail-not-allowed`, `id-does-not-match`, `incompatible-billing-interval`, `incomplete-payout-billing-info`, `inconsistent-currencies`, `incorrect-pricing-modifier-prefix`, `input-json-invalid-characters`, `input-json-not-object`, `input-json-too-long`, `input-update-collision`, `insufficient-permissions`, `insufficient-permissions-to-change-field`, `insufficient-security-measures`, `insufficient-tax-country-evidence`, `integration-auth-error`, `internal-server-error`, `invalid-billing-info`, `invalid-billing-period-for-payout`, `invalid-build`, `invalid-client-key`, `invalid-collection`, `invalid-conference-login-password`, `invalid-content-type-header`, `invalid-credentials`, `invalid-git-auth-token`, `invalid-github-issue-url`, `invalid-header`, `invalid-id`, `invalid-idempotency-key`, `invalid-input`, `invalid-input-schema`, `invalid-invoice`, `invalid-invoice-type`, `invalid-issue-date`, `invalid-label-params`, `invalid-main-account-user-id`, `invalid-oauth-app`, `invalid-oauth-scope`, `invalid-one-time-invoice`, `invalid-parameter`, `invalid-payout-status`, `invalid-picture-url`, `invalid-record-key`, `invalid-request`, `invalid-resource-type`, `invalid-signature`, `invalid-subscription-plan`, `invalid-tax-number`, `invalid-tax-number-format`, `invalid-token`, `invalid-token-type`, `invalid-two-factor-code`, `invalid-two-factor-code-or-recovery-code`, `invalid-two-factor-recovery-code`, `invalid-username`, `invalid-value`, `invitation-invalid-resource-type`, `invitation-no-longer-valid`, `invoice-canceled`, `invoice-cannot-be-refunded-due-to-too-high-amount`, `invoice-incomplete`, `invoice-is-draft`, `invoice-locked`, `invoice-must-be-buffer`, `invoice-not-canceled`, `invoice-not-draft`, `invoice-not-found`, `invoice-outdated`, `invoice-paid-already`, `issue-already-connected-to-github`, `issue-not-found`, `issues-bad-request`, `issuer-not-registered`, `job-finished`, `label-already-linked`, `last-api-token`, `limit-reached`, `max-items-must-be-greater-than-zero`, `max-metamorphs-exceeded`, `max-total-charge-usd-below-minimum`, `max-total-charge-usd-must-be-greater-than-zero`, `method-not-allowed`, `migration-disabled`, `missing-actor-rights`, `missing-api-token`, `missing-billing-info`, `missing-line-items`, `missing-payment-date`, `missing-payout-billing-info`, `missing-proxy-password`, `missing-reporting-fields`, `missing-resource-name`, `missing-settings`, `missing-username`, `monthly-usage-limit-too-low`, `more-than-one-update-not-allowed`, `multiple-records-found`, `must-be-admin`, `name-not-unique`, `next-runtime-computation-failed`, `no-columns-in-exported-dataset`, `no-payment-attempt-for-refund-found`, `no-payment-method-available`, `no-team-account-seats-available`, `non-temporary-email`, `not-enough-usage-to-run-paid-actor`, `not-implemented`, `not-supported-currencies`, `o-auth-service-already-connected`, `o-auth-service-not-connected`, `oauth-resource-access-failed`, `one-time-invoice-already-marked-paid`, `only-drafts-can-be-deleted`, `operation-canceled`, `operation-not-allowed`, `operation-timed-out`, `organization-cannot-own-itself`, `organization-role-not-found`, `overlapping-payout-billing-periods`, `own-token-required`, `page-not-found`, `param-not-one-of`, `parameter-required`, `parameters-mismatched`, `password-reset-email-already-sent`, `password-reset-token-expired`, `pay-as-you-go-without-monthly-interval`, `payment-attempt-status-message-required`, `payout-already-paid`, `payout-canceled`, `payout-invalid-state`, `payout-must-be-approved-to-be-marked-paid`, `payout-not-found`, `payout-number-already-exists`, `phone-number-invalid`, `phone-number-landline`, `phone-number-opted-out`, `phone-verification-disabled`, `platform-feature-disabled`, `price-overrides-validation-failed`, `pricing-model-not-supported`, `promotional-plan-not-available`, `proxy-auth-ip-not-unique`, `public-actor-disabled`, `query-timeout`, `quoted-price-outdated`, `rate-limit-exceeded`, `recaptcha-invalid`, `recaptcha-required`, `record-not-found`, `record-not-public`, `record-or-token-not-found`, `record-too-large`, `redirect-uri-mismatch`, `reduced-plan-not-available`, `rental-charge-already-reimbursed`, `rental-not-allowed`, `request-aborted-prematurely`, `request-handled-or-locked`, `request-id-invalid`, `request-queue-duplicate-requests`, `request-too-large`, `requested-dataset-view-does-not-exist`, `resume-token-expired`, `run-failed`, `run-input-body-not-valid-json`, `run-timeout-exceeded`, `russia-is-evil`, `same-user`, `schedule-actor-not-found`, `schedule-actor-task-not-found`, `schedule-name-not-unique`, `schema-validation`, `schema-validation-error`, `schema-validation-failed`, `service-worker-registration-not-allowed`, `sign-up-method-not-allowed`, `slack-integration-not-custom`, `socket-closed`, `socket-destroyed`, `store-schema-invalid`, `store-terms-not-accepted`, `stripe-enabled`, `stripe-generic-decline`, `stripe-not-enabled`, `stripe-not-enabled-for-user`, `tagged-build-required`, `tax-country-invalid`, `tax-number-invalid`, `tax-number-validation-failed`, `taxamo-call-failed`, `taxamo-request-failed`, `testing-error`, `token-not-provided`, `too-few-versions`, `too-many-actor-tasks`, `too-many-actors`, `too-many-labels-on-resource`, `too-many-mcp-connectors`, `too-many-o-auth-apps`, `too-many-organizations`, `too-many-requests`, `too-many-schedules`, `too-many-ui-access-keys`, `too-many-user-labels`, `too-many-values`, `too-many-versions`, `too-many-webhooks`, `unexpected-route`, `unknown-build-tag`, `unknown-payment-provider`, `unsubscribe-token-invalid`, `unsupported-actor-pricing-model-for-agentic-payments`, `unsupported-content-encoding`, `unsupported-file-type-for-issue`, `unsupported-file-type-image-expected`, `unsupported-file-type-text-or-json-expected`, `unsupported-permission`, `upcoming-subscription-bill-not-up-to-date`, `user-already-exists`, `user-already-verified`, `user-creates-organizations-too-fast`, `user-disabled`, `user-email-is-disposable`, `user-email-not-set`, `user-email-not-verified`, `user-has-no-subscription`, `user-integration-not-found`, `user-is-already-invited`, `user-is-already-organization-member`, `user-is-not-member-of-organization`, `user-is-not-organization`, `user-is-organization`, `user-is-organization-owner`, `user-is-removed`, `user-not-found`, `user-not-logged-in`, `user-not-verified`, `user-or-token-not-found`, `user-plan-not-allowed-for-coupon`, `user-problem-with-card`, `user-record-not-found`, `username-already-taken`, `username-missing`, `username-not-allowed`, `username-removal-forbidden`, `username-required`, `verification-email-already-sent`, `verification-token-expired`, `version-already-exists`, `versions-size-exceeded`, `weak-password`, `x402-agentic-payment-already-finalized`, `x402-agentic-payment-insufficient-amount`, `x402-agentic-payment-malformed-token`, `x402-agentic-payment-settlement-failed`, `x402-agentic-payment-settlement-in-progress`, `x402-agentic-payment-settlement-stuck`, `x402-agentic-payment-unauthorized`, `x402-payment-required`, `zero-invoice`]

  * **message** string

    Human-readable error message describing what went wrong.

### Status 404

Not found - the requested resource does not exist.


```json
{

  "error": {

    "type": "record-not-found",

    "message": "The requested resource was not found."

  }

}
```


**Schema**

* **error** object required

  * **type** ErrorType (string)

    Machine-processable error type identifier.

    **Possible values:** \[`3d-secure-auth-failed`, `access-right-already-exists`, `action-not-found`, `actor-already-rented`, `actor-can-not-be-rented`, `actor-disabled`, `actor-is-not-rented`, `actor-memory-limit-exceeded`, `actor-name-exists-new-owner`, `actor-name-not-unique`, `actor-not-found`, `actor-not-github-actor`, `actor-not-public`, `actor-permission-level-not-supported-for-agentic-payments`, `actor-review-already-exists`, `actor-run-failed`, `actor-standby-not-supported-for-agentic-payments`, `actor-task-name-not-unique`, `agentic-payment-info-retrieval-error`, `agentic-payment-information-missing`, `agentic-payment-insufficient-amount`, `agentic-payment-provider-internal-error`, `agentic-payment-provider-unauthorized`, `airtable-webhook-deprecated`, `already-subscribed-to-paid-actor`, `apify-plan-required-to-use-paid-actor`, `apify-signup-not-allowed`, `auth-method-not-supported`, `authorization-server-not-found`, `auto-issue-date-invalid`, `background-check-required`, `billing-system-error`, `black-friday-plan-expired`, `braintree-error`, `braintree-not-linked`, `braintree-operation-timed-out`, `braintree-unsupported-currency`, `build-not-found`, `build-outdated`, `cannot-add-apify-events-to-ppe-actor`, `cannot-add-multiple-pricing-infos`, `cannot-add-pricing-info-that-alters-past`, `cannot-add-second-future-pricing-info`, `cannot-build-actor-from-webhook`, `cannot-change-billing-interval`, `cannot-change-owner`, `cannot-charge-apify-event`, `cannot-charge-non-pay-per-event-actor`, `cannot-comment-as-other-user`, `cannot-copy-actor-task`, `cannot-create-payout`, `cannot-create-public-actor`, `cannot-create-tax-transaction`, `cannot-delete-critical-actor`, `cannot-delete-invoice`, `cannot-delete-paid-actor`, `cannot-disable-one-time-event-for-apify-start-event`, `cannot-disable-organization-with-enabled-members`, `cannot-disable-user-with-subscription`, `cannot-link-oauth-to-unverified-email`, `cannot-metamorph-to-pay-per-result-actor`, `cannot-modify-actor-pricing-too-frequently`, `cannot-modify-actor-pricing-with-immediate-effect`, `cannot-monetize-without-payout-billing-info`, `cannot-override-paid-actor-trial`, `cannot-permanently-delete-subscription`, `cannot-publish-actor`, `cannot-publish-actor-task`, `cannot-reduce-last-full-token`, `cannot-reimburse-more-than-original-charge`, `cannot-reimburse-non-rental-charge`, `cannot-remove-own-actor-from-recently-used`, `cannot-remove-payment-method`, `cannot-remove-pricing-info`, `cannot-remove-running-run`, `cannot-remove-user-with-public-actors`, `cannot-remove-user-with-subscription`, `cannot-remove-user-with-unpaid-invoice`, `cannot-rename-env-var`, `cannot-rent-paid-actor`, `cannot-review-own-actor`, `cannot-set-access-rights-for-owner`, `cannot-set-is-status-message-terminal`, `cannot-unpublish-critical-actor`, `cannot-unpublish-paid-actor`, `cannot-unpublish-profile`, `cannot-update-invoice-field`, `concurrent-runs-limit-exceeded`, `concurrent-update-detected`, `conference-token-not-found`, `content-encoding-forbidden-for-html`, `coupon-already-redeemed`, `coupon-expired`, `coupon-for-new-customers`, `coupon-for-subscribed-users`, `coupon-limits-are-in-conflict-with-current-limits`, `coupon-max-number-of-redemptions-reached`, `coupon-not-found`, `coupon-not-unique`, `coupons-disabled`, `create-github-issue-not-allowed`, `creator-plan-not-available`, `cron-expression-invalid`, `daily-ai-token-limit-exceeded`, `daily-publication-limit-exceeded`, `dataset-does-not-have-fields-schema`, `dataset-does-not-have-schema`, `dataset-locked`, `dataset-schema-invalid`, `dcr-not-supported`, `default-dataset-not-found`, `deleting-default-build`, `deleting-unfinished-build`, `email-already-taken`, `email-already-taken-removed-user`, `email-domain-not-allowed-for-coupon`, `email-invalid`, `email-not-allowed`, `email-not-valid`, `email-update-too-soon`, `elevated-permissions-needed`, `env-var-already-exists`, `exchange-rate-fetch-failed`, `expired-conference-token`, `failed-to-charge-user`, `final-invoice-negative`, `full-permission-actor-blocked-for-admin`, `full-permission-actor-not-approved`, `github-branch-empty`, `github-issue-already-exists`, `github-public-key-not-found`, `github-repository-not-found`, `github-signature-does-not-match-payload`, `github-user-not-authorized-for-issues`, `gmail-not-allowed`, `id-does-not-match`, `incompatible-billing-interval`, `incomplete-payout-billing-info`, `inconsistent-currencies`, `incorrect-pricing-modifier-prefix`, `input-json-invalid-characters`, `input-json-not-object`, `input-json-too-long`, `input-update-collision`, `insufficient-permissions`, `insufficient-permissions-to-change-field`, `insufficient-security-measures`, `insufficient-tax-country-evidence`, `integration-auth-error`, `internal-server-error`, `invalid-billing-info`, `invalid-billing-period-for-payout`, `invalid-build`, `invalid-client-key`, `invalid-collection`, `invalid-conference-login-password`, `invalid-content-type-header`, `invalid-credentials`, `invalid-git-auth-token`, `invalid-github-issue-url`, `invalid-header`, `invalid-id`, `invalid-idempotency-key`, `invalid-input`, `invalid-input-schema`, `invalid-invoice`, `invalid-invoice-type`, `invalid-issue-date`, `invalid-label-params`, `invalid-main-account-user-id`, `invalid-oauth-app`, `invalid-oauth-scope`, `invalid-one-time-invoice`, `invalid-parameter`, `invalid-payout-status`, `invalid-picture-url`, `invalid-record-key`, `invalid-request`, `invalid-resource-type`, `invalid-signature`, `invalid-subscription-plan`, `invalid-tax-number`, `invalid-tax-number-format`, `invalid-token`, `invalid-token-type`, `invalid-two-factor-code`, `invalid-two-factor-code-or-recovery-code`, `invalid-two-factor-recovery-code`, `invalid-username`, `invalid-value`, `invitation-invalid-resource-type`, `invitation-no-longer-valid`, `invoice-canceled`, `invoice-cannot-be-refunded-due-to-too-high-amount`, `invoice-incomplete`, `invoice-is-draft`, `invoice-locked`, `invoice-must-be-buffer`, `invoice-not-canceled`, `invoice-not-draft`, `invoice-not-found`, `invoice-outdated`, `invoice-paid-already`, `issue-already-connected-to-github`, `issue-not-found`, `issues-bad-request`, `issuer-not-registered`, `job-finished`, `label-already-linked`, `last-api-token`, `limit-reached`, `max-items-must-be-greater-than-zero`, `max-metamorphs-exceeded`, `max-total-charge-usd-below-minimum`, `max-total-charge-usd-must-be-greater-than-zero`, `method-not-allowed`, `migration-disabled`, `missing-actor-rights`, `missing-api-token`, `missing-billing-info`, `missing-line-items`, `missing-payment-date`, `missing-payout-billing-info`, `missing-proxy-password`, `missing-reporting-fields`, `missing-resource-name`, `missing-settings`, `missing-username`, `monthly-usage-limit-too-low`, `more-than-one-update-not-allowed`, `multiple-records-found`, `must-be-admin`, `name-not-unique`, `next-runtime-computation-failed`, `no-columns-in-exported-dataset`, `no-payment-attempt-for-refund-found`, `no-payment-method-available`, `no-team-account-seats-available`, `non-temporary-email`, `not-enough-usage-to-run-paid-actor`, `not-implemented`, `not-supported-currencies`, `o-auth-service-already-connected`, `o-auth-service-not-connected`, `oauth-resource-access-failed`, `one-time-invoice-already-marked-paid`, `only-drafts-can-be-deleted`, `operation-canceled`, `operation-not-allowed`, `operation-timed-out`, `organization-cannot-own-itself`, `organization-role-not-found`, `overlapping-payout-billing-periods`, `own-token-required`, `page-not-found`, `param-not-one-of`, `parameter-required`, `parameters-mismatched`, `password-reset-email-already-sent`, `password-reset-token-expired`, `pay-as-you-go-without-monthly-interval`, `payment-attempt-status-message-required`, `payout-already-paid`, `payout-canceled`, `payout-invalid-state`, `payout-must-be-approved-to-be-marked-paid`, `payout-not-found`, `payout-number-already-exists`, `phone-number-invalid`, `phone-number-landline`, `phone-number-opted-out`, `phone-verification-disabled`, `platform-feature-disabled`, `price-overrides-validation-failed`, `pricing-model-not-supported`, `promotional-plan-not-available`, `proxy-auth-ip-not-unique`, `public-actor-disabled`, `query-timeout`, `quoted-price-outdated`, `rate-limit-exceeded`, `recaptcha-invalid`, `recaptcha-required`, `record-not-found`, `record-not-public`, `record-or-token-not-found`, `record-too-large`, `redirect-uri-mismatch`, `reduced-plan-not-available`, `rental-charge-already-reimbursed`, `rental-not-allowed`, `request-aborted-prematurely`, `request-handled-or-locked`, `request-id-invalid`, `request-queue-duplicate-requests`, `request-too-large`, `requested-dataset-view-does-not-exist`, `resume-token-expired`, `run-failed`, `run-input-body-not-valid-json`, `run-timeout-exceeded`, `russia-is-evil`, `same-user`, `schedule-actor-not-found`, `schedule-actor-task-not-found`, `schedule-name-not-unique`, `schema-validation`, `schema-validation-error`, `schema-validation-failed`, `service-worker-registration-not-allowed`, `sign-up-method-not-allowed`, `slack-integration-not-custom`, `socket-closed`, `socket-destroyed`, `store-schema-invalid`, `store-terms-not-accepted`, `stripe-enabled`, `stripe-generic-decline`, `stripe-not-enabled`, `stripe-not-enabled-for-user`, `tagged-build-required`, `tax-country-invalid`, `tax-number-invalid`, `tax-number-validation-failed`, `taxamo-call-failed`, `taxamo-request-failed`, `testing-error`, `token-not-provided`, `too-few-versions`, `too-many-actor-tasks`, `too-many-actors`, `too-many-labels-on-resource`, `too-many-mcp-connectors`, `too-many-o-auth-apps`, `too-many-organizations`, `too-many-requests`, `too-many-schedules`, `too-many-ui-access-keys`, `too-many-user-labels`, `too-many-values`, `too-many-versions`, `too-many-webhooks`, `unexpected-route`, `unknown-build-tag`, `unknown-payment-provider`, `unsubscribe-token-invalid`, `unsupported-actor-pricing-model-for-agentic-payments`, `unsupported-content-encoding`, `unsupported-file-type-for-issue`, `unsupported-file-type-image-expected`, `unsupported-file-type-text-or-json-expected`, `unsupported-permission`, `upcoming-subscription-bill-not-up-to-date`, `user-already-exists`, `user-already-verified`, `user-creates-organizations-too-fast`, `user-disabled`, `user-email-is-disposable`, `user-email-not-set`, `user-email-not-verified`, `user-has-no-subscription`, `user-integration-not-found`, `user-is-already-invited`, `user-is-already-organization-member`, `user-is-not-member-of-organization`, `user-is-not-organization`, `user-is-organization`, `user-is-organization-owner`, `user-is-removed`, `user-not-found`, `user-not-logged-in`, `user-not-verified`, `user-or-token-not-found`, `user-plan-not-allowed-for-coupon`, `user-problem-with-card`, `user-record-not-found`, `username-already-taken`, `username-missing`, `username-not-allowed`, `username-removal-forbidden`, `username-required`, `verification-email-already-sent`, `verification-token-expired`, `version-already-exists`, `versions-size-exceeded`, `weak-password`, `x402-agentic-payment-already-finalized`, `x402-agentic-payment-insufficient-amount`, `x402-agentic-payment-malformed-token`, `x402-agentic-payment-settlement-failed`, `x402-agentic-payment-settlement-in-progress`, `x402-agentic-payment-settlement-stuck`, `x402-agentic-payment-unauthorized`, `x402-payment-required`, `zero-invoice`]

  * **message** string

    Human-readable error message describing what went wrong.


```json
{

  "error": {

    "type": "record-not-found",

    "message": "The requested resource was not found."

  }

}
```


**Schema**

* **error** object required

  * **type** ErrorType (string)

    Machine-processable error type identifier.

    **Possible values:** \[`3d-secure-auth-failed`, `access-right-already-exists`, `action-not-found`, `actor-already-rented`, `actor-can-not-be-rented`, `actor-disabled`, `actor-is-not-rented`, `actor-memory-limit-exceeded`, `actor-name-exists-new-owner`, `actor-name-not-unique`, `actor-not-found`, `actor-not-github-actor`, `actor-not-public`, `actor-permission-level-not-supported-for-agentic-payments`, `actor-review-already-exists`, `actor-run-failed`, `actor-standby-not-supported-for-agentic-payments`, `actor-task-name-not-unique`, `agentic-payment-info-retrieval-error`, `agentic-payment-information-missing`, `agentic-payment-insufficient-amount`, `agentic-payment-provider-internal-error`, `agentic-payment-provider-unauthorized`, `airtable-webhook-deprecated`, `already-subscribed-to-paid-actor`, `apify-plan-required-to-use-paid-actor`, `apify-signup-not-allowed`, `auth-method-not-supported`, `authorization-server-not-found`, `auto-issue-date-invalid`, `background-check-required`, `billing-system-error`, `black-friday-plan-expired`, `braintree-error`, `braintree-not-linked`, `braintree-operation-timed-out`, `braintree-unsupported-currency`, `build-not-found`, `build-outdated`, `cannot-add-apify-events-to-ppe-actor`, `cannot-add-multiple-pricing-infos`, `cannot-add-pricing-info-that-alters-past`, `cannot-add-second-future-pricing-info`, `cannot-build-actor-from-webhook`, `cannot-change-billing-interval`, `cannot-change-owner`, `cannot-charge-apify-event`, `cannot-charge-non-pay-per-event-actor`, `cannot-comment-as-other-user`, `cannot-copy-actor-task`, `cannot-create-payout`, `cannot-create-public-actor`, `cannot-create-tax-transaction`, `cannot-delete-critical-actor`, `cannot-delete-invoice`, `cannot-delete-paid-actor`, `cannot-disable-one-time-event-for-apify-start-event`, `cannot-disable-organization-with-enabled-members`, `cannot-disable-user-with-subscription`, `cannot-link-oauth-to-unverified-email`, `cannot-metamorph-to-pay-per-result-actor`, `cannot-modify-actor-pricing-too-frequently`, `cannot-modify-actor-pricing-with-immediate-effect`, `cannot-monetize-without-payout-billing-info`, `cannot-override-paid-actor-trial`, `cannot-permanently-delete-subscription`, `cannot-publish-actor`, `cannot-publish-actor-task`, `cannot-reduce-last-full-token`, `cannot-reimburse-more-than-original-charge`, `cannot-reimburse-non-rental-charge`, `cannot-remove-own-actor-from-recently-used`, `cannot-remove-payment-method`, `cannot-remove-pricing-info`, `cannot-remove-running-run`, `cannot-remove-user-with-public-actors`, `cannot-remove-user-with-subscription`, `cannot-remove-user-with-unpaid-invoice`, `cannot-rename-env-var`, `cannot-rent-paid-actor`, `cannot-review-own-actor`, `cannot-set-access-rights-for-owner`, `cannot-set-is-status-message-terminal`, `cannot-unpublish-critical-actor`, `cannot-unpublish-paid-actor`, `cannot-unpublish-profile`, `cannot-update-invoice-field`, `concurrent-runs-limit-exceeded`, `concurrent-update-detected`, `conference-token-not-found`, `content-encoding-forbidden-for-html`, `coupon-already-redeemed`, `coupon-expired`, `coupon-for-new-customers`, `coupon-for-subscribed-users`, `coupon-limits-are-in-conflict-with-current-limits`, `coupon-max-number-of-redemptions-reached`, `coupon-not-found`, `coupon-not-unique`, `coupons-disabled`, `create-github-issue-not-allowed`, `creator-plan-not-available`, `cron-expression-invalid`, `daily-ai-token-limit-exceeded`, `daily-publication-limit-exceeded`, `dataset-does-not-have-fields-schema`, `dataset-does-not-have-schema`, `dataset-locked`, `dataset-schema-invalid`, `dcr-not-supported`, `default-dataset-not-found`, `deleting-default-build`, `deleting-unfinished-build`, `email-already-taken`, `email-already-taken-removed-user`, `email-domain-not-allowed-for-coupon`, `email-invalid`, `email-not-allowed`, `email-not-valid`, `email-update-too-soon`, `elevated-permissions-needed`, `env-var-already-exists`, `exchange-rate-fetch-failed`, `expired-conference-token`, `failed-to-charge-user`, `final-invoice-negative`, `full-permission-actor-blocked-for-admin`, `full-permission-actor-not-approved`, `github-branch-empty`, `github-issue-already-exists`, `github-public-key-not-found`, `github-repository-not-found`, `github-signature-does-not-match-payload`, `github-user-not-authorized-for-issues`, `gmail-not-allowed`, `id-does-not-match`, `incompatible-billing-interval`, `incomplete-payout-billing-info`, `inconsistent-currencies`, `incorrect-pricing-modifier-prefix`, `input-json-invalid-characters`, `input-json-not-object`, `input-json-too-long`, `input-update-collision`, `insufficient-permissions`, `insufficient-permissions-to-change-field`, `insufficient-security-measures`, `insufficient-tax-country-evidence`, `integration-auth-error`, `internal-server-error`, `invalid-billing-info`, `invalid-billing-period-for-payout`, `invalid-build`, `invalid-client-key`, `invalid-collection`, `invalid-conference-login-password`, `invalid-content-type-header`, `invalid-credentials`, `invalid-git-auth-token`, `invalid-github-issue-url`, `invalid-header`, `invalid-id`, `invalid-idempotency-key`, `invalid-input`, `invalid-input-schema`, `invalid-invoice`, `invalid-invoice-type`, `invalid-issue-date`, `invalid-label-params`, `invalid-main-account-user-id`, `invalid-oauth-app`, `invalid-oauth-scope`, `invalid-one-time-invoice`, `invalid-parameter`, `invalid-payout-status`, `invalid-picture-url`, `invalid-record-key`, `invalid-request`, `invalid-resource-type`, `invalid-signature`, `invalid-subscription-plan`, `invalid-tax-number`, `invalid-tax-number-format`, `invalid-token`, `invalid-token-type`, `invalid-two-factor-code`, `invalid-two-factor-code-or-recovery-code`, `invalid-two-factor-recovery-code`, `invalid-username`, `invalid-value`, `invitation-invalid-resource-type`, `invitation-no-longer-valid`, `invoice-canceled`, `invoice-cannot-be-refunded-due-to-too-high-amount`, `invoice-incomplete`, `invoice-is-draft`, `invoice-locked`, `invoice-must-be-buffer`, `invoice-not-canceled`, `invoice-not-draft`, `invoice-not-found`, `invoice-outdated`, `invoice-paid-already`, `issue-already-connected-to-github`, `issue-not-found`, `issues-bad-request`, `issuer-not-registered`, `job-finished`, `label-already-linked`, `last-api-token`, `limit-reached`, `max-items-must-be-greater-than-zero`, `max-metamorphs-exceeded`, `max-total-charge-usd-below-minimum`, `max-total-charge-usd-must-be-greater-than-zero`, `method-not-allowed`, `migration-disabled`, `missing-actor-rights`, `missing-api-token`, `missing-billing-info`, `missing-line-items`, `missing-payment-date`, `missing-payout-billing-info`, `missing-proxy-password`, `missing-reporting-fields`, `missing-resource-name`, `missing-settings`, `missing-username`, `monthly-usage-limit-too-low`, `more-than-one-update-not-allowed`, `multiple-records-found`, `must-be-admin`, `name-not-unique`, `next-runtime-computation-failed`, `no-columns-in-exported-dataset`, `no-payment-attempt-for-refund-found`, `no-payment-method-available`, `no-team-account-seats-available`, `non-temporary-email`, `not-enough-usage-to-run-paid-actor`, `not-implemented`, `not-supported-currencies`, `o-auth-service-already-connected`, `o-auth-service-not-connected`, `oauth-resource-access-failed`, `one-time-invoice-already-marked-paid`, `only-drafts-can-be-deleted`, `operation-canceled`, `operation-not-allowed`, `operation-timed-out`, `organization-cannot-own-itself`, `organization-role-not-found`, `overlapping-payout-billing-periods`, `own-token-required`, `page-not-found`, `param-not-one-of`, `parameter-required`, `parameters-mismatched`, `password-reset-email-already-sent`, `password-reset-token-expired`, `pay-as-you-go-without-monthly-interval`, `payment-attempt-status-message-required`, `payout-already-paid`, `payout-canceled`, `payout-invalid-state`, `payout-must-be-approved-to-be-marked-paid`, `payout-not-found`, `payout-number-already-exists`, `phone-number-invalid`, `phone-number-landline`, `phone-number-opted-out`, `phone-verification-disabled`, `platform-feature-disabled`, `price-overrides-validation-failed`, `pricing-model-not-supported`, `promotional-plan-not-available`, `proxy-auth-ip-not-unique`, `public-actor-disabled`, `query-timeout`, `quoted-price-outdated`, `rate-limit-exceeded`, `recaptcha-invalid`, `recaptcha-required`, `record-not-found`, `record-not-public`, `record-or-token-not-found`, `record-too-large`, `redirect-uri-mismatch`, `reduced-plan-not-available`, `rental-charge-already-reimbursed`, `rental-not-allowed`, `request-aborted-prematurely`, `request-handled-or-locked`, `request-id-invalid`, `request-queue-duplicate-requests`, `request-too-large`, `requested-dataset-view-does-not-exist`, `resume-token-expired`, `run-failed`, `run-input-body-not-valid-json`, `run-timeout-exceeded`, `russia-is-evil`, `same-user`, `schedule-actor-not-found`, `schedule-actor-task-not-found`, `schedule-name-not-unique`, `schema-validation`, `schema-validation-error`, `schema-validation-failed`, `service-worker-registration-not-allowed`, `sign-up-method-not-allowed`, `slack-integration-not-custom`, `socket-closed`, `socket-destroyed`, `store-schema-invalid`, `store-terms-not-accepted`, `stripe-enabled`, `stripe-generic-decline`, `stripe-not-enabled`, `stripe-not-enabled-for-user`, `tagged-build-required`, `tax-country-invalid`, `tax-number-invalid`, `tax-number-validation-failed`, `taxamo-call-failed`, `taxamo-request-failed`, `testing-error`, `token-not-provided`, `too-few-versions`, `too-many-actor-tasks`, `too-many-actors`, `too-many-labels-on-resource`, `too-many-mcp-connectors`, `too-many-o-auth-apps`, `too-many-organizations`, `too-many-requests`, `too-many-schedules`, `too-many-ui-access-keys`, `too-many-user-labels`, `too-many-values`, `too-many-versions`, `too-many-webhooks`, `unexpected-route`, `unknown-build-tag`, `unknown-payment-provider`, `unsubscribe-token-invalid`, `unsupported-actor-pricing-model-for-agentic-payments`, `unsupported-content-encoding`, `unsupported-file-type-for-issue`, `unsupported-file-type-image-expected`, `unsupported-file-type-text-or-json-expected`, `unsupported-permission`, `upcoming-subscription-bill-not-up-to-date`, `user-already-exists`, `user-already-verified`, `user-creates-organizations-too-fast`, `user-disabled`, `user-email-is-disposable`, `user-email-not-set`, `user-email-not-verified`, `user-has-no-subscription`, `user-integration-not-found`, `user-is-already-invited`, `user-is-already-organization-member`, `user-is-not-member-of-organization`, `user-is-not-organization`, `user-is-organization`, `user-is-organization-owner`, `user-is-removed`, `user-not-found`, `user-not-logged-in`, `user-not-verified`, `user-or-token-not-found`, `user-plan-not-allowed-for-coupon`, `user-problem-with-card`, `user-record-not-found`, `username-already-taken`, `username-missing`, `username-not-allowed`, `username-removal-forbidden`, `username-required`, `verification-email-already-sent`, `verification-token-expired`, `version-already-exists`, `versions-size-exceeded`, `weak-password`, `x402-agentic-payment-already-finalized`, `x402-agentic-payment-insufficient-amount`, `x402-agentic-payment-malformed-token`, `x402-agentic-payment-settlement-failed`, `x402-agentic-payment-settlement-in-progress`, `x402-agentic-payment-settlement-stuck`, `x402-agentic-payment-unauthorized`, `x402-payment-required`, `zero-invoice`]

  * **message** string

    Human-readable error message describing what went wrong.

### Status 405

Method not allowed.


```json
{

  "error": {

    "type": "method-not-allowed",

    "message": "This API end-point can only be accessed using the following HTTP methods: OPTIONS,GET"

  }

}
```


**Schema**

* **error** object required

  * **type** ErrorType (string)

    Machine-processable error type identifier.

    **Possible values:** \[`3d-secure-auth-failed`, `access-right-already-exists`, `action-not-found`, `actor-already-rented`, `actor-can-not-be-rented`, `actor-disabled`, `actor-is-not-rented`, `actor-memory-limit-exceeded`, `actor-name-exists-new-owner`, `actor-name-not-unique`, `actor-not-found`, `actor-not-github-actor`, `actor-not-public`, `actor-permission-level-not-supported-for-agentic-payments`, `actor-review-already-exists`, `actor-run-failed`, `actor-standby-not-supported-for-agentic-payments`, `actor-task-name-not-unique`, `agentic-payment-info-retrieval-error`, `agentic-payment-information-missing`, `agentic-payment-insufficient-amount`, `agentic-payment-provider-internal-error`, `agentic-payment-provider-unauthorized`, `airtable-webhook-deprecated`, `already-subscribed-to-paid-actor`, `apify-plan-required-to-use-paid-actor`, `apify-signup-not-allowed`, `auth-method-not-supported`, `authorization-server-not-found`, `auto-issue-date-invalid`, `background-check-required`, `billing-system-error`, `black-friday-plan-expired`, `braintree-error`, `braintree-not-linked`, `braintree-operation-timed-out`, `braintree-unsupported-currency`, `build-not-found`, `build-outdated`, `cannot-add-apify-events-to-ppe-actor`, `cannot-add-multiple-pricing-infos`, `cannot-add-pricing-info-that-alters-past`, `cannot-add-second-future-pricing-info`, `cannot-build-actor-from-webhook`, `cannot-change-billing-interval`, `cannot-change-owner`, `cannot-charge-apify-event`, `cannot-charge-non-pay-per-event-actor`, `cannot-comment-as-other-user`, `cannot-copy-actor-task`, `cannot-create-payout`, `cannot-create-public-actor`, `cannot-create-tax-transaction`, `cannot-delete-critical-actor`, `cannot-delete-invoice`, `cannot-delete-paid-actor`, `cannot-disable-one-time-event-for-apify-start-event`, `cannot-disable-organization-with-enabled-members`, `cannot-disable-user-with-subscription`, `cannot-link-oauth-to-unverified-email`, `cannot-metamorph-to-pay-per-result-actor`, `cannot-modify-actor-pricing-too-frequently`, `cannot-modify-actor-pricing-with-immediate-effect`, `cannot-monetize-without-payout-billing-info`, `cannot-override-paid-actor-trial`, `cannot-permanently-delete-subscription`, `cannot-publish-actor`, `cannot-publish-actor-task`, `cannot-reduce-last-full-token`, `cannot-reimburse-more-than-original-charge`, `cannot-reimburse-non-rental-charge`, `cannot-remove-own-actor-from-recently-used`, `cannot-remove-payment-method`, `cannot-remove-pricing-info`, `cannot-remove-running-run`, `cannot-remove-user-with-public-actors`, `cannot-remove-user-with-subscription`, `cannot-remove-user-with-unpaid-invoice`, `cannot-rename-env-var`, `cannot-rent-paid-actor`, `cannot-review-own-actor`, `cannot-set-access-rights-for-owner`, `cannot-set-is-status-message-terminal`, `cannot-unpublish-critical-actor`, `cannot-unpublish-paid-actor`, `cannot-unpublish-profile`, `cannot-update-invoice-field`, `concurrent-runs-limit-exceeded`, `concurrent-update-detected`, `conference-token-not-found`, `content-encoding-forbidden-for-html`, `coupon-already-redeemed`, `coupon-expired`, `coupon-for-new-customers`, `coupon-for-subscribed-users`, `coupon-limits-are-in-conflict-with-current-limits`, `coupon-max-number-of-redemptions-reached`, `coupon-not-found`, `coupon-not-unique`, `coupons-disabled`, `create-github-issue-not-allowed`, `creator-plan-not-available`, `cron-expression-invalid`, `daily-ai-token-limit-exceeded`, `daily-publication-limit-exceeded`, `dataset-does-not-have-fields-schema`, `dataset-does-not-have-schema`, `dataset-locked`, `dataset-schema-invalid`, `dcr-not-supported`, `default-dataset-not-found`, `deleting-default-build`, `deleting-unfinished-build`, `email-already-taken`, `email-already-taken-removed-user`, `email-domain-not-allowed-for-coupon`, `email-invalid`, `email-not-allowed`, `email-not-valid`, `email-update-too-soon`, `elevated-permissions-needed`, `env-var-already-exists`, `exchange-rate-fetch-failed`, `expired-conference-token`, `failed-to-charge-user`, `final-invoice-negative`, `full-permission-actor-blocked-for-admin`, `full-permission-actor-not-approved`, `github-branch-empty`, `github-issue-already-exists`, `github-public-key-not-found`, `github-repository-not-found`, `github-signature-does-not-match-payload`, `github-user-not-authorized-for-issues`, `gmail-not-allowed`, `id-does-not-match`, `incompatible-billing-interval`, `incomplete-payout-billing-info`, `inconsistent-currencies`, `incorrect-pricing-modifier-prefix`, `input-json-invalid-characters`, `input-json-not-object`, `input-json-too-long`, `input-update-collision`, `insufficient-permissions`, `insufficient-permissions-to-change-field`, `insufficient-security-measures`, `insufficient-tax-country-evidence`, `integration-auth-error`, `internal-server-error`, `invalid-billing-info`, `invalid-billing-period-for-payout`, `invalid-build`, `invalid-client-key`, `invalid-collection`, `invalid-conference-login-password`, `invalid-content-type-header`, `invalid-credentials`, `invalid-git-auth-token`, `invalid-github-issue-url`, `invalid-header`, `invalid-id`, `invalid-idempotency-key`, `invalid-input`, `invalid-input-schema`, `invalid-invoice`, `invalid-invoice-type`, `invalid-issue-date`, `invalid-label-params`, `invalid-main-account-user-id`, `invalid-oauth-app`, `invalid-oauth-scope`, `invalid-one-time-invoice`, `invalid-parameter`, `invalid-payout-status`, `invalid-picture-url`, `invalid-record-key`, `invalid-request`, `invalid-resource-type`, `invalid-signature`, `invalid-subscription-plan`, `invalid-tax-number`, `invalid-tax-number-format`, `invalid-token`, `invalid-token-type`, `invalid-two-factor-code`, `invalid-two-factor-code-or-recovery-code`, `invalid-two-factor-recovery-code`, `invalid-username`, `invalid-value`, `invitation-invalid-resource-type`, `invitation-no-longer-valid`, `invoice-canceled`, `invoice-cannot-be-refunded-due-to-too-high-amount`, `invoice-incomplete`, `invoice-is-draft`, `invoice-locked`, `invoice-must-be-buffer`, `invoice-not-canceled`, `invoice-not-draft`, `invoice-not-found`, `invoice-outdated`, `invoice-paid-already`, `issue-already-connected-to-github`, `issue-not-found`, `issues-bad-request`, `issuer-not-registered`, `job-finished`, `label-already-linked`, `last-api-token`, `limit-reached`, `max-items-must-be-greater-than-zero`, `max-metamorphs-exceeded`, `max-total-charge-usd-below-minimum`, `max-total-charge-usd-must-be-greater-than-zero`, `method-not-allowed`, `migration-disabled`, `missing-actor-rights`, `missing-api-token`, `missing-billing-info`, `missing-line-items`, `missing-payment-date`, `missing-payout-billing-info`, `missing-proxy-password`, `missing-reporting-fields`, `missing-resource-name`, `missing-settings`, `missing-username`, `monthly-usage-limit-too-low`, `more-than-one-update-not-allowed`, `multiple-records-found`, `must-be-admin`, `name-not-unique`, `next-runtime-computation-failed`, `no-columns-in-exported-dataset`, `no-payment-attempt-for-refund-found`, `no-payment-method-available`, `no-team-account-seats-available`, `non-temporary-email`, `not-enough-usage-to-run-paid-actor`, `not-implemented`, `not-supported-currencies`, `o-auth-service-already-connected`, `o-auth-service-not-connected`, `oauth-resource-access-failed`, `one-time-invoice-already-marked-paid`, `only-drafts-can-be-deleted`, `operation-canceled`, `operation-not-allowed`, `operation-timed-out`, `organization-cannot-own-itself`, `organization-role-not-found`, `overlapping-payout-billing-periods`, `own-token-required`, `page-not-found`, `param-not-one-of`, `parameter-required`, `parameters-mismatched`, `password-reset-email-already-sent`, `password-reset-token-expired`, `pay-as-you-go-without-monthly-interval`, `payment-attempt-status-message-required`, `payout-already-paid`, `payout-canceled`, `payout-invalid-state`, `payout-must-be-approved-to-be-marked-paid`, `payout-not-found`, `payout-number-already-exists`, `phone-number-invalid`, `phone-number-landline`, `phone-number-opted-out`, `phone-verification-disabled`, `platform-feature-disabled`, `price-overrides-validation-failed`, `pricing-model-not-supported`, `promotional-plan-not-available`, `proxy-auth-ip-not-unique`, `public-actor-disabled`, `query-timeout`, `quoted-price-outdated`, `rate-limit-exceeded`, `recaptcha-invalid`, `recaptcha-required`, `record-not-found`, `record-not-public`, `record-or-token-not-found`, `record-too-large`, `redirect-uri-mismatch`, `reduced-plan-not-available`, `rental-charge-already-reimbursed`, `rental-not-allowed`, `request-aborted-prematurely`, `request-handled-or-locked`, `request-id-invalid`, `request-queue-duplicate-requests`, `request-too-large`, `requested-dataset-view-does-not-exist`, `resume-token-expired`, `run-failed`, `run-input-body-not-valid-json`, `run-timeout-exceeded`, `russia-is-evil`, `same-user`, `schedule-actor-not-found`, `schedule-actor-task-not-found`, `schedule-name-not-unique`, `schema-validation`, `schema-validation-error`, `schema-validation-failed`, `service-worker-registration-not-allowed`, `sign-up-method-not-allowed`, `slack-integration-not-custom`, `socket-closed`, `socket-destroyed`, `store-schema-invalid`, `store-terms-not-accepted`, `stripe-enabled`, `stripe-generic-decline`, `stripe-not-enabled`, `stripe-not-enabled-for-user`, `tagged-build-required`, `tax-country-invalid`, `tax-number-invalid`, `tax-number-validation-failed`, `taxamo-call-failed`, `taxamo-request-failed`, `testing-error`, `token-not-provided`, `too-few-versions`, `too-many-actor-tasks`, `too-many-actors`, `too-many-labels-on-resource`, `too-many-mcp-connectors`, `too-many-o-auth-apps`, `too-many-organizations`, `too-many-requests`, `too-many-schedules`, `too-many-ui-access-keys`, `too-many-user-labels`, `too-many-values`, `too-many-versions`, `too-many-webhooks`, `unexpected-route`, `unknown-build-tag`, `unknown-payment-provider`, `unsubscribe-token-invalid`, `unsupported-actor-pricing-model-for-agentic-payments`, `unsupported-content-encoding`, `unsupported-file-type-for-issue`, `unsupported-file-type-image-expected`, `unsupported-file-type-text-or-json-expected`, `unsupported-permission`, `upcoming-subscription-bill-not-up-to-date`, `user-already-exists`, `user-already-verified`, `user-creates-organizations-too-fast`, `user-disabled`, `user-email-is-disposable`, `user-email-not-set`, `user-email-not-verified`, `user-has-no-subscription`, `user-integration-not-found`, `user-is-already-invited`, `user-is-already-organization-member`, `user-is-not-member-of-organization`, `user-is-not-organization`, `user-is-organization`, `user-is-organization-owner`, `user-is-removed`, `user-not-found`, `user-not-logged-in`, `user-not-verified`, `user-or-token-not-found`, `user-plan-not-allowed-for-coupon`, `user-problem-with-card`, `user-record-not-found`, `username-already-taken`, `username-missing`, `username-not-allowed`, `username-removal-forbidden`, `username-required`, `verification-email-already-sent`, `verification-token-expired`, `version-already-exists`, `versions-size-exceeded`, `weak-password`, `x402-agentic-payment-already-finalized`, `x402-agentic-payment-insufficient-amount`, `x402-agentic-payment-malformed-token`, `x402-agentic-payment-settlement-failed`, `x402-agentic-payment-settlement-in-progress`, `x402-agentic-payment-settlement-stuck`, `x402-agentic-payment-unauthorized`, `x402-payment-required`, `zero-invoice`]

  * **message** string

    Human-readable error message describing what went wrong.


```json
{

  "error": {

    "type": "method-not-allowed",

    "message": "This API end-point can only be accessed using the following HTTP methods: OPTIONS,GET"

  }

}
```


**Schema**

* **error** object required

  * **type** ErrorType (string)

    Machine-processable error type identifier.

    **Possible values:** \[`3d-secure-auth-failed`, `access-right-already-exists`, `action-not-found`, `actor-already-rented`, `actor-can-not-be-rented`, `actor-disabled`, `actor-is-not-rented`, `actor-memory-limit-exceeded`, `actor-name-exists-new-owner`, `actor-name-not-unique`, `actor-not-found`, `actor-not-github-actor`, `actor-not-public`, `actor-permission-level-not-supported-for-agentic-payments`, `actor-review-already-exists`, `actor-run-failed`, `actor-standby-not-supported-for-agentic-payments`, `actor-task-name-not-unique`, `agentic-payment-info-retrieval-error`, `agentic-payment-information-missing`, `agentic-payment-insufficient-amount`, `agentic-payment-provider-internal-error`, `agentic-payment-provider-unauthorized`, `airtable-webhook-deprecated`, `already-subscribed-to-paid-actor`, `apify-plan-required-to-use-paid-actor`, `apify-signup-not-allowed`, `auth-method-not-supported`, `authorization-server-not-found`, `auto-issue-date-invalid`, `background-check-required`, `billing-system-error`, `black-friday-plan-expired`, `braintree-error`, `braintree-not-linked`, `braintree-operation-timed-out`, `braintree-unsupported-currency`, `build-not-found`, `build-outdated`, `cannot-add-apify-events-to-ppe-actor`, `cannot-add-multiple-pricing-infos`, `cannot-add-pricing-info-that-alters-past`, `cannot-add-second-future-pricing-info`, `cannot-build-actor-from-webhook`, `cannot-change-billing-interval`, `cannot-change-owner`, `cannot-charge-apify-event`, `cannot-charge-non-pay-per-event-actor`, `cannot-comment-as-other-user`, `cannot-copy-actor-task`, `cannot-create-payout`, `cannot-create-public-actor`, `cannot-create-tax-transaction`, `cannot-delete-critical-actor`, `cannot-delete-invoice`, `cannot-delete-paid-actor`, `cannot-disable-one-time-event-for-apify-start-event`, `cannot-disable-organization-with-enabled-members`, `cannot-disable-user-with-subscription`, `cannot-link-oauth-to-unverified-email`, `cannot-metamorph-to-pay-per-result-actor`, `cannot-modify-actor-pricing-too-frequently`, `cannot-modify-actor-pricing-with-immediate-effect`, `cannot-monetize-without-payout-billing-info`, `cannot-override-paid-actor-trial`, `cannot-permanently-delete-subscription`, `cannot-publish-actor`, `cannot-publish-actor-task`, `cannot-reduce-last-full-token`, `cannot-reimburse-more-than-original-charge`, `cannot-reimburse-non-rental-charge`, `cannot-remove-own-actor-from-recently-used`, `cannot-remove-payment-method`, `cannot-remove-pricing-info`, `cannot-remove-running-run`, `cannot-remove-user-with-public-actors`, `cannot-remove-user-with-subscription`, `cannot-remove-user-with-unpaid-invoice`, `cannot-rename-env-var`, `cannot-rent-paid-actor`, `cannot-review-own-actor`, `cannot-set-access-rights-for-owner`, `cannot-set-is-status-message-terminal`, `cannot-unpublish-critical-actor`, `cannot-unpublish-paid-actor`, `cannot-unpublish-profile`, `cannot-update-invoice-field`, `concurrent-runs-limit-exceeded`, `concurrent-update-detected`, `conference-token-not-found`, `content-encoding-forbidden-for-html`, `coupon-already-redeemed`, `coupon-expired`, `coupon-for-new-customers`, `coupon-for-subscribed-users`, `coupon-limits-are-in-conflict-with-current-limits`, `coupon-max-number-of-redemptions-reached`, `coupon-not-found`, `coupon-not-unique`, `coupons-disabled`, `create-github-issue-not-allowed`, `creator-plan-not-available`, `cron-expression-invalid`, `daily-ai-token-limit-exceeded`, `daily-publication-limit-exceeded`, `dataset-does-not-have-fields-schema`, `dataset-does-not-have-schema`, `dataset-locked`, `dataset-schema-invalid`, `dcr-not-supported`, `default-dataset-not-found`, `deleting-default-build`, `deleting-unfinished-build`, `email-already-taken`, `email-already-taken-removed-user`, `email-domain-not-allowed-for-coupon`, `email-invalid`, `email-not-allowed`, `email-not-valid`, `email-update-too-soon`, `elevated-permissions-needed`, `env-var-already-exists`, `exchange-rate-fetch-failed`, `expired-conference-token`, `failed-to-charge-user`, `final-invoice-negative`, `full-permission-actor-blocked-for-admin`, `full-permission-actor-not-approved`, `github-branch-empty`, `github-issue-already-exists`, `github-public-key-not-found`, `github-repository-not-found`, `github-signature-does-not-match-payload`, `github-user-not-authorized-for-issues`, `gmail-not-allowed`, `id-does-not-match`, `incompatible-billing-interval`, `incomplete-payout-billing-info`, `inconsistent-currencies`, `incorrect-pricing-modifier-prefix`, `input-json-invalid-characters`, `input-json-not-object`, `input-json-too-long`, `input-update-collision`, `insufficient-permissions`, `insufficient-permissions-to-change-field`, `insufficient-security-measures`, `insufficient-tax-country-evidence`, `integration-auth-error`, `internal-server-error`, `invalid-billing-info`, `invalid-billing-period-for-payout`, `invalid-build`, `invalid-client-key`, `invalid-collection`, `invalid-conference-login-password`, `invalid-content-type-header`, `invalid-credentials`, `invalid-git-auth-token`, `invalid-github-issue-url`, `invalid-header`, `invalid-id`, `invalid-idempotency-key`, `invalid-input`, `invalid-input-schema`, `invalid-invoice`, `invalid-invoice-type`, `invalid-issue-date`, `invalid-label-params`, `invalid-main-account-user-id`, `invalid-oauth-app`, `invalid-oauth-scope`, `invalid-one-time-invoice`, `invalid-parameter`, `invalid-payout-status`, `invalid-picture-url`, `invalid-record-key`, `invalid-request`, `invalid-resource-type`, `invalid-signature`, `invalid-subscription-plan`, `invalid-tax-number`, `invalid-tax-number-format`, `invalid-token`, `invalid-token-type`, `invalid-two-factor-code`, `invalid-two-factor-code-or-recovery-code`, `invalid-two-factor-recovery-code`, `invalid-username`, `invalid-value`, `invitation-invalid-resource-type`, `invitation-no-longer-valid`, `invoice-canceled`, `invoice-cannot-be-refunded-due-to-too-high-amount`, `invoice-incomplete`, `invoice-is-draft`, `invoice-locked`, `invoice-must-be-buffer`, `invoice-not-canceled`, `invoice-not-draft`, `invoice-not-found`, `invoice-outdated`, `invoice-paid-already`, `issue-already-connected-to-github`, `issue-not-found`, `issues-bad-request`, `issuer-not-registered`, `job-finished`, `label-already-linked`, `last-api-token`, `limit-reached`, `max-items-must-be-greater-than-zero`, `max-metamorphs-exceeded`, `max-total-charge-usd-below-minimum`, `max-total-charge-usd-must-be-greater-than-zero`, `method-not-allowed`, `migration-disabled`, `missing-actor-rights`, `missing-api-token`, `missing-billing-info`, `missing-line-items`, `missing-payment-date`, `missing-payout-billing-info`, `missing-proxy-password`, `missing-reporting-fields`, `missing-resource-name`, `missing-settings`, `missing-username`, `monthly-usage-limit-too-low`, `more-than-one-update-not-allowed`, `multiple-records-found`, `must-be-admin`, `name-not-unique`, `next-runtime-computation-failed`, `no-columns-in-exported-dataset`, `no-payment-attempt-for-refund-found`, `no-payment-method-available`, `no-team-account-seats-available`, `non-temporary-email`, `not-enough-usage-to-run-paid-actor`, `not-implemented`, `not-supported-currencies`, `o-auth-service-already-connected`, `o-auth-service-not-connected`, `oauth-resource-access-failed`, `one-time-invoice-already-marked-paid`, `only-drafts-can-be-deleted`, `operation-canceled`, `operation-not-allowed`, `operation-timed-out`, `organization-cannot-own-itself`, `organization-role-not-found`, `overlapping-payout-billing-periods`, `own-token-required`, `page-not-found`, `param-not-one-of`, `parameter-required`, `parameters-mismatched`, `password-reset-email-already-sent`, `password-reset-token-expired`, `pay-as-you-go-without-monthly-interval`, `payment-attempt-status-message-required`, `payout-already-paid`, `payout-canceled`, `payout-invalid-state`, `payout-must-be-approved-to-be-marked-paid`, `payout-not-found`, `payout-number-already-exists`, `phone-number-invalid`, `phone-number-landline`, `phone-number-opted-out`, `phone-verification-disabled`, `platform-feature-disabled`, `price-overrides-validation-failed`, `pricing-model-not-supported`, `promotional-plan-not-available`, `proxy-auth-ip-not-unique`, `public-actor-disabled`, `query-timeout`, `quoted-price-outdated`, `rate-limit-exceeded`, `recaptcha-invalid`, `recaptcha-required`, `record-not-found`, `record-not-public`, `record-or-token-not-found`, `record-too-large`, `redirect-uri-mismatch`, `reduced-plan-not-available`, `rental-charge-already-reimbursed`, `rental-not-allowed`, `request-aborted-prematurely`, `request-handled-or-locked`, `request-id-invalid`, `request-queue-duplicate-requests`, `request-too-large`, `requested-dataset-view-does-not-exist`, `resume-token-expired`, `run-failed`, `run-input-body-not-valid-json`, `run-timeout-exceeded`, `russia-is-evil`, `same-user`, `schedule-actor-not-found`, `schedule-actor-task-not-found`, `schedule-name-not-unique`, `schema-validation`, `schema-validation-error`, `schema-validation-failed`, `service-worker-registration-not-allowed`, `sign-up-method-not-allowed`, `slack-integration-not-custom`, `socket-closed`, `socket-destroyed`, `store-schema-invalid`, `store-terms-not-accepted`, `stripe-enabled`, `stripe-generic-decline`, `stripe-not-enabled`, `stripe-not-enabled-for-user`, `tagged-build-required`, `tax-country-invalid`, `tax-number-invalid`, `tax-number-validation-failed`, `taxamo-call-failed`, `taxamo-request-failed`, `testing-error`, `token-not-provided`, `too-few-versions`, `too-many-actor-tasks`, `too-many-actors`, `too-many-labels-on-resource`, `too-many-mcp-connectors`, `too-many-o-auth-apps`, `too-many-organizations`, `too-many-requests`, `too-many-schedules`, `too-many-ui-access-keys`, `too-many-user-labels`, `too-many-values`, `too-many-versions`, `too-many-webhooks`, `unexpected-route`, `unknown-build-tag`, `unknown-payment-provider`, `unsubscribe-token-invalid`, `unsupported-actor-pricing-model-for-agentic-payments`, `unsupported-content-encoding`, `unsupported-file-type-for-issue`, `unsupported-file-type-image-expected`, `unsupported-file-type-text-or-json-expected`, `unsupported-permission`, `upcoming-subscription-bill-not-up-to-date`, `user-already-exists`, `user-already-verified`, `user-creates-organizations-too-fast`, `user-disabled`, `user-email-is-disposable`, `user-email-not-set`, `user-email-not-verified`, `user-has-no-subscription`, `user-integration-not-found`, `user-is-already-invited`, `user-is-already-organization-member`, `user-is-not-member-of-organization`, `user-is-not-organization`, `user-is-organization`, `user-is-organization-owner`, `user-is-removed`, `user-not-found`, `user-not-logged-in`, `user-not-verified`, `user-or-token-not-found`, `user-plan-not-allowed-for-coupon`, `user-problem-with-card`, `user-record-not-found`, `username-already-taken`, `username-missing`, `username-not-allowed`, `username-removal-forbidden`, `username-required`, `verification-email-already-sent`, `verification-token-expired`, `version-already-exists`, `versions-size-exceeded`, `weak-password`, `x402-agentic-payment-already-finalized`, `x402-agentic-payment-insufficient-amount`, `x402-agentic-payment-malformed-token`, `x402-agentic-payment-settlement-failed`, `x402-agentic-payment-settlement-in-progress`, `x402-agentic-payment-settlement-stuck`, `x402-agentic-payment-unauthorized`, `x402-payment-required`, `zero-invoice`]

  * **message** string

    Human-readable error message describing what went wrong.

### Status 413

Payload too large - the request body exceeds the size limit.


```json
{

  "error": {

    "type": "request-too-large",

    "message": "The POST payload is too large (limit: 9437184 bytes, actual length: 10485760 bytes)."

  }

}
```


**Schema**

* **error** object required

  * **type** ErrorType (string)

    Machine-processable error type identifier.

    **Possible values:** \[`3d-secure-auth-failed`, `access-right-already-exists`, `action-not-found`, `actor-already-rented`, `actor-can-not-be-rented`, `actor-disabled`, `actor-is-not-rented`, `actor-memory-limit-exceeded`, `actor-name-exists-new-owner`, `actor-name-not-unique`, `actor-not-found`, `actor-not-github-actor`, `actor-not-public`, `actor-permission-level-not-supported-for-agentic-payments`, `actor-review-already-exists`, `actor-run-failed`, `actor-standby-not-supported-for-agentic-payments`, `actor-task-name-not-unique`, `agentic-payment-info-retrieval-error`, `agentic-payment-information-missing`, `agentic-payment-insufficient-amount`, `agentic-payment-provider-internal-error`, `agentic-payment-provider-unauthorized`, `airtable-webhook-deprecated`, `already-subscribed-to-paid-actor`, `apify-plan-required-to-use-paid-actor`, `apify-signup-not-allowed`, `auth-method-not-supported`, `authorization-server-not-found`, `auto-issue-date-invalid`, `background-check-required`, `billing-system-error`, `black-friday-plan-expired`, `braintree-error`, `braintree-not-linked`, `braintree-operation-timed-out`, `braintree-unsupported-currency`, `build-not-found`, `build-outdated`, `cannot-add-apify-events-to-ppe-actor`, `cannot-add-multiple-pricing-infos`, `cannot-add-pricing-info-that-alters-past`, `cannot-add-second-future-pricing-info`, `cannot-build-actor-from-webhook`, `cannot-change-billing-interval`, `cannot-change-owner`, `cannot-charge-apify-event`, `cannot-charge-non-pay-per-event-actor`, `cannot-comment-as-other-user`, `cannot-copy-actor-task`, `cannot-create-payout`, `cannot-create-public-actor`, `cannot-create-tax-transaction`, `cannot-delete-critical-actor`, `cannot-delete-invoice`, `cannot-delete-paid-actor`, `cannot-disable-one-time-event-for-apify-start-event`, `cannot-disable-organization-with-enabled-members`, `cannot-disable-user-with-subscription`, `cannot-link-oauth-to-unverified-email`, `cannot-metamorph-to-pay-per-result-actor`, `cannot-modify-actor-pricing-too-frequently`, `cannot-modify-actor-pricing-with-immediate-effect`, `cannot-monetize-without-payout-billing-info`, `cannot-override-paid-actor-trial`, `cannot-permanently-delete-subscription`, `cannot-publish-actor`, `cannot-publish-actor-task`, `cannot-reduce-last-full-token`, `cannot-reimburse-more-than-original-charge`, `cannot-reimburse-non-rental-charge`, `cannot-remove-own-actor-from-recently-used`, `cannot-remove-payment-method`, `cannot-remove-pricing-info`, `cannot-remove-running-run`, `cannot-remove-user-with-public-actors`, `cannot-remove-user-with-subscription`, `cannot-remove-user-with-unpaid-invoice`, `cannot-rename-env-var`, `cannot-rent-paid-actor`, `cannot-review-own-actor`, `cannot-set-access-rights-for-owner`, `cannot-set-is-status-message-terminal`, `cannot-unpublish-critical-actor`, `cannot-unpublish-paid-actor`, `cannot-unpublish-profile`, `cannot-update-invoice-field`, `concurrent-runs-limit-exceeded`, `concurrent-update-detected`, `conference-token-not-found`, `content-encoding-forbidden-for-html`, `coupon-already-redeemed`, `coupon-expired`, `coupon-for-new-customers`, `coupon-for-subscribed-users`, `coupon-limits-are-in-conflict-with-current-limits`, `coupon-max-number-of-redemptions-reached`, `coupon-not-found`, `coupon-not-unique`, `coupons-disabled`, `create-github-issue-not-allowed`, `creator-plan-not-available`, `cron-expression-invalid`, `daily-ai-token-limit-exceeded`, `daily-publication-limit-exceeded`, `dataset-does-not-have-fields-schema`, `dataset-does-not-have-schema`, `dataset-locked`, `dataset-schema-invalid`, `dcr-not-supported`, `default-dataset-not-found`, `deleting-default-build`, `deleting-unfinished-build`, `email-already-taken`, `email-already-taken-removed-user`, `email-domain-not-allowed-for-coupon`, `email-invalid`, `email-not-allowed`, `email-not-valid`, `email-update-too-soon`, `elevated-permissions-needed`, `env-var-already-exists`, `exchange-rate-fetch-failed`, `expired-conference-token`, `failed-to-charge-user`, `final-invoice-negative`, `full-permission-actor-blocked-for-admin`, `full-permission-actor-not-approved`, `github-branch-empty`, `github-issue-already-exists`, `github-public-key-not-found`, `github-repository-not-found`, `github-signature-does-not-match-payload`, `github-user-not-authorized-for-issues`, `gmail-not-allowed`, `id-does-not-match`, `incompatible-billing-interval`, `incomplete-payout-billing-info`, `inconsistent-currencies`, `incorrect-pricing-modifier-prefix`, `input-json-invalid-characters`, `input-json-not-object`, `input-json-too-long`, `input-update-collision`, `insufficient-permissions`, `insufficient-permissions-to-change-field`, `insufficient-security-measures`, `insufficient-tax-country-evidence`, `integration-auth-error`, `internal-server-error`, `invalid-billing-info`, `invalid-billing-period-for-payout`, `invalid-build`, `invalid-client-key`, `invalid-collection`, `invalid-conference-login-password`, `invalid-content-type-header`, `invalid-credentials`, `invalid-git-auth-token`, `invalid-github-issue-url`, `invalid-header`, `invalid-id`, `invalid-idempotency-key`, `invalid-input`, `invalid-input-schema`, `invalid-invoice`, `invalid-invoice-type`, `invalid-issue-date`, `invalid-label-params`, `invalid-main-account-user-id`, `invalid-oauth-app`, `invalid-oauth-scope`, `invalid-one-time-invoice`, `invalid-parameter`, `invalid-payout-status`, `invalid-picture-url`, `invalid-record-key`, `invalid-request`, `invalid-resource-type`, `invalid-signature`, `invalid-subscription-plan`, `invalid-tax-number`, `invalid-tax-number-format`, `invalid-token`, `invalid-token-type`, `invalid-two-factor-code`, `invalid-two-factor-code-or-recovery-code`, `invalid-two-factor-recovery-code`, `invalid-username`, `invalid-value`, `invitation-invalid-resource-type`, `invitation-no-longer-valid`, `invoice-canceled`, `invoice-cannot-be-refunded-due-to-too-high-amount`, `invoice-incomplete`, `invoice-is-draft`, `invoice-locked`, `invoice-must-be-buffer`, `invoice-not-canceled`, `invoice-not-draft`, `invoice-not-found`, `invoice-outdated`, `invoice-paid-already`, `issue-already-connected-to-github`, `issue-not-found`, `issues-bad-request`, `issuer-not-registered`, `job-finished`, `label-already-linked`, `last-api-token`, `limit-reached`, `max-items-must-be-greater-than-zero`, `max-metamorphs-exceeded`, `max-total-charge-usd-below-minimum`, `max-total-charge-usd-must-be-greater-than-zero`, `method-not-allowed`, `migration-disabled`, `missing-actor-rights`, `missing-api-token`, `missing-billing-info`, `missing-line-items`, `missing-payment-date`, `missing-payout-billing-info`, `missing-proxy-password`, `missing-reporting-fields`, `missing-resource-name`, `missing-settings`, `missing-username`, `monthly-usage-limit-too-low`, `more-than-one-update-not-allowed`, `multiple-records-found`, `must-be-admin`, `name-not-unique`, `next-runtime-computation-failed`, `no-columns-in-exported-dataset`, `no-payment-attempt-for-refund-found`, `no-payment-method-available`, `no-team-account-seats-available`, `non-temporary-email`, `not-enough-usage-to-run-paid-actor`, `not-implemented`, `not-supported-currencies`, `o-auth-service-already-connected`, `o-auth-service-not-connected`, `oauth-resource-access-failed`, `one-time-invoice-already-marked-paid`, `only-drafts-can-be-deleted`, `operation-canceled`, `operation-not-allowed`, `operation-timed-out`, `organization-cannot-own-itself`, `organization-role-not-found`, `overlapping-payout-billing-periods`, `own-token-required`, `page-not-found`, `param-not-one-of`, `parameter-required`, `parameters-mismatched`, `password-reset-email-already-sent`, `password-reset-token-expired`, `pay-as-you-go-without-monthly-interval`, `payment-attempt-status-message-required`, `payout-already-paid`, `payout-canceled`, `payout-invalid-state`, `payout-must-be-approved-to-be-marked-paid`, `payout-not-found`, `payout-number-already-exists`, `phone-number-invalid`, `phone-number-landline`, `phone-number-opted-out`, `phone-verification-disabled`, `platform-feature-disabled`, `price-overrides-validation-failed`, `pricing-model-not-supported`, `promotional-plan-not-available`, `proxy-auth-ip-not-unique`, `public-actor-disabled`, `query-timeout`, `quoted-price-outdated`, `rate-limit-exceeded`, `recaptcha-invalid`, `recaptcha-required`, `record-not-found`, `record-not-public`, `record-or-token-not-found`, `record-too-large`, `redirect-uri-mismatch`, `reduced-plan-not-available`, `rental-charge-already-reimbursed`, `rental-not-allowed`, `request-aborted-prematurely`, `request-handled-or-locked`, `request-id-invalid`, `request-queue-duplicate-requests`, `request-too-large`, `requested-dataset-view-does-not-exist`, `resume-token-expired`, `run-failed`, `run-input-body-not-valid-json`, `run-timeout-exceeded`, `russia-is-evil`, `same-user`, `schedule-actor-not-found`, `schedule-actor-task-not-found`, `schedule-name-not-unique`, `schema-validation`, `schema-validation-error`, `schema-validation-failed`, `service-worker-registration-not-allowed`, `sign-up-method-not-allowed`, `slack-integration-not-custom`, `socket-closed`, `socket-destroyed`, `store-schema-invalid`, `store-terms-not-accepted`, `stripe-enabled`, `stripe-generic-decline`, `stripe-not-enabled`, `stripe-not-enabled-for-user`, `tagged-build-required`, `tax-country-invalid`, `tax-number-invalid`, `tax-number-validation-failed`, `taxamo-call-failed`, `taxamo-request-failed`, `testing-error`, `token-not-provided`, `too-few-versions`, `too-many-actor-tasks`, `too-many-actors`, `too-many-labels-on-resource`, `too-many-mcp-connectors`, `too-many-o-auth-apps`, `too-many-organizations`, `too-many-requests`, `too-many-schedules`, `too-many-ui-access-keys`, `too-many-user-labels`, `too-many-values`, `too-many-versions`, `too-many-webhooks`, `unexpected-route`, `unknown-build-tag`, `unknown-payment-provider`, `unsubscribe-token-invalid`, `unsupported-actor-pricing-model-for-agentic-payments`, `unsupported-content-encoding`, `unsupported-file-type-for-issue`, `unsupported-file-type-image-expected`, `unsupported-file-type-text-or-json-expected`, `unsupported-permission`, `upcoming-subscription-bill-not-up-to-date`, `user-already-exists`, `user-already-verified`, `user-creates-organizations-too-fast`, `user-disabled`, `user-email-is-disposable`, `user-email-not-set`, `user-email-not-verified`, `user-has-no-subscription`, `user-integration-not-found`, `user-is-already-invited`, `user-is-already-organization-member`, `user-is-not-member-of-organization`, `user-is-not-organization`, `user-is-organization`, `user-is-organization-owner`, `user-is-removed`, `user-not-found`, `user-not-logged-in`, `user-not-verified`, `user-or-token-not-found`, `user-plan-not-allowed-for-coupon`, `user-problem-with-card`, `user-record-not-found`, `username-already-taken`, `username-missing`, `username-not-allowed`, `username-removal-forbidden`, `username-required`, `verification-email-already-sent`, `verification-token-expired`, `version-already-exists`, `versions-size-exceeded`, `weak-password`, `x402-agentic-payment-already-finalized`, `x402-agentic-payment-insufficient-amount`, `x402-agentic-payment-malformed-token`, `x402-agentic-payment-settlement-failed`, `x402-agentic-payment-settlement-in-progress`, `x402-agentic-payment-settlement-stuck`, `x402-agentic-payment-unauthorized`, `x402-payment-required`, `zero-invoice`]

  * **message** string

    Human-readable error message describing what went wrong.


```json
{

  "error": {

    "type": "request-too-large",

    "message": "The POST payload is too large (limit: 9437184 bytes, actual length: 10485760 bytes)."

  }

}
```


**Schema**

* **error** object required

  * **type** ErrorType (string)

    Machine-processable error type identifier.

    **Possible values:** \[`3d-secure-auth-failed`, `access-right-already-exists`, `action-not-found`, `actor-already-rented`, `actor-can-not-be-rented`, `actor-disabled`, `actor-is-not-rented`, `actor-memory-limit-exceeded`, `actor-name-exists-new-owner`, `actor-name-not-unique`, `actor-not-found`, `actor-not-github-actor`, `actor-not-public`, `actor-permission-level-not-supported-for-agentic-payments`, `actor-review-already-exists`, `actor-run-failed`, `actor-standby-not-supported-for-agentic-payments`, `actor-task-name-not-unique`, `agentic-payment-info-retrieval-error`, `agentic-payment-information-missing`, `agentic-payment-insufficient-amount`, `agentic-payment-provider-internal-error`, `agentic-payment-provider-unauthorized`, `airtable-webhook-deprecated`, `already-subscribed-to-paid-actor`, `apify-plan-required-to-use-paid-actor`, `apify-signup-not-allowed`, `auth-method-not-supported`, `authorization-server-not-found`, `auto-issue-date-invalid`, `background-check-required`, `billing-system-error`, `black-friday-plan-expired`, `braintree-error`, `braintree-not-linked`, `braintree-operation-timed-out`, `braintree-unsupported-currency`, `build-not-found`, `build-outdated`, `cannot-add-apify-events-to-ppe-actor`, `cannot-add-multiple-pricing-infos`, `cannot-add-pricing-info-that-alters-past`, `cannot-add-second-future-pricing-info`, `cannot-build-actor-from-webhook`, `cannot-change-billing-interval`, `cannot-change-owner`, `cannot-charge-apify-event`, `cannot-charge-non-pay-per-event-actor`, `cannot-comment-as-other-user`, `cannot-copy-actor-task`, `cannot-create-payout`, `cannot-create-public-actor`, `cannot-create-tax-transaction`, `cannot-delete-critical-actor`, `cannot-delete-invoice`, `cannot-delete-paid-actor`, `cannot-disable-one-time-event-for-apify-start-event`, `cannot-disable-organization-with-enabled-members`, `cannot-disable-user-with-subscription`, `cannot-link-oauth-to-unverified-email`, `cannot-metamorph-to-pay-per-result-actor`, `cannot-modify-actor-pricing-too-frequently`, `cannot-modify-actor-pricing-with-immediate-effect`, `cannot-monetize-without-payout-billing-info`, `cannot-override-paid-actor-trial`, `cannot-permanently-delete-subscription`, `cannot-publish-actor`, `cannot-publish-actor-task`, `cannot-reduce-last-full-token`, `cannot-reimburse-more-than-original-charge`, `cannot-reimburse-non-rental-charge`, `cannot-remove-own-actor-from-recently-used`, `cannot-remove-payment-method`, `cannot-remove-pricing-info`, `cannot-remove-running-run`, `cannot-remove-user-with-public-actors`, `cannot-remove-user-with-subscription`, `cannot-remove-user-with-unpaid-invoice`, `cannot-rename-env-var`, `cannot-rent-paid-actor`, `cannot-review-own-actor`, `cannot-set-access-rights-for-owner`, `cannot-set-is-status-message-terminal`, `cannot-unpublish-critical-actor`, `cannot-unpublish-paid-actor`, `cannot-unpublish-profile`, `cannot-update-invoice-field`, `concurrent-runs-limit-exceeded`, `concurrent-update-detected`, `conference-token-not-found`, `content-encoding-forbidden-for-html`, `coupon-already-redeemed`, `coupon-expired`, `coupon-for-new-customers`, `coupon-for-subscribed-users`, `coupon-limits-are-in-conflict-with-current-limits`, `coupon-max-number-of-redemptions-reached`, `coupon-not-found`, `coupon-not-unique`, `coupons-disabled`, `create-github-issue-not-allowed`, `creator-plan-not-available`, `cron-expression-invalid`, `daily-ai-token-limit-exceeded`, `daily-publication-limit-exceeded`, `dataset-does-not-have-fields-schema`, `dataset-does-not-have-schema`, `dataset-locked`, `dataset-schema-invalid`, `dcr-not-supported`, `default-dataset-not-found`, `deleting-default-build`, `deleting-unfinished-build`, `email-already-taken`, `email-already-taken-removed-user`, `email-domain-not-allowed-for-coupon`, `email-invalid`, `email-not-allowed`, `email-not-valid`, `email-update-too-soon`, `elevated-permissions-needed`, `env-var-already-exists`, `exchange-rate-fetch-failed`, `expired-conference-token`, `failed-to-charge-user`, `final-invoice-negative`, `full-permission-actor-blocked-for-admin`, `full-permission-actor-not-approved`, `github-branch-empty`, `github-issue-already-exists`, `github-public-key-not-found`, `github-repository-not-found`, `github-signature-does-not-match-payload`, `github-user-not-authorized-for-issues`, `gmail-not-allowed`, `id-does-not-match`, `incompatible-billing-interval`, `incomplete-payout-billing-info`, `inconsistent-currencies`, `incorrect-pricing-modifier-prefix`, `input-json-invalid-characters`, `input-json-not-object`, `input-json-too-long`, `input-update-collision`, `insufficient-permissions`, `insufficient-permissions-to-change-field`, `insufficient-security-measures`, `insufficient-tax-country-evidence`, `integration-auth-error`, `internal-server-error`, `invalid-billing-info`, `invalid-billing-period-for-payout`, `invalid-build`, `invalid-client-key`, `invalid-collection`, `invalid-conference-login-password`, `invalid-content-type-header`, `invalid-credentials`, `invalid-git-auth-token`, `invalid-github-issue-url`, `invalid-header`, `invalid-id`, `invalid-idempotency-key`, `invalid-input`, `invalid-input-schema`, `invalid-invoice`, `invalid-invoice-type`, `invalid-issue-date`, `invalid-label-params`, `invalid-main-account-user-id`, `invalid-oauth-app`, `invalid-oauth-scope`, `invalid-one-time-invoice`, `invalid-parameter`, `invalid-payout-status`, `invalid-picture-url`, `invalid-record-key`, `invalid-request`, `invalid-resource-type`, `invalid-signature`, `invalid-subscription-plan`, `invalid-tax-number`, `invalid-tax-number-format`, `invalid-token`, `invalid-token-type`, `invalid-two-factor-code`, `invalid-two-factor-code-or-recovery-code`, `invalid-two-factor-recovery-code`, `invalid-username`, `invalid-value`, `invitation-invalid-resource-type`, `invitation-no-longer-valid`, `invoice-canceled`, `invoice-cannot-be-refunded-due-to-too-high-amount`, `invoice-incomplete`, `invoice-is-draft`, `invoice-locked`, `invoice-must-be-buffer`, `invoice-not-canceled`, `invoice-not-draft`, `invoice-not-found`, `invoice-outdated`, `invoice-paid-already`, `issue-already-connected-to-github`, `issue-not-found`, `issues-bad-request`, `issuer-not-registered`, `job-finished`, `label-already-linked`, `last-api-token`, `limit-reached`, `max-items-must-be-greater-than-zero`, `max-metamorphs-exceeded`, `max-total-charge-usd-below-minimum`, `max-total-charge-usd-must-be-greater-than-zero`, `method-not-allowed`, `migration-disabled`, `missing-actor-rights`, `missing-api-token`, `missing-billing-info`, `missing-line-items`, `missing-payment-date`, `missing-payout-billing-info`, `missing-proxy-password`, `missing-reporting-fields`, `missing-resource-name`, `missing-settings`, `missing-username`, `monthly-usage-limit-too-low`, `more-than-one-update-not-allowed`, `multiple-records-found`, `must-be-admin`, `name-not-unique`, `next-runtime-computation-failed`, `no-columns-in-exported-dataset`, `no-payment-attempt-for-refund-found`, `no-payment-method-available`, `no-team-account-seats-available`, `non-temporary-email`, `not-enough-usage-to-run-paid-actor`, `not-implemented`, `not-supported-currencies`, `o-auth-service-already-connected`, `o-auth-service-not-connected`, `oauth-resource-access-failed`, `one-time-invoice-already-marked-paid`, `only-drafts-can-be-deleted`, `operation-canceled`, `operation-not-allowed`, `operation-timed-out`, `organization-cannot-own-itself`, `organization-role-not-found`, `overlapping-payout-billing-periods`, `own-token-required`, `page-not-found`, `param-not-one-of`, `parameter-required`, `parameters-mismatched`, `password-reset-email-already-sent`, `password-reset-token-expired`, `pay-as-you-go-without-monthly-interval`, `payment-attempt-status-message-required`, `payout-already-paid`, `payout-canceled`, `payout-invalid-state`, `payout-must-be-approved-to-be-marked-paid`, `payout-not-found`, `payout-number-already-exists`, `phone-number-invalid`, `phone-number-landline`, `phone-number-opted-out`, `phone-verification-disabled`, `platform-feature-disabled`, `price-overrides-validation-failed`, `pricing-model-not-supported`, `promotional-plan-not-available`, `proxy-auth-ip-not-unique`, `public-actor-disabled`, `query-timeout`, `quoted-price-outdated`, `rate-limit-exceeded`, `recaptcha-invalid`, `recaptcha-required`, `record-not-found`, `record-not-public`, `record-or-token-not-found`, `record-too-large`, `redirect-uri-mismatch`, `reduced-plan-not-available`, `rental-charge-already-reimbursed`, `rental-not-allowed`, `request-aborted-prematurely`, `request-handled-or-locked`, `request-id-invalid`, `request-queue-duplicate-requests`, `request-too-large`, `requested-dataset-view-does-not-exist`, `resume-token-expired`, `run-failed`, `run-input-body-not-valid-json`, `run-timeout-exceeded`, `russia-is-evil`, `same-user`, `schedule-actor-not-found`, `schedule-actor-task-not-found`, `schedule-name-not-unique`, `schema-validation`, `schema-validation-error`, `schema-validation-failed`, `service-worker-registration-not-allowed`, `sign-up-method-not-allowed`, `slack-integration-not-custom`, `socket-closed`, `socket-destroyed`, `store-schema-invalid`, `store-terms-not-accepted`, `stripe-enabled`, `stripe-generic-decline`, `stripe-not-enabled`, `stripe-not-enabled-for-user`, `tagged-build-required`, `tax-country-invalid`, `tax-number-invalid`, `tax-number-validation-failed`, `taxamo-call-failed`, `taxamo-request-failed`, `testing-error`, `token-not-provided`, `too-few-versions`, `too-many-actor-tasks`, `too-many-actors`, `too-many-labels-on-resource`, `too-many-mcp-connectors`, `too-many-o-auth-apps`, `too-many-organizations`, `too-many-requests`, `too-many-schedules`, `too-many-ui-access-keys`, `too-many-user-labels`, `too-many-values`, `too-many-versions`, `too-many-webhooks`, `unexpected-route`, `unknown-build-tag`, `unknown-payment-provider`, `unsubscribe-token-invalid`, `unsupported-actor-pricing-model-for-agentic-payments`, `unsupported-content-encoding`, `unsupported-file-type-for-issue`, `unsupported-file-type-image-expected`, `unsupported-file-type-text-or-json-expected`, `unsupported-permission`, `upcoming-subscription-bill-not-up-to-date`, `user-already-exists`, `user-already-verified`, `user-creates-organizations-too-fast`, `user-disabled`, `user-email-is-disposable`, `user-email-not-set`, `user-email-not-verified`, `user-has-no-subscription`, `user-integration-not-found`, `user-is-already-invited`, `user-is-already-organization-member`, `user-is-not-member-of-organization`, `user-is-not-organization`, `user-is-organization`, `user-is-organization-owner`, `user-is-removed`, `user-not-found`, `user-not-logged-in`, `user-not-verified`, `user-or-token-not-found`, `user-plan-not-allowed-for-coupon`, `user-problem-with-card`, `user-record-not-found`, `username-already-taken`, `username-missing`, `username-not-allowed`, `username-removal-forbidden`, `username-required`, `verification-email-already-sent`, `verification-token-expired`, `version-already-exists`, `versions-size-exceeded`, `weak-password`, `x402-agentic-payment-already-finalized`, `x402-agentic-payment-insufficient-amount`, `x402-agentic-payment-malformed-token`, `x402-agentic-payment-settlement-failed`, `x402-agentic-payment-settlement-in-progress`, `x402-agentic-payment-settlement-stuck`, `x402-agentic-payment-unauthorized`, `x402-payment-required`, `zero-invoice`]

  * **message** string

    Human-readable error message describing what went wrong.

### Status 415

Unsupported media type - the Content-Encoding of the request is not supported.


```json
{

  "error": {

    "type": "unsupported-content-encoding",

    "message": "Content-Encoding \"bla\" is not supported."

  }

}
```


**Schema**

* **error** object required

  * **type** ErrorType (string)

    Machine-processable error type identifier.

    **Possible values:** \[`3d-secure-auth-failed`, `access-right-already-exists`, `action-not-found`, `actor-already-rented`, `actor-can-not-be-rented`, `actor-disabled`, `actor-is-not-rented`, `actor-memory-limit-exceeded`, `actor-name-exists-new-owner`, `actor-name-not-unique`, `actor-not-found`, `actor-not-github-actor`, `actor-not-public`, `actor-permission-level-not-supported-for-agentic-payments`, `actor-review-already-exists`, `actor-run-failed`, `actor-standby-not-supported-for-agentic-payments`, `actor-task-name-not-unique`, `agentic-payment-info-retrieval-error`, `agentic-payment-information-missing`, `agentic-payment-insufficient-amount`, `agentic-payment-provider-internal-error`, `agentic-payment-provider-unauthorized`, `airtable-webhook-deprecated`, `already-subscribed-to-paid-actor`, `apify-plan-required-to-use-paid-actor`, `apify-signup-not-allowed`, `auth-method-not-supported`, `authorization-server-not-found`, `auto-issue-date-invalid`, `background-check-required`, `billing-system-error`, `black-friday-plan-expired`, `braintree-error`, `braintree-not-linked`, `braintree-operation-timed-out`, `braintree-unsupported-currency`, `build-not-found`, `build-outdated`, `cannot-add-apify-events-to-ppe-actor`, `cannot-add-multiple-pricing-infos`, `cannot-add-pricing-info-that-alters-past`, `cannot-add-second-future-pricing-info`, `cannot-build-actor-from-webhook`, `cannot-change-billing-interval`, `cannot-change-owner`, `cannot-charge-apify-event`, `cannot-charge-non-pay-per-event-actor`, `cannot-comment-as-other-user`, `cannot-copy-actor-task`, `cannot-create-payout`, `cannot-create-public-actor`, `cannot-create-tax-transaction`, `cannot-delete-critical-actor`, `cannot-delete-invoice`, `cannot-delete-paid-actor`, `cannot-disable-one-time-event-for-apify-start-event`, `cannot-disable-organization-with-enabled-members`, `cannot-disable-user-with-subscription`, `cannot-link-oauth-to-unverified-email`, `cannot-metamorph-to-pay-per-result-actor`, `cannot-modify-actor-pricing-too-frequently`, `cannot-modify-actor-pricing-with-immediate-effect`, `cannot-monetize-without-payout-billing-info`, `cannot-override-paid-actor-trial`, `cannot-permanently-delete-subscription`, `cannot-publish-actor`, `cannot-publish-actor-task`, `cannot-reduce-last-full-token`, `cannot-reimburse-more-than-original-charge`, `cannot-reimburse-non-rental-charge`, `cannot-remove-own-actor-from-recently-used`, `cannot-remove-payment-method`, `cannot-remove-pricing-info`, `cannot-remove-running-run`, `cannot-remove-user-with-public-actors`, `cannot-remove-user-with-subscription`, `cannot-remove-user-with-unpaid-invoice`, `cannot-rename-env-var`, `cannot-rent-paid-actor`, `cannot-review-own-actor`, `cannot-set-access-rights-for-owner`, `cannot-set-is-status-message-terminal`, `cannot-unpublish-critical-actor`, `cannot-unpublish-paid-actor`, `cannot-unpublish-profile`, `cannot-update-invoice-field`, `concurrent-runs-limit-exceeded`, `concurrent-update-detected`, `conference-token-not-found`, `content-encoding-forbidden-for-html`, `coupon-already-redeemed`, `coupon-expired`, `coupon-for-new-customers`, `coupon-for-subscribed-users`, `coupon-limits-are-in-conflict-with-current-limits`, `coupon-max-number-of-redemptions-reached`, `coupon-not-found`, `coupon-not-unique`, `coupons-disabled`, `create-github-issue-not-allowed`, `creator-plan-not-available`, `cron-expression-invalid`, `daily-ai-token-limit-exceeded`, `daily-publication-limit-exceeded`, `dataset-does-not-have-fields-schema`, `dataset-does-not-have-schema`, `dataset-locked`, `dataset-schema-invalid`, `dcr-not-supported`, `default-dataset-not-found`, `deleting-default-build`, `deleting-unfinished-build`, `email-already-taken`, `email-already-taken-removed-user`, `email-domain-not-allowed-for-coupon`, `email-invalid`, `email-not-allowed`, `email-not-valid`, `email-update-too-soon`, `elevated-permissions-needed`, `env-var-already-exists`, `exchange-rate-fetch-failed`, `expired-conference-token`, `failed-to-charge-user`, `final-invoice-negative`, `full-permission-actor-blocked-for-admin`, `full-permission-actor-not-approved`, `github-branch-empty`, `github-issue-already-exists`, `github-public-key-not-found`, `github-repository-not-found`, `github-signature-does-not-match-payload`, `github-user-not-authorized-for-issues`, `gmail-not-allowed`, `id-does-not-match`, `incompatible-billing-interval`, `incomplete-payout-billing-info`, `inconsistent-currencies`, `incorrect-pricing-modifier-prefix`, `input-json-invalid-characters`, `input-json-not-object`, `input-json-too-long`, `input-update-collision`, `insufficient-permissions`, `insufficient-permissions-to-change-field`, `insufficient-security-measures`, `insufficient-tax-country-evidence`, `integration-auth-error`, `internal-server-error`, `invalid-billing-info`, `invalid-billing-period-for-payout`, `invalid-build`, `invalid-client-key`, `invalid-collection`, `invalid-conference-login-password`, `invalid-content-type-header`, `invalid-credentials`, `invalid-git-auth-token`, `invalid-github-issue-url`, `invalid-header`, `invalid-id`, `invalid-idempotency-key`, `invalid-input`, `invalid-input-schema`, `invalid-invoice`, `invalid-invoice-type`, `invalid-issue-date`, `invalid-label-params`, `invalid-main-account-user-id`, `invalid-oauth-app`, `invalid-oauth-scope`, `invalid-one-time-invoice`, `invalid-parameter`, `invalid-payout-status`, `invalid-picture-url`, `invalid-record-key`, `invalid-request`, `invalid-resource-type`, `invalid-signature`, `invalid-subscription-plan`, `invalid-tax-number`, `invalid-tax-number-format`, `invalid-token`, `invalid-token-type`, `invalid-two-factor-code`, `invalid-two-factor-code-or-recovery-code`, `invalid-two-factor-recovery-code`, `invalid-username`, `invalid-value`, `invitation-invalid-resource-type`, `invitation-no-longer-valid`, `invoice-canceled`, `invoice-cannot-be-refunded-due-to-too-high-amount`, `invoice-incomplete`, `invoice-is-draft`, `invoice-locked`, `invoice-must-be-buffer`, `invoice-not-canceled`, `invoice-not-draft`, `invoice-not-found`, `invoice-outdated`, `invoice-paid-already`, `issue-already-connected-to-github`, `issue-not-found`, `issues-bad-request`, `issuer-not-registered`, `job-finished`, `label-already-linked`, `last-api-token`, `limit-reached`, `max-items-must-be-greater-than-zero`, `max-metamorphs-exceeded`, `max-total-charge-usd-below-minimum`, `max-total-charge-usd-must-be-greater-than-zero`, `method-not-allowed`, `migration-disabled`, `missing-actor-rights`, `missing-api-token`, `missing-billing-info`, `missing-line-items`, `missing-payment-date`, `missing-payout-billing-info`, `missing-proxy-password`, `missing-reporting-fields`, `missing-resource-name`, `missing-settings`, `missing-username`, `monthly-usage-limit-too-low`, `more-than-one-update-not-allowed`, `multiple-records-found`, `must-be-admin`, `name-not-unique`, `next-runtime-computation-failed`, `no-columns-in-exported-dataset`, `no-payment-attempt-for-refund-found`, `no-payment-method-available`, `no-team-account-seats-available`, `non-temporary-email`, `not-enough-usage-to-run-paid-actor`, `not-implemented`, `not-supported-currencies`, `o-auth-service-already-connected`, `o-auth-service-not-connected`, `oauth-resource-access-failed`, `one-time-invoice-already-marked-paid`, `only-drafts-can-be-deleted`, `operation-canceled`, `operation-not-allowed`, `operation-timed-out`, `organization-cannot-own-itself`, `organization-role-not-found`, `overlapping-payout-billing-periods`, `own-token-required`, `page-not-found`, `param-not-one-of`, `parameter-required`, `parameters-mismatched`, `password-reset-email-already-sent`, `password-reset-token-expired`, `pay-as-you-go-without-monthly-interval`, `payment-attempt-status-message-required`, `payout-already-paid`, `payout-canceled`, `payout-invalid-state`, `payout-must-be-approved-to-be-marked-paid`, `payout-not-found`, `payout-number-already-exists`, `phone-number-invalid`, `phone-number-landline`, `phone-number-opted-out`, `phone-verification-disabled`, `platform-feature-disabled`, `price-overrides-validation-failed`, `pricing-model-not-supported`, `promotional-plan-not-available`, `proxy-auth-ip-not-unique`, `public-actor-disabled`, `query-timeout`, `quoted-price-outdated`, `rate-limit-exceeded`, `recaptcha-invalid`, `recaptcha-required`, `record-not-found`, `record-not-public`, `record-or-token-not-found`, `record-too-large`, `redirect-uri-mismatch`, `reduced-plan-not-available`, `rental-charge-already-reimbursed`, `rental-not-allowed`, `request-aborted-prematurely`, `request-handled-or-locked`, `request-id-invalid`, `request-queue-duplicate-requests`, `request-too-large`, `requested-dataset-view-does-not-exist`, `resume-token-expired`, `run-failed`, `run-input-body-not-valid-json`, `run-timeout-exceeded`, `russia-is-evil`, `same-user`, `schedule-actor-not-found`, `schedule-actor-task-not-found`, `schedule-name-not-unique`, `schema-validation`, `schema-validation-error`, `schema-validation-failed`, `service-worker-registration-not-allowed`, `sign-up-method-not-allowed`, `slack-integration-not-custom`, `socket-closed`, `socket-destroyed`, `store-schema-invalid`, `store-terms-not-accepted`, `stripe-enabled`, `stripe-generic-decline`, `stripe-not-enabled`, `stripe-not-enabled-for-user`, `tagged-build-required`, `tax-country-invalid`, `tax-number-invalid`, `tax-number-validation-failed`, `taxamo-call-failed`, `taxamo-request-failed`, `testing-error`, `token-not-provided`, `too-few-versions`, `too-many-actor-tasks`, `too-many-actors`, `too-many-labels-on-resource`, `too-many-mcp-connectors`, `too-many-o-auth-apps`, `too-many-organizations`, `too-many-requests`, `too-many-schedules`, `too-many-ui-access-keys`, `too-many-user-labels`, `too-many-values`, `too-many-versions`, `too-many-webhooks`, `unexpected-route`, `unknown-build-tag`, `unknown-payment-provider`, `unsubscribe-token-invalid`, `unsupported-actor-pricing-model-for-agentic-payments`, `unsupported-content-encoding`, `unsupported-file-type-for-issue`, `unsupported-file-type-image-expected`, `unsupported-file-type-text-or-json-expected`, `unsupported-permission`, `upcoming-subscription-bill-not-up-to-date`, `user-already-exists`, `user-already-verified`, `user-creates-organizations-too-fast`, `user-disabled`, `user-email-is-disposable`, `user-email-not-set`, `user-email-not-verified`, `user-has-no-subscription`, `user-integration-not-found`, `user-is-already-invited`, `user-is-already-organization-member`, `user-is-not-member-of-organization`, `user-is-not-organization`, `user-is-organization`, `user-is-organization-owner`, `user-is-removed`, `user-not-found`, `user-not-logged-in`, `user-not-verified`, `user-or-token-not-found`, `user-plan-not-allowed-for-coupon`, `user-problem-with-card`, `user-record-not-found`, `username-already-taken`, `username-missing`, `username-not-allowed`, `username-removal-forbidden`, `username-required`, `verification-email-already-sent`, `verification-token-expired`, `version-already-exists`, `versions-size-exceeded`, `weak-password`, `x402-agentic-payment-already-finalized`, `x402-agentic-payment-insufficient-amount`, `x402-agentic-payment-malformed-token`, `x402-agentic-payment-settlement-failed`, `x402-agentic-payment-settlement-in-progress`, `x402-agentic-payment-settlement-stuck`, `x402-agentic-payment-unauthorized`, `x402-payment-required`, `zero-invoice`]

  * **message** string

    Human-readable error message describing what went wrong.


```json
{

  "error": {

    "type": "unsupported-content-encoding",

    "message": "Content-Encoding \"bla\" is not supported."

  }

}
```


**Schema**

* **error** object required

  * **type** ErrorType (string)

    Machine-processable error type identifier.

    **Possible values:** \[`3d-secure-auth-failed`, `access-right-already-exists`, `action-not-found`, `actor-already-rented`, `actor-can-not-be-rented`, `actor-disabled`, `actor-is-not-rented`, `actor-memory-limit-exceeded`, `actor-name-exists-new-owner`, `actor-name-not-unique`, `actor-not-found`, `actor-not-github-actor`, `actor-not-public`, `actor-permission-level-not-supported-for-agentic-payments`, `actor-review-already-exists`, `actor-run-failed`, `actor-standby-not-supported-for-agentic-payments`, `actor-task-name-not-unique`, `agentic-payment-info-retrieval-error`, `agentic-payment-information-missing`, `agentic-payment-insufficient-amount`, `agentic-payment-provider-internal-error`, `agentic-payment-provider-unauthorized`, `airtable-webhook-deprecated`, `already-subscribed-to-paid-actor`, `apify-plan-required-to-use-paid-actor`, `apify-signup-not-allowed`, `auth-method-not-supported`, `authorization-server-not-found`, `auto-issue-date-invalid`, `background-check-required`, `billing-system-error`, `black-friday-plan-expired`, `braintree-error`, `braintree-not-linked`, `braintree-operation-timed-out`, `braintree-unsupported-currency`, `build-not-found`, `build-outdated`, `cannot-add-apify-events-to-ppe-actor`, `cannot-add-multiple-pricing-infos`, `cannot-add-pricing-info-that-alters-past`, `cannot-add-second-future-pricing-info`, `cannot-build-actor-from-webhook`, `cannot-change-billing-interval`, `cannot-change-owner`, `cannot-charge-apify-event`, `cannot-charge-non-pay-per-event-actor`, `cannot-comment-as-other-user`, `cannot-copy-actor-task`, `cannot-create-payout`, `cannot-create-public-actor`, `cannot-create-tax-transaction`, `cannot-delete-critical-actor`, `cannot-delete-invoice`, `cannot-delete-paid-actor`, `cannot-disable-one-time-event-for-apify-start-event`, `cannot-disable-organization-with-enabled-members`, `cannot-disable-user-with-subscription`, `cannot-link-oauth-to-unverified-email`, `cannot-metamorph-to-pay-per-result-actor`, `cannot-modify-actor-pricing-too-frequently`, `cannot-modify-actor-pricing-with-immediate-effect`, `cannot-monetize-without-payout-billing-info`, `cannot-override-paid-actor-trial`, `cannot-permanently-delete-subscription`, `cannot-publish-actor`, `cannot-publish-actor-task`, `cannot-reduce-last-full-token`, `cannot-reimburse-more-than-original-charge`, `cannot-reimburse-non-rental-charge`, `cannot-remove-own-actor-from-recently-used`, `cannot-remove-payment-method`, `cannot-remove-pricing-info`, `cannot-remove-running-run`, `cannot-remove-user-with-public-actors`, `cannot-remove-user-with-subscription`, `cannot-remove-user-with-unpaid-invoice`, `cannot-rename-env-var`, `cannot-rent-paid-actor`, `cannot-review-own-actor`, `cannot-set-access-rights-for-owner`, `cannot-set-is-status-message-terminal`, `cannot-unpublish-critical-actor`, `cannot-unpublish-paid-actor`, `cannot-unpublish-profile`, `cannot-update-invoice-field`, `concurrent-runs-limit-exceeded`, `concurrent-update-detected`, `conference-token-not-found`, `content-encoding-forbidden-for-html`, `coupon-already-redeemed`, `coupon-expired`, `coupon-for-new-customers`, `coupon-for-subscribed-users`, `coupon-limits-are-in-conflict-with-current-limits`, `coupon-max-number-of-redemptions-reached`, `coupon-not-found`, `coupon-not-unique`, `coupons-disabled`, `create-github-issue-not-allowed`, `creator-plan-not-available`, `cron-expression-invalid`, `daily-ai-token-limit-exceeded`, `daily-publication-limit-exceeded`, `dataset-does-not-have-fields-schema`, `dataset-does-not-have-schema`, `dataset-locked`, `dataset-schema-invalid`, `dcr-not-supported`, `default-dataset-not-found`, `deleting-default-build`, `deleting-unfinished-build`, `email-already-taken`, `email-already-taken-removed-user`, `email-domain-not-allowed-for-coupon`, `email-invalid`, `email-not-allowed`, `email-not-valid`, `email-update-too-soon`, `elevated-permissions-needed`, `env-var-already-exists`, `exchange-rate-fetch-failed`, `expired-conference-token`, `failed-to-charge-user`, `final-invoice-negative`, `full-permission-actor-blocked-for-admin`, `full-permission-actor-not-approved`, `github-branch-empty`, `github-issue-already-exists`, `github-public-key-not-found`, `github-repository-not-found`, `github-signature-does-not-match-payload`, `github-user-not-authorized-for-issues`, `gmail-not-allowed`, `id-does-not-match`, `incompatible-billing-interval`, `incomplete-payout-billing-info`, `inconsistent-currencies`, `incorrect-pricing-modifier-prefix`, `input-json-invalid-characters`, `input-json-not-object`, `input-json-too-long`, `input-update-collision`, `insufficient-permissions`, `insufficient-permissions-to-change-field`, `insufficient-security-measures`, `insufficient-tax-country-evidence`, `integration-auth-error`, `internal-server-error`, `invalid-billing-info`, `invalid-billing-period-for-payout`, `invalid-build`, `invalid-client-key`, `invalid-collection`, `invalid-conference-login-password`, `invalid-content-type-header`, `invalid-credentials`, `invalid-git-auth-token`, `invalid-github-issue-url`, `invalid-header`, `invalid-id`, `invalid-idempotency-key`, `invalid-input`, `invalid-input-schema`, `invalid-invoice`, `invalid-invoice-type`, `invalid-issue-date`, `invalid-label-params`, `invalid-main-account-user-id`, `invalid-oauth-app`, `invalid-oauth-scope`, `invalid-one-time-invoice`, `invalid-parameter`, `invalid-payout-status`, `invalid-picture-url`, `invalid-record-key`, `invalid-request`, `invalid-resource-type`, `invalid-signature`, `invalid-subscription-plan`, `invalid-tax-number`, `invalid-tax-number-format`, `invalid-token`, `invalid-token-type`, `invalid-two-factor-code`, `invalid-two-factor-code-or-recovery-code`, `invalid-two-factor-recovery-code`, `invalid-username`, `invalid-value`, `invitation-invalid-resource-type`, `invitation-no-longer-valid`, `invoice-canceled`, `invoice-cannot-be-refunded-due-to-too-high-amount`, `invoice-incomplete`, `invoice-is-draft`, `invoice-locked`, `invoice-must-be-buffer`, `invoice-not-canceled`, `invoice-not-draft`, `invoice-not-found`, `invoice-outdated`, `invoice-paid-already`, `issue-already-connected-to-github`, `issue-not-found`, `issues-bad-request`, `issuer-not-registered`, `job-finished`, `label-already-linked`, `last-api-token`, `limit-reached`, `max-items-must-be-greater-than-zero`, `max-metamorphs-exceeded`, `max-total-charge-usd-below-minimum`, `max-total-charge-usd-must-be-greater-than-zero`, `method-not-allowed`, `migration-disabled`, `missing-actor-rights`, `missing-api-token`, `missing-billing-info`, `missing-line-items`, `missing-payment-date`, `missing-payout-billing-info`, `missing-proxy-password`, `missing-reporting-fields`, `missing-resource-name`, `missing-settings`, `missing-username`, `monthly-usage-limit-too-low`, `more-than-one-update-not-allowed`, `multiple-records-found`, `must-be-admin`, `name-not-unique`, `next-runtime-computation-failed`, `no-columns-in-exported-dataset`, `no-payment-attempt-for-refund-found`, `no-payment-method-available`, `no-team-account-seats-available`, `non-temporary-email`, `not-enough-usage-to-run-paid-actor`, `not-implemented`, `not-supported-currencies`, `o-auth-service-already-connected`, `o-auth-service-not-connected`, `oauth-resource-access-failed`, `one-time-invoice-already-marked-paid`, `only-drafts-can-be-deleted`, `operation-canceled`, `operation-not-allowed`, `operation-timed-out`, `organization-cannot-own-itself`, `organization-role-not-found`, `overlapping-payout-billing-periods`, `own-token-required`, `page-not-found`, `param-not-one-of`, `parameter-required`, `parameters-mismatched`, `password-reset-email-already-sent`, `password-reset-token-expired`, `pay-as-you-go-without-monthly-interval`, `payment-attempt-status-message-required`, `payout-already-paid`, `payout-canceled`, `payout-invalid-state`, `payout-must-be-approved-to-be-marked-paid`, `payout-not-found`, `payout-number-already-exists`, `phone-number-invalid`, `phone-number-landline`, `phone-number-opted-out`, `phone-verification-disabled`, `platform-feature-disabled`, `price-overrides-validation-failed`, `pricing-model-not-supported`, `promotional-plan-not-available`, `proxy-auth-ip-not-unique`, `public-actor-disabled`, `query-timeout`, `quoted-price-outdated`, `rate-limit-exceeded`, `recaptcha-invalid`, `recaptcha-required`, `record-not-found`, `record-not-public`, `record-or-token-not-found`, `record-too-large`, `redirect-uri-mismatch`, `reduced-plan-not-available`, `rental-charge-already-reimbursed`, `rental-not-allowed`, `request-aborted-prematurely`, `request-handled-or-locked`, `request-id-invalid`, `request-queue-duplicate-requests`, `request-too-large`, `requested-dataset-view-does-not-exist`, `resume-token-expired`, `run-failed`, `run-input-body-not-valid-json`, `run-timeout-exceeded`, `russia-is-evil`, `same-user`, `schedule-actor-not-found`, `schedule-actor-task-not-found`, `schedule-name-not-unique`, `schema-validation`, `schema-validation-error`, `schema-validation-failed`, `service-worker-registration-not-allowed`, `sign-up-method-not-allowed`, `slack-integration-not-custom`, `socket-closed`, `socket-destroyed`, `store-schema-invalid`, `store-terms-not-accepted`, `stripe-enabled`, `stripe-generic-decline`, `stripe-not-enabled`, `stripe-not-enabled-for-user`, `tagged-build-required`, `tax-country-invalid`, `tax-number-invalid`, `tax-number-validation-failed`, `taxamo-call-failed`, `taxamo-request-failed`, `testing-error`, `token-not-provided`, `too-few-versions`, `too-many-actor-tasks`, `too-many-actors`, `too-many-labels-on-resource`, `too-many-mcp-connectors`, `too-many-o-auth-apps`, `too-many-organizations`, `too-many-requests`, `too-many-schedules`, `too-many-ui-access-keys`, `too-many-user-labels`, `too-many-values`, `too-many-versions`, `too-many-webhooks`, `unexpected-route`, `unknown-build-tag`, `unknown-payment-provider`, `unsubscribe-token-invalid`, `unsupported-actor-pricing-model-for-agentic-payments`, `unsupported-content-encoding`, `unsupported-file-type-for-issue`, `unsupported-file-type-image-expected`, `unsupported-file-type-text-or-json-expected`, `unsupported-permission`, `upcoming-subscription-bill-not-up-to-date`, `user-already-exists`, `user-already-verified`, `user-creates-organizations-too-fast`, `user-disabled`, `user-email-is-disposable`, `user-email-not-set`, `user-email-not-verified`, `user-has-no-subscription`, `user-integration-not-found`, `user-is-already-invited`, `user-is-already-organization-member`, `user-is-not-member-of-organization`, `user-is-not-organization`, `user-is-organization`, `user-is-organization-owner`, `user-is-removed`, `user-not-found`, `user-not-logged-in`, `user-not-verified`, `user-or-token-not-found`, `user-plan-not-allowed-for-coupon`, `user-problem-with-card`, `user-record-not-found`, `username-already-taken`, `username-missing`, `username-not-allowed`, `username-removal-forbidden`, `username-required`, `verification-email-already-sent`, `verification-token-expired`, `version-already-exists`, `versions-size-exceeded`, `weak-password`, `x402-agentic-payment-already-finalized`, `x402-agentic-payment-insufficient-amount`, `x402-agentic-payment-malformed-token`, `x402-agentic-payment-settlement-failed`, `x402-agentic-payment-settlement-in-progress`, `x402-agentic-payment-settlement-stuck`, `x402-agentic-payment-unauthorized`, `x402-payment-required`, `zero-invoice`]

  * **message** string

    Human-readable error message describing what went wrong.

### Status 429

Too many requests - rate limit exceeded.


```json
{

  "error": {

    "type": "rate-limit-exceeded",

    "message": "You have exceeded the rate limit. Please try again later."

  }

}
```


**Schema**

* **error** object required

  * **type** ErrorType (string)

    Machine-processable error type identifier.

    **Possible values:** \[`3d-secure-auth-failed`, `access-right-already-exists`, `action-not-found`, `actor-already-rented`, `actor-can-not-be-rented`, `actor-disabled`, `actor-is-not-rented`, `actor-memory-limit-exceeded`, `actor-name-exists-new-owner`, `actor-name-not-unique`, `actor-not-found`, `actor-not-github-actor`, `actor-not-public`, `actor-permission-level-not-supported-for-agentic-payments`, `actor-review-already-exists`, `actor-run-failed`, `actor-standby-not-supported-for-agentic-payments`, `actor-task-name-not-unique`, `agentic-payment-info-retrieval-error`, `agentic-payment-information-missing`, `agentic-payment-insufficient-amount`, `agentic-payment-provider-internal-error`, `agentic-payment-provider-unauthorized`, `airtable-webhook-deprecated`, `already-subscribed-to-paid-actor`, `apify-plan-required-to-use-paid-actor`, `apify-signup-not-allowed`, `auth-method-not-supported`, `authorization-server-not-found`, `auto-issue-date-invalid`, `background-check-required`, `billing-system-error`, `black-friday-plan-expired`, `braintree-error`, `braintree-not-linked`, `braintree-operation-timed-out`, `braintree-unsupported-currency`, `build-not-found`, `build-outdated`, `cannot-add-apify-events-to-ppe-actor`, `cannot-add-multiple-pricing-infos`, `cannot-add-pricing-info-that-alters-past`, `cannot-add-second-future-pricing-info`, `cannot-build-actor-from-webhook`, `cannot-change-billing-interval`, `cannot-change-owner`, `cannot-charge-apify-event`, `cannot-charge-non-pay-per-event-actor`, `cannot-comment-as-other-user`, `cannot-copy-actor-task`, `cannot-create-payout`, `cannot-create-public-actor`, `cannot-create-tax-transaction`, `cannot-delete-critical-actor`, `cannot-delete-invoice`, `cannot-delete-paid-actor`, `cannot-disable-one-time-event-for-apify-start-event`, `cannot-disable-organization-with-enabled-members`, `cannot-disable-user-with-subscription`, `cannot-link-oauth-to-unverified-email`, `cannot-metamorph-to-pay-per-result-actor`, `cannot-modify-actor-pricing-too-frequently`, `cannot-modify-actor-pricing-with-immediate-effect`, `cannot-monetize-without-payout-billing-info`, `cannot-override-paid-actor-trial`, `cannot-permanently-delete-subscription`, `cannot-publish-actor`, `cannot-publish-actor-task`, `cannot-reduce-last-full-token`, `cannot-reimburse-more-than-original-charge`, `cannot-reimburse-non-rental-charge`, `cannot-remove-own-actor-from-recently-used`, `cannot-remove-payment-method`, `cannot-remove-pricing-info`, `cannot-remove-running-run`, `cannot-remove-user-with-public-actors`, `cannot-remove-user-with-subscription`, `cannot-remove-user-with-unpaid-invoice`, `cannot-rename-env-var`, `cannot-rent-paid-actor`, `cannot-review-own-actor`, `cannot-set-access-rights-for-owner`, `cannot-set-is-status-message-terminal`, `cannot-unpublish-critical-actor`, `cannot-unpublish-paid-actor`, `cannot-unpublish-profile`, `cannot-update-invoice-field`, `concurrent-runs-limit-exceeded`, `concurrent-update-detected`, `conference-token-not-found`, `content-encoding-forbidden-for-html`, `coupon-already-redeemed`, `coupon-expired`, `coupon-for-new-customers`, `coupon-for-subscribed-users`, `coupon-limits-are-in-conflict-with-current-limits`, `coupon-max-number-of-redemptions-reached`, `coupon-not-found`, `coupon-not-unique`, `coupons-disabled`, `create-github-issue-not-allowed`, `creator-plan-not-available`, `cron-expression-invalid`, `daily-ai-token-limit-exceeded`, `daily-publication-limit-exceeded`, `dataset-does-not-have-fields-schema`, `dataset-does-not-have-schema`, `dataset-locked`, `dataset-schema-invalid`, `dcr-not-supported`, `default-dataset-not-found`, `deleting-default-build`, `deleting-unfinished-build`, `email-already-taken`, `email-already-taken-removed-user`, `email-domain-not-allowed-for-coupon`, `email-invalid`, `email-not-allowed`, `email-not-valid`, `email-update-too-soon`, `elevated-permissions-needed`, `env-var-already-exists`, `exchange-rate-fetch-failed`, `expired-conference-token`, `failed-to-charge-user`, `final-invoice-negative`, `full-permission-actor-blocked-for-admin`, `full-permission-actor-not-approved`, `github-branch-empty`, `github-issue-already-exists`, `github-public-key-not-found`, `github-repository-not-found`, `github-signature-does-not-match-payload`, `github-user-not-authorized-for-issues`, `gmail-not-allowed`, `id-does-not-match`, `incompatible-billing-interval`, `incomplete-payout-billing-info`, `inconsistent-currencies`, `incorrect-pricing-modifier-prefix`, `input-json-invalid-characters`, `input-json-not-object`, `input-json-too-long`, `input-update-collision`, `insufficient-permissions`, `insufficient-permissions-to-change-field`, `insufficient-security-measures`, `insufficient-tax-country-evidence`, `integration-auth-error`, `internal-server-error`, `invalid-billing-info`, `invalid-billing-period-for-payout`, `invalid-build`, `invalid-client-key`, `invalid-collection`, `invalid-conference-login-password`, `invalid-content-type-header`, `invalid-credentials`, `invalid-git-auth-token`, `invalid-github-issue-url`, `invalid-header`, `invalid-id`, `invalid-idempotency-key`, `invalid-input`, `invalid-input-schema`, `invalid-invoice`, `invalid-invoice-type`, `invalid-issue-date`, `invalid-label-params`, `invalid-main-account-user-id`, `invalid-oauth-app`, `invalid-oauth-scope`, `invalid-one-time-invoice`, `invalid-parameter`, `invalid-payout-status`, `invalid-picture-url`, `invalid-record-key`, `invalid-request`, `invalid-resource-type`, `invalid-signature`, `invalid-subscription-plan`, `invalid-tax-number`, `invalid-tax-number-format`, `invalid-token`, `invalid-token-type`, `invalid-two-factor-code`, `invalid-two-factor-code-or-recovery-code`, `invalid-two-factor-recovery-code`, `invalid-username`, `invalid-value`, `invitation-invalid-resource-type`, `invitation-no-longer-valid`, `invoice-canceled`, `invoice-cannot-be-refunded-due-to-too-high-amount`, `invoice-incomplete`, `invoice-is-draft`, `invoice-locked`, `invoice-must-be-buffer`, `invoice-not-canceled`, `invoice-not-draft`, `invoice-not-found`, `invoice-outdated`, `invoice-paid-already`, `issue-already-connected-to-github`, `issue-not-found`, `issues-bad-request`, `issuer-not-registered`, `job-finished`, `label-already-linked`, `last-api-token`, `limit-reached`, `max-items-must-be-greater-than-zero`, `max-metamorphs-exceeded`, `max-total-charge-usd-below-minimum`, `max-total-charge-usd-must-be-greater-than-zero`, `method-not-allowed`, `migration-disabled`, `missing-actor-rights`, `missing-api-token`, `missing-billing-info`, `missing-line-items`, `missing-payment-date`, `missing-payout-billing-info`, `missing-proxy-password`, `missing-reporting-fields`, `missing-resource-name`, `missing-settings`, `missing-username`, `monthly-usage-limit-too-low`, `more-than-one-update-not-allowed`, `multiple-records-found`, `must-be-admin`, `name-not-unique`, `next-runtime-computation-failed`, `no-columns-in-exported-dataset`, `no-payment-attempt-for-refund-found`, `no-payment-method-available`, `no-team-account-seats-available`, `non-temporary-email`, `not-enough-usage-to-run-paid-actor`, `not-implemented`, `not-supported-currencies`, `o-auth-service-already-connected`, `o-auth-service-not-connected`, `oauth-resource-access-failed`, `one-time-invoice-already-marked-paid`, `only-drafts-can-be-deleted`, `operation-canceled`, `operation-not-allowed`, `operation-timed-out`, `organization-cannot-own-itself`, `organization-role-not-found`, `overlapping-payout-billing-periods`, `own-token-required`, `page-not-found`, `param-not-one-of`, `parameter-required`, `parameters-mismatched`, `password-reset-email-already-sent`, `password-reset-token-expired`, `pay-as-you-go-without-monthly-interval`, `payment-attempt-status-message-required`, `payout-already-paid`, `payout-canceled`, `payout-invalid-state`, `payout-must-be-approved-to-be-marked-paid`, `payout-not-found`, `payout-number-already-exists`, `phone-number-invalid`, `phone-number-landline`, `phone-number-opted-out`, `phone-verification-disabled`, `platform-feature-disabled`, `price-overrides-validation-failed`, `pricing-model-not-supported`, `promotional-plan-not-available`, `proxy-auth-ip-not-unique`, `public-actor-disabled`, `query-timeout`, `quoted-price-outdated`, `rate-limit-exceeded`, `recaptcha-invalid`, `recaptcha-required`, `record-not-found`, `record-not-public`, `record-or-token-not-found`, `record-too-large`, `redirect-uri-mismatch`, `reduced-plan-not-available`, `rental-charge-already-reimbursed`, `rental-not-allowed`, `request-aborted-prematurely`, `request-handled-or-locked`, `request-id-invalid`, `request-queue-duplicate-requests`, `request-too-large`, `requested-dataset-view-does-not-exist`, `resume-token-expired`, `run-failed`, `run-input-body-not-valid-json`, `run-timeout-exceeded`, `russia-is-evil`, `same-user`, `schedule-actor-not-found`, `schedule-actor-task-not-found`, `schedule-name-not-unique`, `schema-validation`, `schema-validation-error`, `schema-validation-failed`, `service-worker-registration-not-allowed`, `sign-up-method-not-allowed`, `slack-integration-not-custom`, `socket-closed`, `socket-destroyed`, `store-schema-invalid`, `store-terms-not-accepted`, `stripe-enabled`, `stripe-generic-decline`, `stripe-not-enabled`, `stripe-not-enabled-for-user`, `tagged-build-required`, `tax-country-invalid`, `tax-number-invalid`, `tax-number-validation-failed`, `taxamo-call-failed`, `taxamo-request-failed`, `testing-error`, `token-not-provided`, `too-few-versions`, `too-many-actor-tasks`, `too-many-actors`, `too-many-labels-on-resource`, `too-many-mcp-connectors`, `too-many-o-auth-apps`, `too-many-organizations`, `too-many-requests`, `too-many-schedules`, `too-many-ui-access-keys`, `too-many-user-labels`, `too-many-values`, `too-many-versions`, `too-many-webhooks`, `unexpected-route`, `unknown-build-tag`, `unknown-payment-provider`, `unsubscribe-token-invalid`, `unsupported-actor-pricing-model-for-agentic-payments`, `unsupported-content-encoding`, `unsupported-file-type-for-issue`, `unsupported-file-type-image-expected`, `unsupported-file-type-text-or-json-expected`, `unsupported-permission`, `upcoming-subscription-bill-not-up-to-date`, `user-already-exists`, `user-already-verified`, `user-creates-organizations-too-fast`, `user-disabled`, `user-email-is-disposable`, `user-email-not-set`, `user-email-not-verified`, `user-has-no-subscription`, `user-integration-not-found`, `user-is-already-invited`, `user-is-already-organization-member`, `user-is-not-member-of-organization`, `user-is-not-organization`, `user-is-organization`, `user-is-organization-owner`, `user-is-removed`, `user-not-found`, `user-not-logged-in`, `user-not-verified`, `user-or-token-not-found`, `user-plan-not-allowed-for-coupon`, `user-problem-with-card`, `user-record-not-found`, `username-already-taken`, `username-missing`, `username-not-allowed`, `username-removal-forbidden`, `username-required`, `verification-email-already-sent`, `verification-token-expired`, `version-already-exists`, `versions-size-exceeded`, `weak-password`, `x402-agentic-payment-already-finalized`, `x402-agentic-payment-insufficient-amount`, `x402-agentic-payment-malformed-token`, `x402-agentic-payment-settlement-failed`, `x402-agentic-payment-settlement-in-progress`, `x402-agentic-payment-settlement-stuck`, `x402-agentic-payment-unauthorized`, `x402-payment-required`, `zero-invoice`]

  * **message** string

    Human-readable error message describing what went wrong.


```json
{

  "error": {

    "type": "rate-limit-exceeded",

    "message": "You have exceeded the rate limit. Please try again later."

  }

}
```


**Schema**

* **error** object required

  * **type** ErrorType (string)

    Machine-processable error type identifier.

    **Possible values:** \[`3d-secure-auth-failed`, `access-right-already-exists`, `action-not-found`, `actor-already-rented`, `actor-can-not-be-rented`, `actor-disabled`, `actor-is-not-rented`, `actor-memory-limit-exceeded`, `actor-name-exists-new-owner`, `actor-name-not-unique`, `actor-not-found`, `actor-not-github-actor`, `actor-not-public`, `actor-permission-level-not-supported-for-agentic-payments`, `actor-review-already-exists`, `actor-run-failed`, `actor-standby-not-supported-for-agentic-payments`, `actor-task-name-not-unique`, `agentic-payment-info-retrieval-error`, `agentic-payment-information-missing`, `agentic-payment-insufficient-amount`, `agentic-payment-provider-internal-error`, `agentic-payment-provider-unauthorized`, `airtable-webhook-deprecated`, `already-subscribed-to-paid-actor`, `apify-plan-required-to-use-paid-actor`, `apify-signup-not-allowed`, `auth-method-not-supported`, `authorization-server-not-found`, `auto-issue-date-invalid`, `background-check-required`, `billing-system-error`, `black-friday-plan-expired`, `braintree-error`, `braintree-not-linked`, `braintree-operation-timed-out`, `braintree-unsupported-currency`, `build-not-found`, `build-outdated`, `cannot-add-apify-events-to-ppe-actor`, `cannot-add-multiple-pricing-infos`, `cannot-add-pricing-info-that-alters-past`, `cannot-add-second-future-pricing-info`, `cannot-build-actor-from-webhook`, `cannot-change-billing-interval`, `cannot-change-owner`, `cannot-charge-apify-event`, `cannot-charge-non-pay-per-event-actor`, `cannot-comment-as-other-user`, `cannot-copy-actor-task`, `cannot-create-payout`, `cannot-create-public-actor`, `cannot-create-tax-transaction`, `cannot-delete-critical-actor`, `cannot-delete-invoice`, `cannot-delete-paid-actor`, `cannot-disable-one-time-event-for-apify-start-event`, `cannot-disable-organization-with-enabled-members`, `cannot-disable-user-with-subscription`, `cannot-link-oauth-to-unverified-email`, `cannot-metamorph-to-pay-per-result-actor`, `cannot-modify-actor-pricing-too-frequently`, `cannot-modify-actor-pricing-with-immediate-effect`, `cannot-monetize-without-payout-billing-info`, `cannot-override-paid-actor-trial`, `cannot-permanently-delete-subscription`, `cannot-publish-actor`, `cannot-publish-actor-task`, `cannot-reduce-last-full-token`, `cannot-reimburse-more-than-original-charge`, `cannot-reimburse-non-rental-charge`, `cannot-remove-own-actor-from-recently-used`, `cannot-remove-payment-method`, `cannot-remove-pricing-info`, `cannot-remove-running-run`, `cannot-remove-user-with-public-actors`, `cannot-remove-user-with-subscription`, `cannot-remove-user-with-unpaid-invoice`, `cannot-rename-env-var`, `cannot-rent-paid-actor`, `cannot-review-own-actor`, `cannot-set-access-rights-for-owner`, `cannot-set-is-status-message-terminal`, `cannot-unpublish-critical-actor`, `cannot-unpublish-paid-actor`, `cannot-unpublish-profile`, `cannot-update-invoice-field`, `concurrent-runs-limit-exceeded`, `concurrent-update-detected`, `conference-token-not-found`, `content-encoding-forbidden-for-html`, `coupon-already-redeemed`, `coupon-expired`, `coupon-for-new-customers`, `coupon-for-subscribed-users`, `coupon-limits-are-in-conflict-with-current-limits`, `coupon-max-number-of-redemptions-reached`, `coupon-not-found`, `coupon-not-unique`, `coupons-disabled`, `create-github-issue-not-allowed`, `creator-plan-not-available`, `cron-expression-invalid`, `daily-ai-token-limit-exceeded`, `daily-publication-limit-exceeded`, `dataset-does-not-have-fields-schema`, `dataset-does-not-have-schema`, `dataset-locked`, `dataset-schema-invalid`, `dcr-not-supported`, `default-dataset-not-found`, `deleting-default-build`, `deleting-unfinished-build`, `email-already-taken`, `email-already-taken-removed-user`, `email-domain-not-allowed-for-coupon`, `email-invalid`, `email-not-allowed`, `email-not-valid`, `email-update-too-soon`, `elevated-permissions-needed`, `env-var-already-exists`, `exchange-rate-fetch-failed`, `expired-conference-token`, `failed-to-charge-user`, `final-invoice-negative`, `full-permission-actor-blocked-for-admin`, `full-permission-actor-not-approved`, `github-branch-empty`, `github-issue-already-exists`, `github-public-key-not-found`, `github-repository-not-found`, `github-signature-does-not-match-payload`, `github-user-not-authorized-for-issues`, `gmail-not-allowed`, `id-does-not-match`, `incompatible-billing-interval`, `incomplete-payout-billing-info`, `inconsistent-currencies`, `incorrect-pricing-modifier-prefix`, `input-json-invalid-characters`, `input-json-not-object`, `input-json-too-long`, `input-update-collision`, `insufficient-permissions`, `insufficient-permissions-to-change-field`, `insufficient-security-measures`, `insufficient-tax-country-evidence`, `integration-auth-error`, `internal-server-error`, `invalid-billing-info`, `invalid-billing-period-for-payout`, `invalid-build`, `invalid-client-key`, `invalid-collection`, `invalid-conference-login-password`, `invalid-content-type-header`, `invalid-credentials`, `invalid-git-auth-token`, `invalid-github-issue-url`, `invalid-header`, `invalid-id`, `invalid-idempotency-key`, `invalid-input`, `invalid-input-schema`, `invalid-invoice`, `invalid-invoice-type`, `invalid-issue-date`, `invalid-label-params`, `invalid-main-account-user-id`, `invalid-oauth-app`, `invalid-oauth-scope`, `invalid-one-time-invoice`, `invalid-parameter`, `invalid-payout-status`, `invalid-picture-url`, `invalid-record-key`, `invalid-request`, `invalid-resource-type`, `invalid-signature`, `invalid-subscription-plan`, `invalid-tax-number`, `invalid-tax-number-format`, `invalid-token`, `invalid-token-type`, `invalid-two-factor-code`, `invalid-two-factor-code-or-recovery-code`, `invalid-two-factor-recovery-code`, `invalid-username`, `invalid-value`, `invitation-invalid-resource-type`, `invitation-no-longer-valid`, `invoice-canceled`, `invoice-cannot-be-refunded-due-to-too-high-amount`, `invoice-incomplete`, `invoice-is-draft`, `invoice-locked`, `invoice-must-be-buffer`, `invoice-not-canceled`, `invoice-not-draft`, `invoice-not-found`, `invoice-outdated`, `invoice-paid-already`, `issue-already-connected-to-github`, `issue-not-found`, `issues-bad-request`, `issuer-not-registered`, `job-finished`, `label-already-linked`, `last-api-token`, `limit-reached`, `max-items-must-be-greater-than-zero`, `max-metamorphs-exceeded`, `max-total-charge-usd-below-minimum`, `max-total-charge-usd-must-be-greater-than-zero`, `method-not-allowed`, `migration-disabled`, `missing-actor-rights`, `missing-api-token`, `missing-billing-info`, `missing-line-items`, `missing-payment-date`, `missing-payout-billing-info`, `missing-proxy-password`, `missing-reporting-fields`, `missing-resource-name`, `missing-settings`, `missing-username`, `monthly-usage-limit-too-low`, `more-than-one-update-not-allowed`, `multiple-records-found`, `must-be-admin`, `name-not-unique`, `next-runtime-computation-failed`, `no-columns-in-exported-dataset`, `no-payment-attempt-for-refund-found`, `no-payment-method-available`, `no-team-account-seats-available`, `non-temporary-email`, `not-enough-usage-to-run-paid-actor`, `not-implemented`, `not-supported-currencies`, `o-auth-service-already-connected`, `o-auth-service-not-connected`, `oauth-resource-access-failed`, `one-time-invoice-already-marked-paid`, `only-drafts-can-be-deleted`, `operation-canceled`, `operation-not-allowed`, `operation-timed-out`, `organization-cannot-own-itself`, `organization-role-not-found`, `overlapping-payout-billing-periods`, `own-token-required`, `page-not-found`, `param-not-one-of`, `parameter-required`, `parameters-mismatched`, `password-reset-email-already-sent`, `password-reset-token-expired`, `pay-as-you-go-without-monthly-interval`, `payment-attempt-status-message-required`, `payout-already-paid`, `payout-canceled`, `payout-invalid-state`, `payout-must-be-approved-to-be-marked-paid`, `payout-not-found`, `payout-number-already-exists`, `phone-number-invalid`, `phone-number-landline`, `phone-number-opted-out`, `phone-verification-disabled`, `platform-feature-disabled`, `price-overrides-validation-failed`, `pricing-model-not-supported`, `promotional-plan-not-available`, `proxy-auth-ip-not-unique`, `public-actor-disabled`, `query-timeout`, `quoted-price-outdated`, `rate-limit-exceeded`, `recaptcha-invalid`, `recaptcha-required`, `record-not-found`, `record-not-public`, `record-or-token-not-found`, `record-too-large`, `redirect-uri-mismatch`, `reduced-plan-not-available`, `rental-charge-already-reimbursed`, `rental-not-allowed`, `request-aborted-prematurely`, `request-handled-or-locked`, `request-id-invalid`, `request-queue-duplicate-requests`, `request-too-large`, `requested-dataset-view-does-not-exist`, `resume-token-expired`, `run-failed`, `run-input-body-not-valid-json`, `run-timeout-exceeded`, `russia-is-evil`, `same-user`, `schedule-actor-not-found`, `schedule-actor-task-not-found`, `schedule-name-not-unique`, `schema-validation`, `schema-validation-error`, `schema-validation-failed`, `service-worker-registration-not-allowed`, `sign-up-method-not-allowed`, `slack-integration-not-custom`, `socket-closed`, `socket-destroyed`, `store-schema-invalid`, `store-terms-not-accepted`, `stripe-enabled`, `stripe-generic-decline`, `stripe-not-enabled`, `stripe-not-enabled-for-user`, `tagged-build-required`, `tax-country-invalid`, `tax-number-invalid`, `tax-number-validation-failed`, `taxamo-call-failed`, `taxamo-request-failed`, `testing-error`, `token-not-provided`, `too-few-versions`, `too-many-actor-tasks`, `too-many-actors`, `too-many-labels-on-resource`, `too-many-mcp-connectors`, `too-many-o-auth-apps`, `too-many-organizations`, `too-many-requests`, `too-many-schedules`, `too-many-ui-access-keys`, `too-many-user-labels`, `too-many-values`, `too-many-versions`, `too-many-webhooks`, `unexpected-route`, `unknown-build-tag`, `unknown-payment-provider`, `unsubscribe-token-invalid`, `unsupported-actor-pricing-model-for-agentic-payments`, `unsupported-content-encoding`, `unsupported-file-type-for-issue`, `unsupported-file-type-image-expected`, `unsupported-file-type-text-or-json-expected`, `unsupported-permission`, `upcoming-subscription-bill-not-up-to-date`, `user-already-exists`, `user-already-verified`, `user-creates-organizations-too-fast`, `user-disabled`, `user-email-is-disposable`, `user-email-not-set`, `user-email-not-verified`, `user-has-no-subscription`, `user-integration-not-found`, `user-is-already-invited`, `user-is-already-organization-member`, `user-is-not-member-of-organization`, `user-is-not-organization`, `user-is-organization`, `user-is-organization-owner`, `user-is-removed`, `user-not-found`, `user-not-logged-in`, `user-not-verified`, `user-or-token-not-found`, `user-plan-not-allowed-for-coupon`, `user-problem-with-card`, `user-record-not-found`, `username-already-taken`, `username-missing`, `username-not-allowed`, `username-removal-forbidden`, `username-required`, `verification-email-already-sent`, `verification-token-expired`, `version-already-exists`, `versions-size-exceeded`, `weak-password`, `x402-agentic-payment-already-finalized`, `x402-agentic-payment-insufficient-amount`, `x402-agentic-payment-malformed-token`, `x402-agentic-payment-settlement-failed`, `x402-agentic-payment-settlement-in-progress`, `x402-agentic-payment-settlement-stuck`, `x402-agentic-payment-unauthorized`, `x402-payment-required`, `zero-invoice`]

  * **message** string

    Human-readable error message describing what went wrong.

