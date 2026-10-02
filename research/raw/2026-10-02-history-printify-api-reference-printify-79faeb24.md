---
url: https://developers.printify.com/
retrieved: 2026-10-02
command: firecrawl scrape https://developers.printify.com/ --only-main-content --json
statusCode: 200
transport: firecrawl-cli
completeness: full
title: History – Printify API Reference
---
![Logo](https://developers.printify.com/images/logo-8fbbf816.svg)

# Automate your Print on Demand business

![](https://developers.printify.com/images/navbar-logo-b4688acd.svg)

- [Overview](https://developers.printify.com/#overview)  - [API Usage Guidelines](https://developers.printify.com/#api-usage-guidelines)
  - [OpenAPI specification](https://developers.printify.com/#openapi-specification)
- [API features](https://developers.printify.com/#api-features)  - [REST API](https://developers.printify.com/#rest-api)
  - [Webhooks and Events](https://developers.printify.com/#webhooks-and-events)
- [Access the Printify API](https://developers.printify.com/#access-the-printify-api)  - [Retrieving Shop ID](https://developers.printify.com/#retrieving-shop-id)
  - [Individual Accounts](https://developers.printify.com/#individual-accounts)
  - [Platforms](https://developers.printify.com/#platforms)
  - [Use cases](https://developers.printify.com/#use-cases)
- [Authentication](https://developers.printify.com/#authentication)  - [Create a personal access token](https://developers.printify.com/#create-a-personal-access-token)
  - [OAuth 2.0](https://developers.printify.com/#oauth-2-0)
  - [Access scopes](https://developers.printify.com/#access-scopes)
- [V1 API Reference](https://developers.printify.com/#v1-api-reference)  - [API basics](https://developers.printify.com/#api-basics)
  - [API pagination](https://developers.printify.com/#api-pagination)
  - [Shops](https://developers.printify.com/#shops)
  - [Catalog](https://developers.printify.com/#catalog)
  - [Products](https://developers.printify.com/#products)
  - [Orders](https://developers.printify.com/#orders)
  - [Personalization](https://developers.printify.com/#personalization)
  - [Uploads](https://developers.printify.com/#uploads)
  - [Events](https://developers.printify.com/#events)
  - [Webhooks](https://developers.printify.com/#webhooks)
- [V2 API Reference](https://developers.printify.com/#v2-api-reference)  - [Catalog V2](https://developers.printify.com/#catalog-v2)
- [HTTP Status Codes](https://developers.printify.com/#http-status-codes)  - [Success](https://developers.printify.com/#success)
  - [User error codes](https://developers.printify.com/#user-error-codes)
  - [Server error codes](https://developers.printify.com/#server-error-codes)
- [History](https://developers.printify.com/#history)

# Overview

This documentation describes the different ways to access our API services. It includes detailed
explanations and code examples to help you quickly create products and fulfill orders. The API supports
both the **Printify** and **Printful Enterprise** brands, with a shared API surface and brand-specific
differences documented where relevant.

## API Usage Guidelines

All integrations must comply with the Printify Terms and Printify API Terms. Please see these pages for more details:

- [https://printify.com/terms-of-service/](https://printify.com/terms-of-service/)
- [https://printify.com/API-terms/](https://printify.com/API-terms/)

The Printify public endpoints are powered by the same underlying technology that powers the core Printify Platform. As a
result, Printify engineering closely monitors usage of the public APIs to ensure a quality experience for users of the
Printify platform.
Below, you'll find the limits by which a single integration (identified per account and not per access token) can
consume the Printify APIs. If you have any questions, please [create a support ticket](https://help.printify.com/hc/en-us/requests/new?ticket_form_id=4421334895377) by selecting one of the topics on the support page and indicating "API" as the option chosen under "Channels". Please add more information to provide full details and we will contact you shortly.

Printify has the following global limit in place for API requests:

- 600 requests per minute.

Customers exceeding this limit will receive error responses with a 429 response code.

|     |     |
| --- | --- |
| ⚠ | All [Catalog API endpoints](https://developers.printify.com/#catalog) have a separate rate limit of **100 requests per minute** per integration (per account, not per access token) in addition to the global API limit.<br> Exceeding this limit will result in a **429 Too Many Requests** response. |

Integrations that use Printify's API to create products and generate mockups have an additional daily limit. The
[product publishing endpoint](https://developers.printify.com/#publish-a-product) has a limit of **200 requests per 30 minutes**, product
creation as a result of Order creation is not limited. If your application will require heavy usage of the Product
or Mockup generation functions, please [create a support ticket](https://help.printify.com/hc/en-us/requests/new?ticket_form_id=4421334895377) by selecting one of the topics on the support page and indicating "API" as the option chosen under "Channels". Please add more information to provide full details and we will contact you shortly.

Requests resulting in an error response may not exceed 5% of your total requests.

We reserve the right to change or deprecate the APIs over time - we will provide developers ample notification in those
cases. These notifications will be sent to the email provided in your API settings.

## OpenAPI specification

Download [OpenAPI specification](https://developers.printify.com/openapi.json)

# API features

## REST API

Printify's REST API allows your application to manage a Printify shop on behalf of a Printify Merchant. Create products,
submit orders, and more...

Check out all available methods: [API Reference](https://developers.printify.com/#api-reference)

## Webhooks and Events

Webhooks allow you to get an instant notification after an event occurrs in a Printify shop.

Send information to accounting right after an order was placed, send tracking to end customers as soon as it's
available, sync product descriptions, etc... - it's totally up to you.

More information:
[Webhooks](https://developers.printify.com/#webhooks)

# Access the Printify API

You can access the Printify API as an individual merchant or as a platform. Both of them require different types of
authentication. Learn about each of them below.

## Retrieving Shop ID

List all the shops associated with your account by calling [Shops API](https://developers.printify.com/#retrieve-a-list-of-existing-shops)`json
[\
    {\
      "id": 5432,\
      "title": "My new store",\
      "sales_channel": "My Sales Channel"\
    },\
    {\
      "id": 9876,\
      "title": "My other new store",\
      "sales_channel": "disconnected"\
    }\
]
`

Then select a shop and note down it's ID e.g. ID of `My new store` is `5432`.

You can now use that ID in all the placeholders marked as `{shop_id}` e.g. `GET /v1/shops/{shop_id}/products.json` =\> `GET /v1/shops/5432/products.json`

## Individual Accounts

Connect to a single Printify Merchant account and the shops that are a part of that account. Create products, submit
artwork, create and receive orders and more. Authentication is achieved through a Personal Access Token.

See more details in
[Authentication](https://developers.printify.com/#create-a-personal-access-token).

## Platforms

Connect applications that offer services to multiple merchants each with different Printify merchant accounts. Manage
orders for multiple Printify Merchants, offer merchants the option to sell on your platform, and more. Authentication is
achieved through OAuth 2.0

See more details in
[Authentication](https://developers.printify.com/#oauth-2-0)

## Use cases

### Create orders with user-generated content

Regardless of whether you use your own mockup generator, or you capture user generated content. Through the Printify API
you can easily place those images on any products in our catalog, offer them for purchase, and fulfill.

### Connect your own E-commerce channel

Don't use Etsy, Shopify, Woocommerce, or any of our other available E-commerce solutions? Connect your own with the
Printify API. Enjoy the same benefits of automation that merchants using our existing integrations do.

### Support existing integrations with more functionality

Already using one of our integrations such as Shopify or Woocommerce? Build any additional functionality you need and
connect via Printify API to continue to get all of your sales and order data in your existing shop.

### Start offering merchandise sales to your community

Do you have an application or platform with an engaged community. Connect to the Printify API and easily start
monetizing your community by allowing them to sell Print on Demand merchandise through your platform.

# Authentication

The Printify platform provides two ways of integrating. You can integrate with a Personal Access Token that you can use
to manage a single Printify account, or you can integrate through OAuth 2.0 as a platform that will be managing multiple
Printify Merchant accounts.

Unless otherwise mentioned in the documentation for a specific endpoint, all endpoints support both OAuth 2.0 and
Personal Access Token.

## Create a personal access token

A personal access token allows your application to connect to a single Printify Merchant account and the shops created within that account.

#### Step 1

Before creating your personal access token, you will first need a Printify account. If you haven't created an account yet, [please do so here](https://printify.com/app/register) and complete the onboarding procedure.

#### Step 2

Now that you have your Printify account, navigate to My Profile, then Connections. In the Connections section you will be able to generate your Personal Access Tokens and set your Token Access Scopes.

#### Step 3

You will be able to generate multiple tokens. Tokens can be set to have different Access Scopes.

Please note that for security purposes, this token will only be visible immediately after generating only. Please make sure you store it in a secure location.

Access tokens are valid for one year, they expire after that timeframe, and you will need to generate a new one to replace it. If you lose your access token, you will also need to generate a new one.

[Generate token](https://printify.com/app/account/api)

#### Step 4

Once generated, you can use that token as credentials for API requests in place of a username and password.

All requests must also specify a _User-Agent_ header. The value of this header should either be the type of client, such
as "Node.js" or "PHP," or the name of your application.

After authenticating, you can send HTTP requests to the API using any programming language
or tool capable of making HTTP requests. Use the appropriate base URL for your brand:

- **Printify**: `https://api.printify.com/v1/`
- **Printful Enterprise**: `https://enterprise.printful.com/api/pfy/public/v1/`

Here is an example:

`curl -X GET https://api.printify.com/v1/shops.json --header "Authorization: Bearer $PRINTIFY_API_TOKEN"`

#### Step 5

Once you’ve set the API up, go to your store by clicking on My Stores, then Add a new store. You should see Shopify, Etsy, WooCommerce, and the new option, API.

Click connect to connect your store to Printify via the API.

## OAuth 2.0

Using OAuth 2.0, you will be able to offer your application to the growing community of Printify Merchants.

On this page:

- [Prerequisites](https://developers.printify.com/#prerequisites)
- [Connecting your app to Printify](https://developers.printify.com/#connecting-your-app-to-printify)
  - [Getting grant codes](https://developers.printify.com/#getting-grant-codes)
  - [Getting tokens](https://developers.printify.com/#getting-tokens)
  - [Refreshing access tokens](https://developers.printify.com/#refreshing-access-tokens)
  - [Using access tokens](https://developers.printify.com/#using-access-tokens)
- [Endpoints](https://developers.printify.com/#authentication-endpoints)

### Prerequisites

1. Authentication for your integration starts with [registering your app.](https://printify.typeform.com/to/L8KXNYke) This
link takes you to an application form where you will answer some questions about your business, expected integration
timeline, and your applications' functionality. If your application is approved, you will receive instructions via
email for how to receive your app ID and how to set the required
[access scopes](https://developers.printify.com/#access-scopes) your application will need.
2. You'll use the app ID to initiate the OAuth handshake between Printify and your integration.

**Note:** Reviewing applications can take up to 1 week.

[Register your app](https://printify.typeform.com/to/L8KXNYke)

### Connecting your app to Printify

There are 4 steps to connecting your integration to a Merchant's Printify account using OAuth:

1. The Printify merchant will be presented with a screen that allows them to
[grant access to your integration](https://developers.printify.com/#getting-grant-codes).
2. After the Merchant grants access, they'll be returned to your app, with a code appended to the URL. Use that code and
your app ID to get an
[access\_token and refresh\_token.](https://developers.printify.com/#getting-tokens)
3. Use that access\_token to
[authenticate any API calls](https://developers.printify.com/#using-access-tokens) that you make for that Printify account.
4. Once that access\_token expires, use the refresh\_token from Step 2 to
[generate a new access\_token.](https://developers.printify.com/#refreshing-access-tokens)

### Getting grant codes

Initiating OAuth access is the first step for having merchants grant your application access to their Printify account. In order to
initiate OAuth connection for your App, you'll first need to send a Printify merchant to an authorization page, where that
merchant will need to grant access to your app. When your app sends a merchant to that authorization page, you'll use
the query parameters detailed below to identify your app.

Merchants must be signed into Printify to grant access, so any user that is not logged into Printify will be directed to
a login screen before being directed back to the authorization page. The authorization screen will show the details of
your app.

Depending on whether or not the merchant grants access, they will be redirected to the accept\_url or decline\_url that you specified, if access was granted, a code query
parameter is appended to the URL and you'll use that code to get an access token from Printify.

#### URL fields

|     |     |
| --- | --- |
| app\_id<br> REQUIRED | `app_id=x`<br> The app ID provided to you after registering your app. |
| accept\_url<br> REQUIRED | `accept_url=x`<br> The URL that you want the visitor redirected to after granting access to your app. A code that can be used to exchange for tokens will be appended to the end of the URL. |
| decline\_url<br> REQUIRED | `decline_url=x`<br> The URL that you want the visitor redirected to after denying access to your app. |
| state<br> RECOMMENDEDOPTIONAL | `state=123`<br> Persistent variable during connection flow. |

|     |     |
| --- | --- |
| ⚠ | For security reasons, the accept and decline URL must use https in production. When testing using localhost, http can be used. Also, you must use a domain, as IP addresses are not supported. |

### Getting tokens

Use the grant code you get after a user authorizes your app to exchange for an access token and refresh token. The access token will be
used to authenticate requests that your app makes. When you get the Access tokens, you also get expiration time
for the token. When token expires you have to use Refresh token to get a new Access token.

#### Request parameters

|     |     |
| --- | --- |
| app\_id<br> REQUIRED | `app_id=x`<br> The app ID provided to you after registering your app. |
| code<br> REQUIRED | `code=y`<br> The code parameter returned to your accept\_url when the user authorized your app, it is returned by the GET /app/oauth/accept endpoint and passed back to the consumer app. |

|     |     |
| --- | --- |
| ⚠ | Printify access tokens will fluctuate in size as we change the information that is encoded in the tokens. We recommend allowing for tokens to be up to 3,000 characters to account for any changes we may make. |

### Refreshing access tokens

Use a previously obtained refresh token to generate a new access token. Access tokens expire after 6 hours, so if you
need offline access to data in Printify, you'll need to store the refresh token you get when initiating your OAuth
integration, and use that to generate a new access token once the initial access token expires.

#### Request parameters

|     |     |
| --- | --- |
| app\_id<br> REQUIRED | `app_id=x`<br> The app ID provided to you after registering your app. |
| refresh\_token<br> REQUIRED | `refresh_token=x`<br> The refresh token returned by POST /app/oauth/tokens in the previous step. |

### Using access tokens

OAuth 2.0 access tokens are provided as a bearer token, in the Authorization http header.

The header format is: `Authorization: Bearer {token}`

### Endpoints

#### Get grant code

This request is made to the base URL `https://printify.com/`.

|     |     |
| --- | --- |
| GET | /app/authorize?{URL\_fields} |
| **Authorization request**<br>**URL fields**`<br>    app_id=x<br>    &accept_url=https://example.com<br>    &decline_url=https://example.com<br>    &state=123<br>` |
| **Possible outcomes**<br>**If access is granted, a URL redirect will follow with a grant code appended to the url**`<br>    https://www.example.com/?code=aabbccxxeeaabbccxxeeaabbccxxee<br>`**If there are any problems with the authorization, error parameters will be received instead of the code**`<br>    https://www.example.com/?error=error_code<br>    &error_description=Human%20readable%20description%20of%20the%20error<br>` |

### Convert grant code to tokens

After authenticating, use the appropriate base URL for your brand:

- **Printify**: `https://api.printify.com/v1/`
- **Printful Enterprise**: `https://enterprise.printful.com/api/pfy/public/v1/`

|     |     |
| --- | --- |
| POST | /app/oauth/tokens |
| **Convert grant code to tokens**<br>**Request parameters**`<br>    app_id=x<br>    &code=y<br>` |
| **Possible responses**<br>**If successful, a JSON response with the tokens will be received** [View Response](https://developers.printify.com/#)`{<br>     "access_token": "...",<br>     "refresh_token": "...",<br>     "expire_at": "2020-10-14 11:26:10+00:00"<br>}`<br>**If there are any problems with the request, a 400 response will be received with an error message** [View Response](https://developers.printify.com/#)`{<br>     "error": "error_code",<br>     "error_description": "A human readable error message"<br>}` |

### Refresh access token

|     |     |
| --- | --- |
| POST | /app/oauth/tokens/refresh |
| **Refresh access token**<br>**Request parameters**`<br>    app_id=x<br>    &refresh_token={from-the-get-tokens-request}<br>` |
| **Possible responses**<br>**If successful, a JSON response with the tokens will be received** [View Response](https://developers.printify.com/#)`{<br>     "access_token": "...",<br>     "refresh_token": "...",<br>     "expire_at": "2020-10-14 11:26:10+00:00"<br>}`<br>**If there are any problems with the request, a 400 response will be received with an error message** [View Response](https://developers.printify.com/#)`{<br>     "error": "error_code",<br>     "error_description": "A human readable error message"<br>}` |

## Access scopes

Scopes are permissions that identify the scope of access your application requests from the Printify Merchant Account.
Below you can see the names of access scopes that exist in Printify and their description.

| Access Scope | Notes |
| --- | --- |
| `shops.read` | Access shops in a Merchant's account |
| `catalog.read` | See Products and Print Providers from the Printify Product Catalog |
| `products.read` | See products created in a Merchant's shop |
| `products.write` | Create products in a Merchant's shop |
| `orders.read` | See orders created in a Merchant shop |
| `orders.write` | Create orders in a Merchant's shop |
| `webhooks.read` | Read installed webhooks |
| `webhooks.write` | Install, update and delete Webhooks |
| `uploads.read` | See uploaded files in a Merchant's account |
| `uploads.write` | Upload image files and archive them |
| `print_providers.read` | See available print providers |

# V1 API Reference

The Printify API is organized around
[REST](https://en.wikipedia.org/wiki/Representational_State_Transfer).

Our API has predictable resource-oriented URLs, accepts
[form-encoded](https://en.wikipedia.org/wiki/POST_(HTTP)#Use_for_submitting_web_forms) request bodies, returns
[JSON-encoded](http://www.json.org/) responses, and uses standard HTTP
[response codes](https://tools.ietf.org/html/rfc7231#section-6.1), authentication, and verbs.

[Download Postman Collection](https://developers.printify.com/postman/printify_postman_collection.json)

## API basics

- All requests are done via HTTPs. Requests via insecure HTTP are not supported.
- Printify API works with UTF-8 encoded data. Please make sure everything you send over in API calls also uses UTF-8.
- All data received from API and submitted to API is JSON, so the content type should be:
`application/json;charset=utf-8`
- Date/time values returned by Printify API are in UTC unless stated otherwise.
- The base URL for all endpoints varies by brand:

  - **Printify**: `https://api.printify.com/v1/`
  - **Printful Enterprise**: `https://enterprise.printful.com/api/pfy/public/v1/`
- `{variable}` in the URLs means you should substitute it with the proper variable value.
- The API currently does not support CORS, and requests from a frontend application will not be processed for
security reasons. You will need to set up a server-side application to access the API and ensure
secure storing of the API token.

## API pagination

Besides the `data` property returned in response, there are also other properties that are helpful for paginating over the resources.

|     |     |
| --- | --- |
| first\_page\_url | `"first_page_url": "/?page=1"`<br> URL for the first page of results - helpful in rewinding to the beginning of batch processing. |
| prev\_page\_url | `"prev_page_url": "/?page=2"`<br> URL for the previous page of results - helpful in going back or iterating from the last resource. |
| next\_page\_url | `"next_page_url": "/?page=4"`<br> URL for next page of results - helpful in iterating over results without doing page calculations. |
| last\_page\_url | `"last_page_url": "/?page=5"`<br> URL for the last page of results - helpful in jumping to the end of results. |
| current\_page | `"current_page": 3`<br> Current page of results. |
| last\_page | `"last_page": 5`<br> Last page of results. |
| total | `"total": 49`<br> The total number of results. |
| per\_page | `"per_page": 10`<br> The number of items retrieved in response. |
| from | `"from": 21`<br> The ordinal number of first item in response. |
| to | `"to": 30`<br> The ordinal number of last item in response. |

## Shops

All product creation and order submission in a Printify Merchant's account happens through a shop. Merchant's can have
multiple shops in one Printify account. Each of these shops can be connected to different sales channels and each has
independent products, orders, and analytics.

On this page:

- [What you can do with the shops resource](https://developers.printify.com/#what-you-can-do-with-the-shops-resource)
- [Shop properties](https://developers.printify.com/#shop-properties)
- [Endpoints](https://developers.printify.com/#shops-endpoints)

### What you can do with the shops resource

The shops resource serves one purpose, it allows you to view the list of existing shops in a Printify account.

- [GET /v1/shops.json](https://developers.printify.com/#retrieve-a-list-of-existing-shops)

Retrieve a list of existing shops in a Printify account
- [DELETE /v1/shops/{shop\_id}/connection.json](https://developers.printify.com/#disconnect-a-shop)

Disconnect a shop from a Printify account

### Shop properties

|     |     |
| --- | --- |
| id<br> READ-ONLY | `"id": 12345`<br> A unique int identifier for the shop. Each id is unique across the Printify system. |
| title<br> READ-ONLY | `"title": "Shop's title"`<br> The name of the shop. |
| sales\_channel<br> READ-ONLY | `"sales_channel": "Sales channel name"`<br> The name of the associated sales channel. If none are connected it defaults to "disconnected". |

### Endpoints

### Retrieve list of shops in a Printify account

|     |     |
| --- | --- |
| GET | /v1/shops.json |
| **Retrieve a list of shops in a Printify account**<br>`GET /v1/shops.json`<br>[View Response](https://developers.printify.com/#)`[<br>    {<br>      "id": 5432,<br>      "title": "My new store",<br>      "sales_channel": "My Sales Channel"<br>    },<br>    {<br>      "id": 9876,<br>      "title": "My other new store",<br>      "sales_channel": "disconnected"<br>    }<br>]` |

#### Disconnect a shop

|     |     |
| --- | --- |
| ⚠ | This endpoint requires a `{shop_id}` parameter. See [Retrieving Shop ID](https://developers.printify.com/#retrieving-shop-id) for instructions on how to obtain your shop ID. |

|     |     |
| --- | --- |
| DELETE | /v1/shops/{shop\_id}/connection.json |
| **Disconnect a shop**<br>`DELETE /v1/shops/{shop_id}/connection.json`<br>[View Response](https://developers.printify.com/#)`{}` |

## Catalog

Through the Catalog resource you can see all of the products, product variants, variant options and print providers
available in the Printify catalog.

Products in the Printify catalog are referred to as blueprints (only after user artwork has been added, are they referred to as products).

Every blueprint in the printify catalog has multiple Print Providers that offer that blueprint. In addition to general
differences between Print Providers including location and print technology employed, each Print Provider also offers
different colors, sizes, print areas and prices.

Each Print Provider's blueprint has specific size and color combinations known as variants. Variants also contain
information on a products available print areas and sizes.

On this page:

- [What you can do with the catalog resource](https://developers.printify.com/#what-you-can-do-with-the-catalog-resource)
- [Blueprint properties](https://developers.printify.com/#blueprint-properties)
  - [Size guide properties](https://developers.printify.com/#catalog-size-guide-properties)
  - [Print provider properties](https://developers.printify.com/#print-provider-properties)
  - [Variant properties](https://developers.printify.com/#catalog-variant-properties)
  - [Placeholder properties](https://developers.printify.com/#catalog-placeholder-properties)
  - [Shipping properties](https://developers.printify.com/#catalog-shipping-properties)
  - [Profile properties](https://developers.printify.com/#profile-properties)
- [Endpoints](https://developers.printify.com/#catalog-endpoints)
- [Structure](https://developers.printify.com/#catalog-structure)

### What you can do with the catalog resource

The Printify Public API lets you do the following with the Catalog resource:

- [GET /v1/catalog/blueprints.json](https://developers.printify.com/#retrieve-a-list-of-available-blueprints)

Retrieve a list of all available blueprints
- [GET /v1/catalog/blueprints/{blueprint\_id}.json](https://developers.printify.com/#retrieve-a-specific-blueprint)

Retrieve a specific blueprint
- [GET /v1/catalog/blueprints/{blueprint\_id}/size\_guide.json](https://developers.printify.com/#retrieve-a-blueprints-size-guide)

Retrieve a blueprint's size guide
- [GET /v1/catalog/blueprints/{blueprint\_id}/print\_providers.json](https://developers.printify.com/#retrieve-a-list-of-print-providers)

Retrieve a list of all print providers that fulfill orders for a specific blueprint
- [GET /v1/catalog/blueprints/{blueprint\_id}/print\_providers/{print\_provider\_id}/variants.json](https://developers.printify.com/#retrieve-a-list-of-variants)

Retrieve a list of all variants of a blueprint from a specific print provider
- [GET /v1/catalog/blueprints/{blueprint\_id}/print\_providers/{print\_provider\_id}/shipping.json](https://developers.printify.com/#retrieve-shipping-information)

Retrieve the shipping information for all variants of a blueprint from a specific print provider
- [GET /v1/catalog/print\_providers.json](https://developers.printify.com/#retrieve-a-list-of-available-print-providers)

Retrieve a list of all available print-providers
- [GET /v1/catalog/print\_providers/{print\_provider\_id}.json](https://developers.printify.com/#retrieve-a-specific-print-provider)

Retrieve a specific print-provider and a list of associated blueprint offerings

### Blueprint properties

|     |     |
| --- | --- |
| id<br> READ-ONLY | `"id": 5`<br> A unique int identifier for the blueprint. Each id is unique across the Printify system. |
| title<br> READ-ONLY | `"title": "Blueprint's title"`<br> The name of the blueprint. |
| brand<br> READ-ONLY | `"brand": "Blueprint's brand"`<br> The brand of the blueprint (i.e. the name of the blank product's manufacturer). |
| model<br> READ-ONLY | `"model": "Blueprint's brand model"`<br> The specific model of the blueprint's brand (i.e. the unique identifier of the blank product's model or style). |
| images<br> READ-ONLY | `"images": [<br>      "https://images.example.com/869549a1a0894a4692371b1f9928e14a.png",<br>      "https://images.example.com/878331a2b0876c9801746d2e2454f14a.png"<br>]`<br> Links to the title image wrappers displayed on the catalog. |
| tags<br> READ-ONLY | `"tags": [<br>      "Early Access"<br>]`<br> List of tags for the blueprint. Only returned by [Retrieve a specific blueprint](https://developers.printify.com/#retrieve-a-specific-blueprint); omitted from the blueprints list response. |
| features<br> READ-ONLY | `"features": [<br>    {<br>        "name": "With side seams",<br>        "description": "Located along the sides, they help hold the garment's shape longer and give it structural support",<br>        "image": "https://images.printify.com/59e0e9dfb8e7e30b9f57668b/icons_v4_outlined_33_with_side_seams.svg"<br>    }<br>]`<br> List of key features for the blueprint. Any of `name`, `description`, or `image` may be `null`. Only returned by [Retrieve a specific blueprint](https://developers.printify.com/#retrieve-a-specific-blueprint); omitted from the blueprints list response. |
| care\_instructions<br> READ-ONLY | `"care_instructions": [<br>      "Machine wash: cold (max 30C or 90F)",<br>      "Non-chlorine: bleach as needed"<br>]`<br> Care and washing instructions for the blueprint. Only returned by [Retrieve a specific blueprint](https://developers.printify.com/#retrieve-a-specific-blueprint); omitted from the blueprints list response. |

### Size guide properties

|     |     |
| --- | --- |
| sizes<br> READ-ONLY | `"sizes": [<br>      "S",<br>      "M",<br>      "L"<br>]`<br> Sizes the blueprint's size guide has measurements for, filtered down to only the sizes that are actually available for the blueprint. Empty when the blueprint has no size guide. |
| types<br> READ-ONLY | `"types": [<br>    {<br>        "name": "Width",<br>        "units": "in",<br>        "ranges": [<br>            {<br>                "from": "18",<br>                "to": "20"<br>            },<br>            {<br>                "from": "20",<br>                "to": "22"<br>            }<br>        ]<br>    }<br>]`<br> Measurement types for the size guide (e.g. `Width`, `Length`). Each type's `ranges` array has one entry per size in `sizes`, in the same order. A range's `from`/`to` may be `null` or an empty string when that bound isn't defined for that size. Empty when the blueprint has no size guide. |

### Print provider properties

|     |     |
| --- | --- |
| id<br> READ-ONLY | `"id": 3`<br> A unique int identifier for the print provider. Each id is unique across the Printify system. |
| title<br> READ-ONLY | `"title": "Print provider's title"`<br> The name of the print provider. |
| location<br> READ-ONLY | `"location": {<br>      "address1": "89 Weirfield St",<br>      "address2": "",<br>      "city": "Brooklyn",<br>      "country": "US",<br>      "region": "NY",<br>      "zip": "11221-5120"<br>}`<br> The return address of the print provider. |

### Variant properties

|     |     |
| --- | --- |
| id<br> READ-ONLY | `"id": 17390`<br> A unique int identifier for the blueprint variant. Each id is unique across the Printify system. |
| title<br> READ-ONLY | `"title": "Variant's title"`<br> The name of the variant. |
| options<br> READ-ONLY | `"options": {<br>    "color": "Heather Grey",<br>    "size": "XS"<br>}`<br> Options are read only values and describes blueprint variant options. There can be up to 3 options for a blueprint. |
| placeholders<br> READ-ONLY | `"placeholders": [<br>    {<br>        "position": "back",<br>        "decoration_method": "dtf",<br>        "height": 3995,<br>        "width": 3153<br>    },<br>    {<br>        "position": "front",<br>        "decoration_method": "dtf",<br>        "height": 3995,<br>        "width": 3153<br>    }<br>]`<br> Placeholders describe the available printable areas for a blueprint.<br> See [placeholder properties](https://developers.printify.com/#catalog-placeholder-properties) for reference.<br> Each position is associated with a specific decoration method. By selecting a position for your images,<br> you also select the decoration method used for printing. For example, a blueprint may provide multiple<br> front positions, such as `large_center_embroidery` for embroidery or `front_dtf`<br> for the DTF decoration method. |
| decoration\_methods<br> READ-ONLY | `"decoration_methods": [<br>    "dtg",<br>    "embroidery"<br>]`<br> List of decoration methods available for a blueprint variant and specific to the selected print provider.<br> To retrieve available decoration methods for a blueprint variant, use the<br> [Retrieve a list of variants of a blueprint from a specific print provider](https://developers.printify.com/#retrieve-a-list-of-variants) endpoint. |

### Placeholder properties

|     |     |
| --- | --- |
| position<br> READ-ONLY | `"position": "front"`<br> Position states the available printable areas for a blueprint fulfilled by a specific print provider. |
| decoration\_method<br> READ-ONLY | `"decoration_method": "dtf"`<br> Decoration method associated with the placeholder. |
| height<br> READ-ONLY | `"height": 3995`<br> Integer value for printable area height in pixels. |
| width<br> READ-ONLY | `"width": 3153`<br> Integer value for printable area width in pixels. |

### Shipping properties

|     |     |
| --- | --- |
| handling\_time<br> READ-ONLY | `"handling_time": {<br>    "value":10,<br>    "unit": "day"<br>}`<br> The standard shipping timeframe for a blueprint from a specific print provider. |
| profiles<br> READ-ONLY | `"profiles": [<br>    {<br>        "variant_ids": [1,2],<br>        "first_item": {<br>             "currency": "USD",<br>             "cost": 1000<br>        },<br>        "additional_items": {<br>             "currency": "USD",<br>             "cost": 1000<br>        },<br>        "countries":["US"]<br>    },<br>    {<br>        "variant_ids": [1,2],<br>        "first_item": {<br>             "currency": "USD",<br>             "cost": 1000<br>        },<br>        "additional_items": {<br>             "currency": "USD",<br>             "cost": 1000<br>        },<br>        "countries":["REST_OF_THE_WORLD"]<br>    }<br>]`<br> The list of shipping locations and flat shipping costs for all variants of a blueprint from a specific print provider. See [profile properties](https://developers.printify.com/#profile-properties) for reference. |

### Profile properties

|     |     |
| --- | --- |
| variant\_ids<br> READ-ONLY | `"variant_ids": [<br>    1,2,3,4,5,6,7<br>]`<br> Lists the ids of all blueprint variants the specific profile is associated to in an array. |
| first\_item<br> READ-ONLY | `"first_item": {<br>    "currency": "USD",<br>    "cost": 1000<br>}`<br> The currency and flat cost of shipping for a line item if identified as the first item in an order. |
| additional\_items<br> READ-ONLY | `"additional_items": {<br>    "currency": "USD",<br>    "cost": 1000<br>}`<br> The currency and flat cost of shipping for all other line items of the specific blueprint and print provider in the same order. |
| countries<br> READ-ONLY | `"countries": [<br>    "US"<br>]`<br> Lists the countries or delivery locations the shipping profile applies to. |

### Print details properties

|     |     |
| --- | --- |
| print\_on\_side<br> OPTIONAL | `"print_on_side": "regular"`<br> States the type of side print. possible values are "regular" for extending print area to the sides of canvas and "mirror" to keep original print area and mirror it to the sides. |
| separator\_type<br> OPTIONAL | `"separator_type": "Numbers"`<br> Required with "separator\_color" and specific to clock type blueprints, States the type clock separator. Possible string values are "Numbers" numeric separators, "Lines" for single bar separators, and "None" to specify that no separators be used. |
| separator\_color<br> OPTIONAL | `"separator_color": "#f100ff"`<br> Required with "separator\_type" and specific to clock type blueprints, States the type clock separator. Value must be a valid string hexadecimal color code. |

### Endpoints

#### Retrieve a list of available blueprints

|     |     |
| --- | --- |
| GET | /v1/catalog/blueprints.json |
| **Retrieve a list of available blueprints**<br>`GET /v1/catalog/blueprints.json`<br>[View Response](https://developers.printify.com/#)`[<br>    {<br>        "id": 3,<br>        "title": "Kids Regular Fit Tee",<br>        "description": "Description goes here",<br>        "brand": "Delta",<br>        "model": "11736",<br>        "images": [<br>            "https://images.printify.com/5853fe7dce46f30f8327f5cd",<br>            "https://images.printify.com/5c487ee2a342bc9b8b2fc4d2"<br>        ]<br>    },<br>    {<br>        "id": 5,<br>        "title": "Men's Cotton Crew Tee",<br>        "description": "Description goes here",<br>        "brand": "Next Level",<br>        "model": "3600",<br>        "images": [<br>            "https://images.printify.com/5a2ffc81b8e7e3656268fb44",<br>            "https://images.printify.com/5cdc0126b97b6a00091b58f7"<br>        ]<br>    },<br>    {<br>        "id": 6,<br>        "title": "Unisex Heavy Cotton Tee",<br>        "description": "Description goes here",<br>        "brand": "Gildan",<br>        "model": "5000",<br>        "images": [<br>            "https://images.printify.com/5a2fd7d9b8e7e36658795dc0",<br>            "https://images.printify.com/5c595436a342bc1670049902",<br>            "https://images.printify.com/5c595427a342bc166b6d3002",<br>            "https://images.printify.com/5a2fd022b8e7e3666c70623a"<br>        ]<br>    },<br>    {<br>        "id": 9,<br>        "title": "Women's Favorite Tee",<br>        "description": "Description goes here",<br>        "brand": "Bella+Canvas",<br>        "model": "6004",<br>        "images": [<br>            "https://images.printify.com/5a2ffeeab8e7e364d660836f",<br>            "https://images.printify.com/59e362cab8e7e30a5b0a55bd",<br>            "https://images.printify.com/59e362d2b8e7e30b9f576691",<br>            "https://images.printify.com/59e362ddb8e7e3174f3196ee",<br>            "https://images.printify.com/59e362eab8e7e3593e2ac98d"<br>        ]<br>    },<br>    {<br>        "id": 10,<br>        "title": "Women's Flowy Racerback Tank",<br>        "description": "Description goes here",<br>        "brand": "Bella+Canvas",<br>        "model": "8800",<br>        "images": [<br>            "https://images.printify.com/5a27eb68b8e7e364d6608322",<br>            "https://images.printify.com/5c485236a342bc521c2a0beb",<br>            "https://images.printify.com/5c485217a342bc686053da46",<br>            "https://images.printify.com/5c485225a342bc52fe5fee83"<br>        ]<br>    },<br>    {<br>        "id": 11,<br>        "title": "Women's Jersey Short Sleeve Deep V-Neck Tee",<br>        "description": "Description goes here",<br>        "brand": "Bella+Canvas",<br>        "model": "6035",<br>        "images": [<br>            "https://images.printify.com/5a27f20fb8e7e316f403a3b1",<br>            "https://images.printify.com/5c472ff0a342bcad97372d72",<br>            "https://images.printify.com/5c472ff8a342bcad9964d115"<br>        ]<br>    },<br>    {<br>        "id": 12,<br>        "title": "Unisex Jersey Short Sleeve Tee",<br>        "description": "Description goes here",<br>        "brand": "Bella+Canvas",<br>        "model": "3001",<br>        "images": [<br>            "https://images.printify.com/5a2ff5b0b8e7e36669068406",<br>            "https://images.printify.com/59e35414b8e7e30aa625995c",<br>            "https://images.printify.com/5cd579548c3769000f274cac",<br>            "https://images.printify.com/5cd579558c37690008453286",<br>            "https://images.printify.com/59e3541bb8e7e30a60795f9c",<br>            "https://images.printify.com/59e35428b8e7e30a1a4de812",<br>            "https://images.printify.com/59e3552db8e7e3174714887a",<br>            "https://images.printify.com/5a8beec5b8e7e304614eb59c"<br>        ]<br>    }<br>]` |

#### Retrieve a specific blueprint

|     |     |
| --- | --- |
| GET | /v1/catalog/blueprints/{blueprint\_id}.json |
| **Retrieve a specific blueprint**<br>`GET /v1/catalog/blueprints/{blueprint_id}.json`<br>[View Response](https://developers.printify.com/#)`{<br>     "id": 3,<br>     "title": "Kids Regular Fit Tee",<br>     "description": "Description goes here",<br>     "brand": "Delta",<br>     "model": "11736",<br>     "images": [<br>        "https://images.printify.com/5853fe7dce46f30f8327f5cd",<br>        "https://images.printify.com/5c487ee2a342bc9b8b2fc4d2"<br>     ],<br>     "tags": [<br>        "Early Access"<br>     ],<br>     "features": [<br>        {<br>            "name": "With side seams",<br>            "description": "Located along the sides, they help hold the garment's shape longer and give it structural support",<br>            "image": "https://images.printify.com/59e0e9dfb8e7e30b9f57668b/icons_v4_outlined_33_with_side_seams.svg"<br>        }<br>     ],<br>     "care_instructions": [<br>        "Machine wash: cold (max 30C or 90F)",<br>        "Non-chlorine: bleach as needed"<br>     ]<br>}` |

#### Retrieve a blueprint's size guide

|     |     |
| --- | --- |
| GET | /v1/catalog/blueprints/{blueprint\_id}/size\_guide.json |
| **Retrieve a blueprint's size guide**<br>`GET /v1/catalog/blueprints/{blueprint_id}/size_guide.json`<br> Sizes are filtered down to only those actually available for the blueprint. Returns `{"sizes": [], "types": []}` when the blueprint has no size guide defined.<br>[View Response](https://developers.printify.com/#)`{<br>    "sizes": [<br>        "S",<br>        "M",<br>        "L"<br>    ],<br>    "types": [<br>        {<br>            "name": "Width",<br>            "units": "in",<br>            "ranges": [<br>                {<br>                    "from": "18",<br>                    "to": "20"<br>                },<br>                {<br>                    "from": "20",<br>                    "to": "22"<br>                },<br>                {<br>                    "from": "22",<br>                    "to": "24"<br>                }<br>            ]<br>        }<br>    ]<br>}` |

#### Retrieve a list of all print providers that fulfill orders for a specific blueprint

|     |     |
| --- | --- |
| GET | /v1/catalog/blueprints/{blueprint\_id}/print\_providers.json |
| **Retrieve a list of all print providers that fulfill orders for a specific blueprint**<br>`GET /v1/catalog/blueprints/{blueprint_id}/print_providers.json`<br>[View Response](https://developers.printify.com/#)`[<br>    {<br>        "id": 3,<br>        "title": "DJ",<br>        "decoration_methods": [<br>              "dtg",<br>              "embroidery"<br>        ]<br>    },<br>    {<br>        "id": 8,<br>        "title": "Fifth Sun",<br>        "decoration_methods": [<br>              "dtg"<br>        ]<br>    },<br>    {<br>        "id": 16,<br>        "title": "MyLocker",<br>        "decoration_methods": [<br>              "dtg"<br>        ]<br>    },<br>    {<br>        "id": 24,<br>        "title": "Inklocker",<br>        "decoration_methods": [<br>            "dtf",<br>            "dtg",<br>            "embroidery"<br>        ]<br>    }<br>]` |

#### Retrieve a list of variants of a blueprint from a specific print provider

|     |     |
| --- | --- |
| GET | /v1/catalog/blueprints/{blueprint\_id}/print\_providers/{print\_provider\_id}/variants.json |
| show-out-of-stock<br> OPTIONAL | Depending on the value, it shows all variants or only those not out of stock. Without passing this query param, the list will contain only those variants in stock.<br> <br>0 - show only variants that are in stock.<br> <br>1 - also show variants out of stock (all variants). |
| **Retrieve a list of variants of a blueprint from a specific print provider**<br>`GET /v1/catalog/blueprints/{blueprint_id}/print_providers/{print_provider_id}/variants.json`<br>[View Response](https://developers.printify.com/#)`{<br>    "id": 3,<br>    "title": "DJ",<br>    "variants": [<br>        {<br>            "id": 17390,<br>            "title": "Heather Grey / XS",<br>            "options": {<br>                "color": "Heather Grey",<br>                "size": "XS"<br>            },<br>            "placeholders": [<br>                {<br>                    "position": "back",<br>                    "decoration_method": "dtf",<br>                    "height": 3995,<br>                    "width": 3153<br>                },<br>                {<br>                    "position": "front",<br>                    "decoration_method": "embroidery",<br>                    "height": 3995,<br>                    "width": 3153<br>                }<br>            ],<br>            "decoration_methods": [<br>                "dtf",<br>                "embroidery"<br>            ]<br>        },<br>        {<br>            "id": 17426,<br>            "title": "Solid Black / XS",<br>            "options": {<br>                "color": "Solid Black",<br>                "size": "XS"<br>            },<br>            "placeholders": [<br>                {<br>                    "position": "back",<br>                    "decoration_method": "dtf",<br>                    "height": 3995,<br>                    "width": 3153<br>                },<br>                {<br>                    "position": "front",<br>                    "decoration_method": "embroidery",<br>                    "height": 3995,<br>                    "width": 3153<br>                }<br>            ],<br>            "decoration_methods": [<br>                "dtf",<br>                "embroidery"<br>            ]<br>        },<br>        {<br>            "id": 17435,<br>            "title": "Solid Scarlet / XS",<br>            "options": {<br>                "color": "Solid Scarlet",<br>                "size": "XS"<br>            },<br>            "placeholders": [<br>                {<br>                    "position": "back",<br>                    "decoration_method": "dtf",<br>                    "height": 3995,<br>                    "width": 3153<br>                },<br>                {<br>                    "position": "front",<br>                    "decoration_method": "embroidery",<br>                    "height": 3995,<br>                    "width": 3153<br>                }<br>            ],<br>            "decoration_methods": [<br>                "dtf",<br>                "embroidery"<br>            ]<br>        },<br>        {<br>            "id": 17444,<br>            "title": "Solid Cool Blue / XS",<br>            "options": {<br>                "color": "Solid Cool Blue",<br>                "size": "XS"<br>            },<br>            "placeholders": [<br>                {<br>                    "position": "back",<br>                    "decoration_method": "dtf",<br>                    "height": 3995,<br>                    "width": 3153<br>                },<br>                {<br>                    "position": "front",<br>                    "decoration_method": "embroidery",<br>                    "height": 3995,<br>                    "width": 3153<br>                }<br>            ],<br>            "decoration_methods": [<br>                "dtf",<br>                "embroidery"<br>            ]<br>        },<br>        {<br>            "id": 17453,<br>            "title": "Solid Cream / XS",<br>            "options": {<br>                "color": "Solid Cream",<br>                "size": "XS"<br>            },<br>            "placeholders": [<br>                {<br>                    "position": "back",<br>                    "decoration_method": "dtf",<br>                    "height": 3995,<br>                    "width": 3153<br>                },<br>                {<br>                    "position": "front",<br>                    "decoration_method": "embroidery",<br>                    "height": 3995,<br>                    "width": 3153<br>                }<br>            ],<br>            "decoration_methods": [<br>                "dtf",<br>                "embroidery"<br>            ]<br>        },<br>        {<br>            "id": 17462,<br>            "title": "Solid Dark Chocolate / XS",<br>            "options": {<br>                "color": "Solid Dark Chocolate",<br>                "size": "XS"<br>            },<br>            "placeholders": [<br>                {<br>                    "position": "back",<br>                    "decoration_method": "dtf",<br>                    "height": 3995,<br>                    "width": 3153<br>                },<br>                {<br>                    "position": "front",<br>                    "decoration_method": "embroidery",<br>                    "height": 3995,<br>                    "width": 3153<br>                }<br>            ],<br>            "decoration_methods": [<br>                "dtf",<br>                "embroidery"<br>            ]<br>        },<br>        {<br>            "id": 17480,<br>            "title": "Solid Heavy Metal / XS",<br>            "options": {<br>                "color": "Solid Heavy Metal",<br>                "size": "XS"<br>            },<br>            "placeholders": [<br>                {<br>                    "position": "back",<br>                    "decoration_method": "dtf",<br>                    "height": 3995,<br>                    "width": 3153<br>                },<br>                {<br>                    "position": "front",<br>                    "decoration_method": "embroidery",<br>                    "height": 3995,<br>                    "width": 3153<br>                }<br>            ],<br>            "decoration_methods": [<br>                "dtf",<br>                "embroidery"<br>            ]<br>        },<br>        {<br>            "id": 17489,<br>            "title": "Solid Indigo / XS",<br>            "options": {<br>                "color": "Solid Indigo",<br>                "size": "XS"<br>            },<br>            "placeholders": [<br>                {<br>                    "position": "back",<br>                    "decoration_method": "dtf",<br>                    "height": 3995,<br>                    "width": 3153<br>                },<br>                {<br>                    "position": "front",<br>                    "decoration_method": "embroidery",<br>                    "height": 3995,<br>                    "width": 3153<br>                }<br>            ],<br>            "decoration_methods": [<br>                "dtf",<br>                "embroidery"<br>            ]<br>        },<br>        {<br>            "id": 17516,<br>            "title": "Solid Light Blue / XS",<br>            "options": {<br>                "color": "Solid Light Blue",<br>                "size": "XS"<br>            },<br>            "placeholders": [<br>                {<br>                    "position": "back",<br>                    "decoration_method": "dtf",<br>                    "height": 3995,<br>                    "width": 3153<br>                },<br>                {<br>                    "position": "front",<br>                    "decoration_method": "embroidery",<br>                    "height": 3995,<br>                    "width": 3153<br>                }<br>            ],<br>            "decoration_methods": [<br>                "dtf",<br>                "embroidery"<br>            ]<br>        },<br>        {<br>            "id": 17552,<br>            "title": "Solid Maroon / XS",<br>            "options": {<br>                "color": "Solid Maroon",<br>                "size": "XS"<br>            },<br>            "placeholders": [<br>                {<br>                    "position": "back",<br>                    "decoration_method": "dtf",<br>                    "height": 3995,<br>                    "width": 3153<br>                },<br>                {<br>                    "position": "front",<br>                    "decoration_method": "embroidery",<br>                    "height": 3995,<br>                    "width": 3153<br>                }<br>            ],<br>            "decoration_methods": [<br>                "dtf",<br>                "embroidery"<br>            ]<br>        },<br>        {<br>            "id": 17588,<br>            "title": "Solid Red / XS",<br>            "options": {<br>                "color": "Solid Red",<br>                "size": "XS"<br>            },<br>            "placeholders": [<br>                {<br>                    "position": "back",<br>                    "decoration_method": "dtf",<br>                    "height": 3995,<br>                    "width": 3153<br>                },<br>                {<br>                    "position": "front",<br>                    "decoration_method": "embroidery",<br>                    "height": 3995,<br>                    "width": 3153<br>                }<br>            ],<br>            "decoration_methods": [<br>                "dtf",<br>                "embroidery"<br>            ]<br>        },<br>        {<br>            "id": 17597,<br>            "title": "Solid Royal / XS",<br>            "options": {<br>                "color": "Solid Royal",<br>                "size": "XS"<br>            },<br>            "placeholders": [<br>                {<br>                    "position": "back",<br>                    "decoration_method": "dtf",<br>                    "height": 3995,<br>                    "width": 3153<br>                },<br>                {<br>                    "position": "front",<br>                    "decoration_method": "embroidery",<br>                    "height": 3995,<br>                    "width": 3153<br>                }<br>            ],<br>            "decoration_methods": [<br>                "dtf",<br>                "embroidery"<br>            ]<br>        },<br>        {<br>            "id": 17606,<br>            "title": "Solid Sand / XS",<br>            "options": {<br>                "color": "Solid Sand",<br>                "size": "XS"<br>            },<br>            "placeholders": [<br>                {<br>                    "position": "back",<br>                    "decoration_method": "dtf",<br>                    "height": 3995,<br>                    "width": 3153<br>                },<br>                {<br>                    "position": "front",<br>                    "decoration_method": "embroidery",<br>                    "height": 3995,<br>                    "width": 3153<br>                }<br>            ],<br>            "decoration_methods": [<br>                "dtf",<br>                "embroidery"<br>            ]<br>        },<br>        {<br>            "id": 17642,<br>            "title": "Solid White / XS",<br>            "options": {<br>                "color": "Solid White",<br>                "size": "XS"<br>            },<br>            "placeholders": [<br>                {<br>                    "position": "back",<br>                    "decoration_method": "dtf",<br>                    "height": 3995,<br>                    "width": 3153<br>                },<br>                {<br>                    "position": "front",<br>                    "decoration_method": "embroidery",<br>                    "height": 3995,<br>                    "width": 3153<br>                }<br>            ],<br>            "decoration_methods": [<br>                "dtf",<br>                "embroidery"<br>            ]<br>        },<br>        {<br>            "id": 17391,<br>            "title": "Heather Grey / S",<br>            "options": {<br>                "color": "Heather Grey",<br>                "size": "S"<br>            },<br>            "placeholders": [<br>                {<br>                    "position": "back",<br>                    "decoration_method": "dtf",<br>                    "height": 4563,<br>                    "width": 3602<br>                },<br>                {<br>                    "position": "front",<br>                    "decoration_method": "embroidery",<br>                    "height": 4563,<br>                    "width": 3602<br>                }<br>            ],<br>            "decoration_methods": [<br>                "dtf",<br>                "embroidery"<br>            ]<br>        },<br>        {<br>            "id": 17427,<br>            "title": "Solid Black / S",<br>            "options": {<br>                "color": "Solid Black",<br>                "size": "S"<br>            },<br>            "placeholders": [<br>                {<br>                    "position": "back",<br>                    "decoration_method": "dtf",<br>                    "height": 4563,<br>                    "width": 3602<br>                },<br>                {<br>                    "position": "front",<br>                    "decoration_method": "embroidery",<br>                    "height": 4563,<br>                    "width": 3602<br>                }<br>            ],<br>            "decoration_methods": [<br>                "dtf",<br>                "embroidery"<br>            ]<br>        },<br>        {<br>            "id": 17436,<br>            "title": "Solid Scarlet / S",<br>            "options": {<br>                "color": "Solid Scarlet",<br>                "size": "S"<br>            },<br>            "placeholders": [<br>                {<br>                    "position": "back",<br>                    "decoration_method": "dtf",<br>                    "height": 4563,<br>                    "width": 3602<br>                },<br>                {<br>                    "position": "front",<br>                    "decoration_method": "embroidery",<br>                    "height": 4563,<br>                    "width": 3602<br>                }<br>            ],<br>            "decoration_methods": [<br>                "dtf",<br>                "embroidery"<br>            ]<br>        },<br>        {<br>            "id": 17445,<br>            "title": "Solid Cool Blue / S",<br>            "options": {<br>                "color": "Solid Cool Blue",<br>                "size": "S"<br>            },<br>            "placeholders": [<br>                {<br>                    "position": "back",<br>                    "decoration_method": "dtf",<br>                    "height": 4563,<br>                    "width": 3602<br>                },<br>                {<br>                    "position": "front",<br>                    "decoration_method": "embroidery",<br>                    "height": 4563,<br>                    "width": 3602<br>                }<br>            ],<br>            "decoration_methods": [<br>                "dtf",<br>                "embroidery"<br>            ]<br>        },<br>        {<br>            "id": 17454,<br>            "title": "Solid Cream / S",<br>            "options": {<br>                "color": "Solid Cream",<br>                "size": "S"<br>            },<br>            "placeholders": [<br>                {<br>                    "position": "back",<br>                    "decoration_method": "dtf",<br>                    "height": 4563,<br>                    "width": 3602<br>                },<br>                {<br>                    "position": "front",<br>                    "decoration_method": "embroidery",<br>                    "height": 4563,<br>                    "width": 3602<br>                }<br>            ],<br>            "decoration_methods": [<br>                "dtf",<br>                "embroidery"<br>            ]<br>        },<br>        {<br>            "id": 17463,<br>            "title": "Solid Dark Chocolate / S",<br>            "options": {<br>                "color": "Solid Dark Chocolate",<br>                "size": "S"<br>            },<br>            "placeholders": [<br>                {<br>                    "position": "back",<br>                    "decoration_method": "dtf",<br>                    "height": 4563,<br>                    "width": 3602<br>                },<br>                {<br>                    "position": "front",<br>                    "decoration_method": "embroidery",<br>                    "height": 4563,<br>                    "width": 3602<br>                }<br>            ],<br>            "decoration_methods": [<br>                "dtf",<br>                "embroidery"<br>            ]<br>        },<br>        {<br>            "id": 17481,<br>            "title": "Solid Heavy Metal / S",<br>            "options": {<br>                "color": "Solid Heavy Metal",<br>                "size": "S"<br>            },<br>            "placeholders": [<br>                {<br>                    "position": "back",<br>                    "decoration_method": "dtf",<br>                    "height": 4563,<br>                    "width": 3602<br>                },<br>                {<br>                    "position": "front",<br>                    "decoration_method": "embroidery",<br>                    "height": 4563,<br>                    "width": 3602<br>                }<br>            ],<br>            "decoration_methods": [<br>                "dtf",<br>                "embroidery"<br>            ]<br>        },<br>        {<br>            "id": 17490,<br>            "title": "Solid Indigo / S",<br>            "options": {<br>                "color": "Solid Indigo",<br>                "size": "S"<br>            },<br>            "placeholders": [<br>                {<br>                    "position": "back",<br>                    "decoration_method": "dtf",<br>                    "height": 4563,<br>                    "width": 3602<br>                },<br>                {<br>                    "position": "front",<br>                    "decoration_method": "embroidery",<br>                    "height": 4563,<br>                    "width": 3602<br>                }<br>            ],<br>            "decoration_methods": [<br>                "dtf",<br>                "embroidery"<br>            ]<br>        },<br>        {<br>            "id": 17517,<br>            "title": "Solid Light Blue / S",<br>            "options": {<br>                "color": "Solid Light Blue",<br>                "size": "S"<br>            },<br>            "placeholders": [<br>                {<br>                    "position": "back",<br>                    "decoration_method": "dtf",<br>                    "height": 4563,<br>                    "width": 3602<br>                },<br>                {<br>                    "position": "front",<br>                    "decoration_method": "embroidery",<br>                    "height": 4563,<br>                    "width": 3602<br>                }<br>            ],<br>            "decoration_methods": [<br>                "dtf",<br>                "embroidery"<br>            ]<br>        },<br>        {<br>            "id": 17553,<br>            "title": "Solid Maroon / S",<br>            "options": {<br>                "color": "Solid Maroon",<br>                "size": "S"<br>            },<br>            "placeholders": [<br>                {<br>                    "position": "back",<br>                    "decoration_method": "dtf",<br>                    "height": 4563,<br>                    "width": 3602<br>                },<br>                {<br>                    "position": "front",<br>                    "decoration_method": "embroidery",<br>                    "height": 4563,<br>                    "width": 3602<br>                }<br>            ],<br>            "decoration_methods": [<br>                "dtf",<br>                "embroidery"<br>            ]<br>        },<br>        {<br>            "id": 17589,<br>            "title": "Solid Red / S",<br>            "options": {<br>                "color": "Solid Red",<br>                "size": "S"<br>            },<br>            "placeholders": [<br>                {<br>                    "position": "back",<br>                    "decoration_method": "dtf",<br>                    "height": 4563,<br>                    "width": 3602<br>                },<br>                {<br>                    "position": "front",<br>                    "decoration_method": "embroidery",<br>                    "height": 4563,<br>                    "width": 3602<br>                }<br>            ],<br>            "decoration_methods": [<br>                "dtf",<br>                "embroidery"<br>            ]<br>        },<br>        {<br>            "id": 17598,<br>            "title": "Solid Royal / S",<br>            "options": {<br>                "color": "Solid Royal",<br>                "size": "S"<br>            },<br>            "placeholders": [<br>                {<br>                    "position": "back",<br>                    "decoration_method": "dtf",<br>                    "height": 4563,<br>                    "width": 3602<br>                },<br>                {<br>                    "position": "front",<br>                    "decoration_method": "embroidery",<br>                    "height": 4563,<br>                    "width": 3602<br>                }<br>            ],<br>            "decoration_methods": [<br>                "dtf",<br>                "embroidery"<br>            ]<br>        },<br>        {<br>            "id": 17607,<br>            "title": "Solid Sand / S",<br>            "options": {<br>                "color": "Solid Sand",<br>                "size": "S"<br>            },<br>            "placeholders": [<br>                {<br>                    "position": "back",<br>                    "decoration_method": "dtf",<br>                    "height": 4563,<br>                    "width": 3602<br>                },<br>                {<br>                    "position": "front",<br>                    "decoration_method": "embroidery",<br>                    "height": 4563,<br>                    "width": 3602<br>                }<br>            ],<br>            "decoration_methods": [<br>                "dtf",<br>                "embroidery"<br>            ]<br>        },<br>        {<br>            "id": 17643,<br>            "title": "Solid White / S",<br>            "options": {<br>                "color": "Solid White",<br>                "size": "S"<br>            },<br>            "placeholders": [<br>                {<br>                    "position": "back",<br>                    "decoration_method": "dtf",<br>                    "height": 4563,<br>                    "width": 3602<br>                },<br>                {<br>                    "position": "front",<br>                    "decoration_method": "embroidery",<br>                    "height": 4563,<br>                    "width": 3602<br>                }<br>            ],<br>            "decoration_methods": [<br>                "dtf",<br>                "embroidery"<br>            ]<br>        },<br>        {<br>            "id": 17392,<br>            "title": "Heather Grey / M",<br>            "options": {<br>                "color": "Heather Grey",<br>                "size": "M"<br>            },<br>            "placeholders": [<br>                {<br>                    "position": "back",<br>                    "decoration_method": "dtf",<br>                    "height": 5131,<br>                    "width": 4051<br>                },<br>                {<br>                    "position": "front",<br>                    "decoration_method": "embroidery",<br>                    "height": 5131,<br>                    "width": 4051<br>                }<br>            ],<br>            "decoration_methods": [<br>                "dtf",<br>                "embroidery"<br>            ]<br>        },<br>        {<br>            "id": 17428,<br>            "title": "Solid Black / M",<br>            "options": {<br>                "color": "Solid Black",<br>                "size": "M"<br>            },<br>            "placeholders": [<br>                {<br>                    "position": "back",<br>                    "decoration_method": "dtf",<br>                    "height": 5131,<br>                    "width": 4051<br>                },<br>                {<br>                    "position": "front",<br>                    "decoration_method": "embroidery",<br>                    "height": 5131,<br>                    "width": 4051<br>                }<br>            ],<br>            "decoration_methods": [<br>                "dtf",<br>                "embroidery"<br>            ]<br>        },<br>        {<br>            "id": 17437,<br>            "title": "Solid Scarlet / M",<br>            "options": {<br>                "color": "Solid Scarlet",<br>                "size": "M"<br>            },<br>            "placeholders": [<br>                {<br>                    "position": "back",<br>                    "decoration_method": "dtf",<br>                    "height": 5131,<br>                    "width": 4051<br>                },<br>                {<br>                    "position": "front",<br>                    "decoration_method": "embroidery",<br>                    "height": 5131,<br>                    "width": 4051<br>                }<br>            ],<br>            "decoration_methods": [<br>                "dtf",<br>                "embroidery"<br>            ]<br>        },<br>        {<br>            "id": 17446,<br>            "title": "Solid Cool Blue / M",<br>            "options": {<br>                "color": "Solid Cool Blue",<br>                "size": "M"<br>            },<br>            "placeholders": [<br>                {<br>                    "position": "back",<br>                    "decoration_method": "dtf",<br>                    "height": 5131,<br>                    "width": 4051<br>                },<br>                {<br>                    "position": "front",<br>                    "decoration_method": "embroidery",<br>                    "height": 5131,<br>                    "width": 4051<br>                }<br>            ],<br>            "decoration_methods": [<br>                "dtf",<br>                "embroidery"<br>            ]<br>        },<br>        {<br>            "id": 17455,<br>            "title": "Solid Cream / M",<br>            "options": {<br>                "color": "Solid Cream",<br>                "size": "M"<br>            },<br>            "placeholders": [<br>                {<br>                    "position": "back",<br>                    "decoration_method": "dtf",<br>                    "height": 5131,<br>                    "width": 4051<br>                },<br>                {<br>                    "position": "front",<br>                    "decoration_method": "embroidery",<br>                    "height": 5131,<br>                    "width": 4051<br>                }<br>            ],<br>            "decoration_methods": [<br>                "dtf",<br>                "embroidery"<br>            ]<br>        },<br>        {<br>            "id": 17464,<br>            "title": "Solid Dark Chocolate / M",<br>            "options": {<br>                "color": "Solid Dark Chocolate",<br>                "size": "M"<br>            },<br>            "placeholders": [<br>                {<br>                    "position": "back",<br>                    "decoration_method": "dtf",<br>                    "height": 5131,<br>                    "width": 4051<br>                },<br>                {<br>                    "position": "front",<br>                    "decoration_method": "embroidery",<br>                    "height": 5131,<br>                    "width": 4051<br>                }<br>            ],<br>            "decoration_methods": [<br>                "dtf",<br>                "embroidery"<br>            ]<br>        },<br>        {<br>            "id": 17482,<br>            "title": "Solid Heavy Metal / M",<br>            "options": {<br>                "color": "Solid Heavy Metal",<br>                "size": "M"<br>            },<br>            "placeholders": [<br>                {<br>                    "position": "back",<br>                    "decoration_method": "dtf",<br>                    "height": 5131,<br>                    "width": 4051<br>                },<br>                {<br>                    "position": "front",<br>                    "decoration_method": "embroidery",<br>                    "height": 5131,<br>                    "width": 4051<br>                }<br>            ],<br>            "decoration_methods": [<br>                "dtf",<br>                "embroidery"<br>            ]<br>        },<br>        {<br>            "id": 17491,<br>            "title": "Solid Indigo / M",<br>            "options": {<br>                "color": "Solid Indigo",<br>                "size": "M"<br>            },<br>            "placeholders": [<br>                {<br>                    "position": "back",<br>                    "decoration_method": "dtf",<br>                    "height": 5131,<br>                    "width": 4051<br>                },<br>                {<br>                    "position": "front",<br>                    "decoration_method": "embroidery",<br>                    "height": 5131,<br>                    "width": 4051<br>                }<br>            ],<br>            "decoration_methods": [<br>                "dtf",<br>                "embroidery"<br>            ]<br>        },<br>        {<br>            "id": 17518,<br>            "title": "Solid Light Blue / M",<br>            "options": {<br>                "color": "Solid Light Blue",<br>                "size": "M"<br>            },<br>            "placeholders": [<br>                {<br>                    "position": "back",<br>                    "decoration_method": "dtf",<br>                    "height": 5131,<br>                    "width": 4051<br>                },<br>                {<br>                    "position": "front",<br>                    "decoration_method": "embroidery",<br>                    "height": 5131,<br>                    "width": 4051<br>                }<br>            ],<br>            "decoration_methods": [<br>                "dtf",<br>                "embroidery"<br>            ]<br>        },<br>        {<br>            "id": 17554,<br>            "title": "Solid Maroon / M",<br>            "options": {<br>                "color": "Solid Maroon",<br>                "size": "M"<br>            },<br>            "placeholders": [<br>                {<br>                    "position": "back",<br>                    "decoration_method": "dtf",<br>                    "height": 5131,<br>                    "width": 4051<br>                },<br>                {<br>                    "position": "front",<br>                    "decoration_method": "embroidery",<br>                    "height": 5131,<br>                    "width": 4051<br>                }<br>            ],<br>            "decoration_methods": [<br>                "dtf",<br>                "embroidery"<br>            ]<br>        },<br>        {<br>            "id": 17590,<br>            "title": "Solid Red / M",<br>            "options": {<br>                "color": "Solid Red",<br>                "size": "M"<br>            },<br>            "placeholders": [<br>                {<br>                    "position": "back",<br>                    "decoration_method": "dtf",<br>                    "height": 5131,<br>                    "width": 4051<br>                },<br>                {<br>                    "position": "front",<br>                    "decoration_method": "embroidery",<br>                    "height": 5131,<br>                    "width": 4051<br>                }<br>            ],<br>            "decoration_methods": [<br>                "dtf",<br>                "embroidery"<br>            ]<br>        },<br>        {<br>            "id": 17599,<br>            "title": "Solid Royal / M",<br>            "options": {<br>                "color": "Solid Royal",<br>                "size": "M"<br>            },<br>            "placeholders": [<br>                {<br>                    "position": "back",<br>                    "decoration_method": "dtf",<br>                    "height": 5131,<br>                    "width": 4051<br>                },<br>                {<br>                    "position": "front",<br>                    "decoration_method": "embroidery",<br>                    "height": 5131,<br>                    "width": 4051<br>                }<br>            ],<br>            "decoration_methods": [<br>                "dtf",<br>                "embroidery"<br>            ]<br>        },<br>        {<br>            "id": 17608,<br>            "title": "Solid Sand / M",<br>            "options": {<br>                "color": "Solid Sand",<br>                "size": "M"<br>            },<br>            "placeholders": [<br>                {<br>                    "position": "back",<br>                    "decoration_method": "dtf",<br>                    "height": 5131,<br>                    "width": 4051<br>                },<br>                {<br>                    "position": "front",<br>                    "decoration_method": "embroidery",<br>                    "height": 5131,<br>                    "width": 4051<br>                }<br>            ],<br>            "decoration_methods": [<br>                "dtf",<br>                "embroidery"<br>            ]<br>        },<br>        {<br>            "id": 17644,<br>            "title": "Solid White / M",<br>            "options": {<br>                "color": "Solid White",<br>                "size": "M"<br>            },<br>            "placeholders": [<br>                {<br>                    "position": "back",<br>                    "decoration_method": "dtf",<br>                    "height": 5131,<br>                    "width": 4051<br>                },<br>                {<br>                    "position": "front",<br>                    "decoration_method": "embroidery",<br>                    "height": 5131,<br>                    "width": 4051<br>                }<br>            ],<br>            "decoration_methods": [<br>                "dtf",<br>                "embroidery"<br>            ]<br>        },<br>        {<br>            "id": 17393,<br>            "title": "Heather Grey / L",<br>            "options": {<br>                "color": "Heather Grey",<br>                "size": "L"<br>            },<br>            "placeholders": [<br>                {<br>                    "position": "back",<br>                    "decoration_method": "dtf",<br>                    "height": 5700,<br>                    "width": 4500<br>                },<br>                {<br>                    "position": "front",<br>                    "decoration_method": "embroidery",<br>                    "height": 5700,<br>                    "width": 4500<br>                }<br>            ],<br>            "decoration_methods": [<br>                "dtf",<br>                "embroidery"<br>            ]<br>        },<br>        {<br>            "id": 17429,<br>            "title": "Solid Black / L",<br>            "options": {<br>                "color": "Solid Black",<br>                "size": "L"<br>            },<br>            "placeholders": [<br>                {<br>                    "position": "back",<br>                    "decoration_method": "dtf",<br>                    "height": 5700,<br>                    "width": 4500<br>                },<br>                {<br>                    "position": "front",<br>                    "decoration_method": "embroidery",<br>                    "height": 5700,<br>                    "width": 4500<br>                }<br>            ],<br>            "decoration_methods": [<br>                "dtf",<br>                "embroidery"<br>            ]<br>        },<br>        {<br>            "id": 17438,<br>            "title": "Solid Scarlet / L",<br>            "options": {<br>                "color": "Solid Scarlet",<br>                "size": "L"<br>            },<br>            "placeholders": [<br>                {<br>                    "position": "back",<br>                    "decoration_method": "dtf",<br>                    "height": 5700,<br>                    "width": 4500<br>                },<br>                {<br>                    "position": "front",<br>                    "decoration_method": "embroidery",<br>                    "height": 5700,<br>                    "width": 4500<br>                }<br>            ],<br>            "decoration_methods": [<br>                "dtf",<br>                "embroidery"<br>            ]<br>        },<br>        {<br>            "id": 17447,<br>            "title": "Solid Cool Blue / L",<br>            "options": {<br>                "color": "Solid Cool Blue",<br>                "size": "L"<br>            },<br>            "placeholders": [<br>                {<br>                    "position": "back",<br>                    "decoration_method": "dtf",<br>                    "height": 5700,<br>                    "width": 4500<br>                },<br>                {<br>                    "position": "front",<br>                    "decoration_method": "embroidery",<br>                    "height": 5700,<br>                    "width": 4500<br>                }<br>            ],<br>            "decoration_methods": [<br>                "dtf",<br>                "embroidery"<br>            ]<br>        },<br>        {<br>            "id": 17456,<br>            "title": "Solid Cream / L",<br>            "options": {<br>                "color": "Solid Cream",<br>                "size": "L"<br>            },<br>            "placeholders": [<br>                {<br>                    "position": "back",<br>                    "decoration_method": "dtf",<br>                    "height": 5700,<br>                    "width": 4500<br>                },<br>                {<br>                    "position": "front",<br>                    "decoration_method": "embroidery",<br>                    "height": 5700,<br>                    "width": 4500<br>                }<br>            ],<br>            "decoration_methods": [<br>                "dtf",<br>                "embroidery"<br>            ]<br>        },<br>        {<br>            "id": 17465,<br>            "title": "Solid Dark Chocolate / L",<br>            "options": {<br>                "color": "Solid Dark Chocolate",<br>                "size": "L"<br>            },<br>            "placeholders": [<br>                {<br>                    "position": "back",<br>                    "decoration_method": "dtf",<br>                    "height": 5700,<br>                    "width": 4500<br>                },<br>                {<br>                    "position": "front",<br>                    "decoration_method": "embroidery",<br>                    "height": 5700,<br>                    "width": 4500<br>                }<br>            ],<br>            "decoration_methods": [<br>                "dtf",<br>                "embroidery"<br>            ]<br>        },<br>        {<br>            "id": 17483,<br>            "title": "Solid Heavy Metal / L",<br>            "options": {<br>                "color": "Solid Heavy Metal",<br>                "size": "L"<br>            },<br>            "placeholders": [<br>                {<br>                    "position": "back",<br>                    "decoration_method": "dtf",<br>                    "height": 5700,<br>                    "width": 4500<br>                },<br>                {<br>                    "position": "front",<br>                    "decoration_method": "embroidery",<br>                    "height": 5700,<br>                    "width": 4500<br>                }<br>            ],<br>            "decoration_methods": [<br>                "dtf",<br>                "embroidery"<br>            ]<br>        },<br>        {<br>            "id": 17492,<br>            "title": "Solid Indigo / L",<br>            "options": {<br>                "color": "Solid Indigo",<br>                "size": "L"<br>            },<br>            "placeholders": [<br>                {<br>                    "position": "back",<br>                    "decoration_method": "dtf",<br>                    "height": 5700,<br>                    "width": 4500<br>                },<br>                {<br>                    "position": "front",<br>                    "decoration_method": "embroidery",<br>                    "height": 5700,<br>                    "width": 4500<br>                }<br>            ],<br>            "decoration_methods": [<br>                "dtf",<br>                "embroidery"<br>            ]<br>        },<br>        {<br>            "id": 17519,<br>            "title": "Solid Light Blue / L",<br>            "options": {<br>                "color": "Solid Light Blue",<br>                "size": "L"<br>            },<br>            "placeholders": [<br>                {<br>                    "position": "back",<br>                    "decoration_method": "dtf",<br>                    "height": 5700,<br>                    "width": 4500<br>                },<br>                {<br>                    "position": "front",<br>                    "decoration_method": "embroidery",<br>                    "height": 5700,<br>                    "width": 4500<br>                }<br>            ],<br>            "decoration_methods": [<br>                "dtf",<br>                "embroidery"<br>            ]<br>        },<br>        {<br>            "id": 17555,<br>            "title": "Solid Maroon / L",<br>            "options": {<br>                "color": "Solid Maroon",<br>                "size": "L"<br>            },<br>            "placeholders": [<br>                {<br>                    "position": "back",<br>                    "decoration_method": "dtf",<br>                    "height": 5700,<br>                    "width": 4500<br>                },<br>                {<br>                    "position": "front",<br>                    "decoration_method": "embroidery",<br>                    "height": 5700,<br>                    "width": 4500<br>                }<br>            ],<br>            "decoration_methods": [<br>                "dtf",<br>                "embroidery"<br>            ]<br>        },<br>        {<br>            "id": 17591,<br>            "title": "Solid Red / L",<br>            "options": {<br>                "color": "Solid Red",<br>                "size": "L"<br>            },<br>            "placeholders": [<br>                {<br>                    "position": "back",<br>                    "decoration_method": "dtf",<br>                    "height": 5700,<br>                    "width": 4500<br>                },<br>                {<br>                    "position": "front",<br>                    "decoration_method": "embroidery",<br>                    "height": 5700,<br>                    "width": 4500<br>                }<br>            ],<br>            "decoration_methods": [<br>                "dtf",<br>                "embroidery"<br>            ]<br>        },<br>        {<br>            "id": 17600,<br>            "title": "Solid Royal / L",<br>            "options": {<br>                "color": "Solid Royal",<br>                "size": "L"<br>            },<br>            "placeholders": [<br>                {<br>                    "position": "back",<br>                    "decoration_method": "dtf",<br>                    "height": 5700,<br>                    "width": 4500<br>                },<br>                {<br>                    "position": "front",<br>                    "decoration_method": "embroidery",<br>                    "height": 5700,<br>                    "width": 4500<br>                }<br>            ],<br>            "decoration_methods": [<br>                "dtf",<br>                "embroidery"<br>            ]<br>        },<br>        {<br>            "id": 17609,<br>            "title": "Solid Sand / L",<br>            "options": {<br>                "color": "Solid Sand",<br>                "size": "L"<br>            },<br>            "placeholders": [<br>                {<br>                    "position": "back",<br>                    "decoration_method": "dtf",<br>                    "height": 5700,<br>                    "width": 4500<br>                },<br>                {<br>                    "position": "front",<br>                    "decoration_method": "embroidery",<br>                    "height": 5700,<br>                    "width": 4500<br>                }<br>            ],<br>            "decoration_methods": [<br>                "dtf",<br>                "embroidery"<br>            ]<br>        },<br>        {<br>            "id": 17645,<br>            "title": "Solid White / L",<br>            "options": {<br>                "color": "Solid White",<br>                "size": "L"<br>            },<br>            "placeholders": [<br>                {<br>                    "position": "back",<br>                    "decoration_method": "dtf",<br>                    "height": 5700,<br>                    "width": 4500<br>                },<br>                {<br>                    "position": "front",<br>                    "decoration_method": "embroidery",<br>                    "height": 5700,<br>                    "width": 4500<br>                }<br>            ],<br>            "decoration_methods": [<br>                "dtf",<br>                "embroidery"<br>            ]<br>        },<br>        {<br>            "id": 17394,<br>            "title": "Heather Grey / XL",<br>            "options": {<br>                "color": "Heather Grey",<br>                "size": "XL"<br>            },<br>            "placeholders": [<br>                {<br>                    "position": "back",<br>                    "decoration_method": "dtf",<br>                    "height": 5700,<br>                    "width": 4500<br>                },<br>                {<br>                    "position": "front",<br>                    "decoration_method": "embroidery",<br>                    "height": 5700,<br>                    "width": 4500<br>                }<br>            ],<br>            "decoration_methods": [<br>                "dtf",<br>                "embroidery"<br>            ]<br>        },<br>        {<br>            "id": 17430,<br>            "title": "Solid Black / XL",<br>            "options": {<br>                "color": "Solid Black",<br>                "size": "XL"<br>            },<br>            "placeholders": [<br>                {<br>                    "position": "back",<br>                    "decoration_method": "dtf",<br>                    "height": 5700,<br>                    "width": 4500<br>                },<br>                {<br>                    "position": "front",<br>                    "decoration_method": "embroidery",<br>                    "height": 5700,<br>                    "width": 4500<br>                }<br>            ],<br>            "decoration_methods": [<br>                "dtf",<br>                "embroidery"<br>            ]<br>        },<br>        {<br>            "id": 17439,<br>            "title": "Solid Scarlet / XL",<br>            "options": {<br>                "color": "Solid Scarlet",<br>                "size": "XL"<br>            },<br>            "placeholders": [<br>                {<br>                    "position": "back",<br>                    "decoration_method": "dtf",<br>                    "height": 5700,<br>                    "width": 4500<br>                },<br>                {<br>                    "position": "front",<br>                    "decoration_method": "embroidery",<br>                    "height": 5700,<br>                    "width": 4500<br>                }<br>            ],<br>            "decoration_methods": [<br>                "dtf",<br>                "embroidery"<br>            ]<br>        },<br>        {<br>            "id": 17448,<br>            "title": "Solid Cool Blue / XL",<br>            "options": {<br>                "color": "Solid Cool Blue",<br>                "size": "XL"<br>            },<br>            "placeholders": [<br>                {<br>                    "position": "back",<br>                    "decoration_method": "dtf",<br>                    "height": 5700,<br>                    "width": 4500<br>                },<br>                {<br>                    "position": "front",<br>                    "decoration_method": "embroidery",<br>                    "height": 5700,<br>                    "width": 4500<br>                }<br>            ],<br>            "decoration_methods": [<br>                "dtf",<br>                "embroidery"<br>            ]<br>        },<br>        {<br>            "id": 17457,<br>            "title": "Solid Cream / XL",<br>            "options": {<br>                "color": "Solid Cream",<br>                "size": "XL"<br>            },<br>            "placeholders": [<br>                {<br>                    "position": "back",<br>                    "decoration_method": "dtf",<br>                    "height": 5700,<br>                    "width": 4500<br>                },<br>                {<br>                    "position": "front",<br>                    "decoration_method": "embroidery",<br>                    "height": 5700,<br>                    "width": 4500<br>                }<br>            ],<br>            "decoration_methods": [<br>                "dtf",<br>                "embroidery"<br>            ]<br>        },<br>        {<br>            "id": 17466,<br>            "title": "Solid Dark Chocolate / XL",<br>            "options": {<br>                "color": "Solid Dark Chocolate",<br>                "size": "XL"<br>            },<br>            "placeholders": [<br>                {<br>                    "position": "back",<br>                    "decoration_method": "dtf",<br>                    "height": 5700,<br>                    "width": 4500<br>                },<br>                {<br>                    "position": "front",<br>                    "decoration_method": "embroidery",<br>                    "height": 5700,<br>                    "width": 4500<br>                }<br>            ],<br>            "decoration_methods": [<br>                "dtf",<br>                "embroidery"<br>            ]<br>        },<br>        {<br>            "id": 17484,<br>            "title": "Solid Heavy Metal / XL",<br>            "options": {<br>                "color": "Solid Heavy Metal",<br>                "size": "XL"<br>            },<br>            "placeholders": [<br>                {<br>                    "position": "back",<br>                    "decoration_method": "dtf",<br>                    "height": 5700,<br>                    "width": 4500<br>                },<br>                {<br>                    "position": "front",<br>                    "decoration_method": "embroidery",<br>                    "height": 5700,<br>                    "width": 4500<br>                }<br>            ],<br>            "decoration_methods": [<br>                "dtf",<br>                "embroidery"<br>            ]<br>        },<br>        {<br>            "id": 17493,<br>            "title": "Solid Indigo / XL",<br>            "options": {<br>                "color": "Solid Indigo",<br>                "size": "XL"<br>            },<br>            "placeholders": [<br>                {<br>                    "position": "back",<br>                    "decoration_method": "dtf",<br>                    "height": 5700,<br>                    "width": 4500<br>                },<br>                {<br>                    "position": "front",<br>                    "decoration_method": "embroidery",<br>                    "height": 5700,<br>                    "width": 4500<br>                }<br>            ],<br>            "decoration_methods": [<br>                "dtf",<br>                "embroidery"<br>            ]<br>        },<br>        {<br>            "id": 17520,<br>            "title": "Solid Light Blue / XL",<br>            "options": {<br>                "color": "Solid Light Blue",<br>                "size": "XL"<br>            },<br>            "placeholders": [<br>                {<br>                    "position": "back",<br>                    "decoration_method": "dtf",<br>                    "height": 5700,<br>                    "width": 4500<br>                },<br>                {<br>                    "position": "front",<br>                    "decoration_method": "embroidery",<br>                    "height": 5700,<br>                    "width": 4500<br>                }<br>            ],<br>            "decoration_methods": [<br>                "dtf",<br>                "embroidery"<br>            ]<br>        },<br>        {<br>            "id": 17556,<br>            "title": "Solid Maroon / XL",<br>            "options": {<br>                "color": "Solid Maroon",<br>                "size": "XL"<br>            },<br>            "placeholders": [<br>                {<br>                    "position": "back",<br>                    "decoration_method": "dtf",<br>                    "height": 5700,<br>                    "width": 4500<br>                },<br>                {<br>                    "position": "front",<br>                    "decoration_method": "embroidery",<br>                    "height": 5700,<br>                    "width": 4500<br>                }<br>            ],<br>            "decoration_methods": [<br>                "dtf",<br>                "embroidery"<br>            ]<br>        },<br>        {<br>            "id": 17592,<br>            "title": "Solid Red / XL",<br>            "options": {<br>                "color": "Solid Red",<br>                "size": "XL"<br>            },<br>            "placeholders": [<br>                {<br>                    "position": "back",<br>                    "decoration_method": "dtf",<br>                    "height": 5700,<br>                    "width": 4500<br>                },<br>                {<br>                    "position": "front",<br>                    "decoration_method": "embroidery",<br>                    "height": 5700,<br>                    "width": 4500<br>                }<br>            ],<br>            "decoration_methods": [<br>                "dtf",<br>                "embroidery"<br>            ]<br>        },<br>        {<br>            "id": 17601,<br>            "title": "Solid Royal / XL",<br>            "options": {<br>                "color": "Solid Royal",<br>                "size": "XL"<br>            },<br>            "placeholders": [<br>                {<br>                    "position": "back",<br>                    "decoration_method": "dtf",<br>                    "height": 5700,<br>                    "width": 4500<br>                },<br>                {<br>                    "position": "front",<br>                    "decoration_method": "embroidery",<br>                    "height": 5700,<br>                    "width": 4500<br>                }<br>            ],<br>            "decoration_methods": [<br>                "dtf",<br>                "embroidery"<br>            ]<br>        },<br>        {<br>            "id": 17610,<br>            "title": "Solid Sand / XL",<br>            "options": {<br>                "color": "Solid Sand",<br>                "size": "XL"<br>            },<br>            "placeholders": [<br>                {<br>                    "position": "back",<br>                    "decoration_method": "dtf",<br>                    "height": 5700,<br>                    "width": 4500<br>                },<br>                {<br>                    "position": "front",<br>                    "decoration_method": "embroidery",<br>                    "height": 5700,<br>                    "width": 4500<br>                }<br>            ],<br>            "decoration_methods": [<br>                "dtf",<br>                "embroidery"<br>            ]<br>        },<br>        {<br>            "id": 17646,<br>            "title": "Solid White / XL",<br>            "options": {<br>                "color": "Solid White",<br>                "size": "XL"<br>            },<br>            "placeholders": [<br>                {<br>                    "position": "back",<br>                    "decoration_method": "dtf",<br>                    "height": 5700,<br>                    "width": 4500<br>                },<br>                {<br>                    "position": "front",<br>                    "decoration_method": "embroidery",<br>                    "height": 5700,<br>                    "width": 4500<br>                }<br>            ],<br>            "decoration_methods": [<br>                "dtf",<br>                "embroidery"<br>            ]<br>        },<br>        {<br>            "id": 17395,<br>            "title": "Heather Grey / 2XL",<br>            "options": {<br>                "color": "Heather Grey",<br>                "size": "2XL"<br>            },<br>            "placeholders": [<br>                {<br>                    "position": "back",<br>                    "decoration_method": "dtf",<br>                    "height": 5700,<br>                    "width": 4500<br>                },<br>                {<br>                    "position": "front",<br>                    "decoration_method": "embroidery",<br>                    "height": 5700,<br>                    "width": 4500<br>                }<br>            ],<br>            "decoration_methods": [<br>                "dtf",<br>                "embroidery"<br>            ]<br>        },<br>        {<br>            "id": 17431,<br>            "title": "Solid Black / 2XL",<br>            "options": {<br>                "color": "Solid Black",<br>                "size": "2XL"<br>            },<br>            "placeholders": [<br>                {<br>                    "position": "back",<br>                    "decoration_method": "dtf",<br>                    "height": 5700,<br>                    "width": 4500<br>                },<br>                {<br>                    "position": "front",<br>                    "decoration_method": "embroidery",<br>                    "height": 5700,<br>                    "width": 4500<br>                }<br>            ],<br>            "decoration_methods": [<br>                "dtf",<br>                "embroidery"<br>            ]<br>        },<br>        {<br>            "id": 17440,<br>            "title": "Solid Scarlet / 2XL",<br>            "options": {<br>                "color": "Solid Scarlet",<br>                "size": "2XL"<br>            },<br>            "placeholders": [<br>                {<br>                    "position": "back",<br>                    "decoration_method": "dtf",<br>                    "height": 5700,<br>                    "width": 4500<br>                },<br>                {<br>                    "position": "front",<br>                    "decoration_method": "embroidery",<br>                    "height": 5700,<br>                    "width": 4500<br>                }<br>            ],<br>            "decoration_methods": [<br>                "dtf",<br>                "embroidery"<br>            ]<br>        },<br>        {<br>            "id": 17449,<br>            "title": "Solid Cool Blue / 2XL",<br>            "options": {<br>                "color": "Solid Cool Blue",<br>                "size": "2XL"<br>            },<br>            "placeholders": [<br>                {<br>                    "position": "back",<br>                    "decoration_method": "dtf",<br>                    "height": 5700,<br>                    "width": 4500<br>                },<br>                {<br>                    "position": "front",<br>                    "decoration_method": "embroidery",<br>                    "height": 5700,<br>                    "width": 4500<br>                }<br>            ],<br>            "decoration_methods": [<br>                "dtf",<br>                "embroidery"<br>            ]<br>        },<br>        {<br>            "id": 17458,<br>            "title": "Solid Cream / 2XL",<br>            "options": {<br>                "color": "Solid Cream",<br>                "size": "2XL"<br>            },<br>            "placeholders": [<br>                {<br>                    "position": "back",<br>                    "decoration_method": "dtf",<br>                    "height": 5700,<br>                    "width": 4500<br>                },<br>                {<br>                    "position": "front",<br>                    "decoration_method": "embroidery",<br>                    "height": 5700,<br>                    "width": 4500<br>                }<br>            ],<br>            "decoration_methods": [<br>                "dtf",<br>                "embroidery"<br>            ]<br>        },<br>        {<br>            "id": 17467,<br>            "title": "Solid Dark Chocolate / 2XL",<br>            "options": {<br>                "color": "Solid Dark Chocolate",<br>                "size": "2XL"<br>            },<br>            "placeholders": [<br>                {<br>                    "position": "back",<br>                    "decoration_method": "dtf",<br>                    "height": 5700,<br>                    "width": 4500<br>                },<br>                {<br>                    "position": "front",<br>                    "decoration_method": "embroidery",<br>                    "height": 5700,<br>                    "width": 4500<br>                }<br>            ],<br>            "decoration_methods": [<br>                "dtf",<br>                "embroidery"<br>            ]<br>        },<br>        {<br>            "id": 17485,<br>            "title": "Solid Heavy Metal / 2XL",<br>            "options": {<br>                "color": "Solid Heavy Metal",<br>                "size": "2XL"<br>            },<br>            "placeholders": [<br>                {<br>                    "position": "back",<br>                    "decoration_method": "dtf",<br>                    "height": 5700,<br>                    "width": 4500<br>                },<br>                {<br>                    "position": "front",<br>                    "decoration_method": "embroidery",<br>                    "height": 5700,<br>                    "width": 4500<br>                }<br>            ],<br>            "decoration_methods": [<br>                "dtf",<br>                "embroidery"<br>            ]<br>        },<br>        {<br>            "id": 17494,<br>            "title": "Solid Indigo / 2XL",<br>            "options": {<br>                "color": "Solid Indigo",<br>                "size": "2XL"<br>            },<br>            "placeholders": [<br>                {<br>                    "position": "back",<br>                    "decoration_method": "dtf",<br>                    "height": 5700,<br>                    "width": 4500<br>                },<br>                {<br>                    "position": "front",<br>                    "decoration_method": "embroidery",<br>                    "height": 5700,<br>                    "width": 4500<br>                }<br>            ],<br>            "decoration_methods": [<br>                "dtf",<br>                "embroidery"<br>            ]<br>        },<br>        {<br>            "id": 17521,<br>            "title": "Solid Light Blue / 2XL",<br>            "options": {<br>                "color": "Solid Light Blue",<br>                "size": "2XL"<br>            },<br>            "placeholders": [<br>                {<br>                    "position": "back",<br>                    "decoration_method": "dtf",<br>                    "height": 5700,<br>                    "width": 4500<br>                },<br>                {<br>                    "position": "front",<br>                    "decoration_method": "embroidery",<br>                    "height": 5700,<br>                    "width": 4500<br>                }<br>            ],<br>            "decoration_methods": [<br>                "dtf",<br>                "embroidery"<br>            ]<br>        },<br>        {<br>            "id": 17557,<br>            "title": "Solid Maroon / 2XL",<br>            "options": {<br>                "color": "Solid Maroon",<br>                "size": "2XL"<br>            },<br>            "placeholders": [<br>                {<br>                    "position": "back",<br>                    "decoration_method": "dtf",<br>                    "height": 5700,<br>                    "width": 4500<br>                },<br>                {<br>                    "position": "front",<br>                    "decoration_method": "embroidery",<br>                    "height": 5700,<br>                    "width": 4500<br>                }<br>            ],<br>            "decoration_methods": [<br>                "dtf",<br>                "embroidery"<br>            ]<br>        },<br>        {<br>            "id": 17593,<br>            "title": "Solid Red / 2XL",<br>            "options": {<br>                "color": "Solid Red",<br>                "size": "2XL"<br>            },<br>            "placeholders": [<br>                {<br>                    "position": "back",<br>                    "decoration_method": "dtf",<br>                    "height": 5700,<br>                    "width": 4500<br>                },<br>                {<br>                    "position": "front",<br>                    "decoration_method": "embroidery",<br>                    "height": 5700,<br>                    "width": 4500<br>                }<br>            ],<br>            "decoration_methods": [<br>                "dtf",<br>                "embroidery"<br>            ]<br>        },<br>        {<br>            "id": 17602,<br>            "title": "Solid Royal / 2XL",<br>            "options": {<br>                "color": "Solid Royal",<br>                "size": "2XL"<br>            },<br>            "placeholders": [<br>                {<br>                    "position": "back",<br>                    "decoration_method": "dtf",<br>                    "height": 5700,<br>                    "width": 4500<br>                },<br>                {<br>                    "position": "front",<br>                    "decoration_method": "embroidery",<br>                    "height": 5700,<br>                    "width": 4500<br>                }<br>            ],<br>            "decoration_methods": [<br>                "dtf",<br>                "embroidery"<br>            ]<br>        },<br>        {<br>            "id": 17611,<br>            "title": "Solid Sand / 2XL",<br>            "options": {<br>                "color": "Solid Sand",<br>                "size": "2XL"<br>            },<br>            "placeholders": [<br>                {<br>                    "position": "back",<br>                    "decoration_method": "dtf",<br>                    "height": 5700,<br>                    "width": 4500<br>                },<br>                {<br>                    "position": "front",<br>                    "decoration_method": "embroidery",<br>                    "height": 5700,<br>                    "width": 4500<br>                }<br>            ],<br>            "decoration_methods": [<br>                "dtf",<br>                "embroidery"<br>            ]<br>        },<br>        {<br>            "id": 17647,<br>            "title": "Solid White / 2XL",<br>            "options": {<br>                "color": "Solid White",<br>                "size": "2XL"<br>            },<br>            "placeholders": [<br>                {<br>                    "position": "back",<br>                    "decoration_method": "dtf",<br>                    "height": 5700,<br>                    "width": 4500<br>                },<br>                {<br>                    "position": "front",<br>                    "decoration_method": "embroidery",<br>                    "height": 5700,<br>                    "width": 4500<br>                }<br>            ],<br>            "decoration_methods": [<br>                "dtf",<br>                "embroidery"<br>            ]<br>        },<br>        {<br>            "id": 17396,<br>            "title": "Heather Grey / 3XL",<br>            "options": {<br>                "color": "Heather Grey",<br>                "size": "3XL"<br>            },<br>            "placeholders": [<br>                {<br>                    "position": "back",<br>                    "decoration_method": "dtf",<br>                    "height": 5700,<br>                    "width": 4500<br>                },<br>                {<br>                    "position": "front",<br>                    "decoration_method": "embroidery",<br>                    "height": 5700,<br>                    "width": 4500<br>                }<br>            ],<br>            "decoration_methods": [<br>                "dtf",<br>                "embroidery"<br>            ]<br>        },<br>        {<br>            "id": 17432,<br>            "title": "Solid Black / 3XL",<br>            "options": {<br>                "color": "Solid Black",<br>                "size": "3XL"<br>            },<br>            "placeholders": [<br>                {<br>                    "position": "back",<br>                    "decoration_method": "dtf",<br>                    "height": 5700,<br>                    "width": 4500<br>                },<br>                {<br>                    "position": "front",<br>                    "decoration_method": "embroidery",<br>                    "height": 5700,<br>                    "width": 4500<br>                }<br>            ],<br>            "decoration_methods": [<br>                "dtf",<br>                "embroidery"<br>            ]<br>        },<br>        {<br>            "id": 17441,<br>            "title": "Solid Scarlet / 3XL",<br>            "options": {<br>                "color": "Solid Scarlet",<br>                "size": "3XL"<br>            },<br>            "placeholders": [<br>                {<br>                    "position": "back",<br>                    "decoration_method": "dtf",<br>                    "height": 5700,<br>                    "width": 4500<br>                },<br>                {<br>                    "position": "front",<br>                    "decoration_method": "embroidery",<br>                    "height": 5700,<br>                    "width": 4500<br>                }<br>            ],<br>            "decoration_methods": [<br>                "dtf",<br>                "embroidery"<br>            ]<br>        },<br>        {<br>            "id": 17450,<br>            "title": "Solid Cool Blue / 3XL",<br>            "options": {<br>                "color": "Solid Cool Blue",<br>                "size": "3XL"<br>            },<br>            "placeholders": [<br>                {<br>                    "position": "back",<br>                    "decoration_method": "dtf",<br>                    "height": 5700,<br>                    "width": 4500<br>                },<br>                {<br>                    "position": "front",<br>                    "decoration_method": "embroidery",<br>                    "height": 5700,<br>                    "width": 4500<br>                }<br>            ],<br>            "decoration_methods": [<br>                "dtf",<br>                "embroidery"<br>            ]<br>        },<br>        {<br>            "id": 17459,<br>            "title": "Solid Cream / 3XL",<br>            "options": {<br>                "color": "Solid Cream",<br>                "size": "3XL"<br>            },<br>            "placeholders": [<br>                {<br>                    "position": "back",<br>                    "decoration_method": "dtf",<br>                    "height": 5700,<br>                    "width": 4500<br>                },<br>                {<br>                    "position": "front",<br>                    "decoration_method": "embroidery",<br>                    "height": 5700,<br>                    "width": 4500<br>                }<br>            ],<br>            "decoration_methods": [<br>                "dtf",<br>                "embroidery"<br>            ]<br>        },<br>        {<br>            "id": 17468,<br>            "title": "Solid Dark Chocolate / 3XL",<br>            "options": {<br>                "color": "Solid Dark Chocolate",<br>                "size": "3XL"<br>            },<br>            "placeholders": [<br>                {<br>                    "position": "back",<br>                    "decoration_method": "dtf",<br>                    "height": 5700,<br>                    "width": 4500<br>                },<br>                {<br>                    "position": "front",<br>                    "decoration_method": "embroidery",<br>                    "height": 5700,<br>                    "width": 4500<br>                }<br>            ],<br>            "decoration_methods": [<br>                "dtf",<br>                "embroidery"<br>            ]<br>        },<br>        {<br>            "id": 17486,<br>            "title": "Solid Heavy Metal / 3XL",<br>            "options": {<br>                "color": "Solid Heavy Metal",<br>                "size": "3XL"<br>            },<br>            "placeholders": [<br>                {<br>                    "position": "back",<br>                    "decoration_method": "dtf",<br>                    "height": 5700,<br>                    "width": 4500<br>                },<br>                {<br>                    "position": "front",<br>                    "decoration_method": "embroidery",<br>                    "height": 5700,<br>                    "width": 4500<br>                }<br>            ],<br>            "decoration_methods": [<br>                "dtf",<br>                "embroidery"<br>            ]<br>        },<br>        {<br>            "id": 17495,<br>            "title": "Solid Indigo / 3XL",<br>            "options": {<br>                "color": "Solid Indigo",<br>                "size": "3XL"<br>            },<br>            "placeholders": [<br>                {<br>                    "position": "back",<br>                    "decoration_method": "dtf",<br>                    "height": 5700,<br>                    "width": 4500<br>                },<br>                {<br>                    "position": "front",<br>                    "decoration_method": "embroidery",<br>                    "height": 5700,<br>                    "width": 4500<br>                }<br>            ],<br>            "decoration_methods": [<br>                "dtf",<br>                "embroidery"<br>            ]<br>        },<br>        {<br>            "id": 17522,<br>            "title": "Solid Light Blue / 3XL",<br>            "options": {<br>                "color": "Solid Light Blue",<br>                "size": "3XL"<br>            },<br>            "placeholders": [<br>                {<br>                    "position": "back",<br>                    "decoration_method": "dtf",<br>                    "height": 5700,<br>                    "width": 4500<br>                },<br>                {<br>                    "position": "front",<br>                    "decoration_method": "embroidery",<br>                    "height": 5700,<br>                    "width": 4500<br>                }<br>            ],<br>            "decoration_methods": [<br>                "dtf",<br>                "embroidery"<br>            ]<br>        },<br>        {<br>            "id": 17558,<br>            "title": "Solid Maroon / 3XL",<br>            "options": {<br>                "color": "Solid Maroon",<br>                "size": "3XL"<br>            },<br>            "placeholders": [<br>                {<br>                    "position": "back",<br>                    "decoration_method": "dtf",<br>                    "height": 5700,<br>                    "width": 4500<br>                },<br>                {<br>                    "position": "front",<br>                    "decoration_method": "embroidery",<br>                    "height": 5700,<br>                    "width": 4500<br>                }<br>            ],<br>            "decoration_methods": [<br>                "dtf",<br>                "embroidery"<br>            ]<br>        },<br>        {<br>            "id": 17594,<br>            "title": "Solid Red / 3XL",<br>            "options": {<br>                "color": "Solid Red",<br>                "size": "3XL"<br>            },<br>            "placeholders": [<br>                {<br>                    "position": "back",<br>                    "decoration_method": "dtf",<br>                    "height": 5700,<br>                    "width": 4500<br>                },<br>                {<br>                    "position": "front",<br>                    "decoration_method": "embroidery",<br>                    "height": 5700,<br>                    "width": 4500<br>                }<br>            ],<br>            "decoration_methods": [<br>                "dtf",<br>                "embroidery"<br>            ]<br>        },<br>        {<br>            "id": 17603,<br>            "title": "Solid Royal / 3XL",<br>            "options": {<br>                "color": "Solid Royal",<br>                "size": "3XL"<br>            },<br>            "placeholders": [<br>                {<br>                    "position": "back",<br>                    "decoration_method": "dtf",<br>                    "height": 5700,<br>                    "width": 4500<br>                },<br>                {<br>                    "position": "front",<br>                    "decoration_method": "embroidery",<br>                    "height": 5700,<br>                    "width": 4500<br>                }<br>            ],<br>            "decoration_methods": [<br>                "dtf",<br>                "embroidery"<br>            ]<br>        },<br>        {<br>            "id": 17612,<br>            "title": "Solid Sand / 3XL",<br>            "options": {<br>                "color": "Solid Sand",<br>                "size": "3XL"<br>            },<br>            "placeholders": [<br>                {<br>                    "position": "back",<br>                    "decoration_method": "dtf",<br>                    "height": 5700,<br>                    "width": 4500<br>                },<br>                {<br>                    "position": "front",<br>                    "decoration_method": "embroidery",<br>                    "height": 5700,<br>                    "width": 4500<br>                }<br>            ],<br>            "decoration_methods": [<br>                "dtf",<br>                "embroidery"<br>            ]<br>        },<br>        {<br>            "id": 17648,<br>            "title": "Solid White / 3XL",<br>            "options": {<br>                "color": "Solid White",<br>                "size": "3XL"<br>            },<br>            "placeholders": [<br>                {<br>                    "position": "back",<br>                    "decoration_method": "dtf",<br>                    "height": 5700,<br>                    "width": 4500<br>                },<br>                {<br>                    "position": "front",<br>                    "decoration_method": "embroidery",<br>                    "height": 5700,<br>                    "width": 4500<br>                }<br>            ],<br>            "decoration_methods": [<br>                "dtf",<br>                "embroidery"<br>            ]<br>        }<br>    ]<br>}` |

#### Retrieve shipping information

|     |     |
| --- | --- |
| GET | /v1/catalog/blueprints/{blueprint\_id}/print\_providers/{print\_provider\_id}/shipping.json |
| **Retrieve shipping information**<br>`GET /v1/catalog/blueprints/{blueprint_id}/print_providers/{print_provider_id}/shipping.json`<br>[View Response](https://developers.printify.com/#)`{<br>    "handling_time": {<br>            "value": 30,<br>            "unit": "day"<br>        },<br>        "profiles": [<br>            {<br>                "variant_ids": [<br>                    42716,<br>                    42717,<br>                    42718,<br>                    42719,<br>                    42720,<br>                    12144,<br>                    12143,<br>                    12142,<br>                    12145,<br>                    12146,<br>                    12150,<br>                    12149,<br>                    12148,<br>                    12151,<br>                    12152,<br>                    12162,<br>                    12161,<br>                    12160,<br>                    12163,<br>                    12164,<br>                    12180,<br>                    12179,<br>                    12178,<br>                    12181,<br>                    12182,<br>                    12192,<br>                    12191,<br>                    12190,<br>                    12193,<br>                    12194,<br>                    11874,<br>                    11873,<br>                    11872,<br>                    11875,<br>                    11876,<br>                    11892,<br>                    11891,<br>                    11890,<br>                    11893,<br>                    11894,<br>                    11898,<br>                    11897,<br>                    11896,<br>                    11899,<br>                    11900,<br>                    11934,<br>                    11933,<br>                    11932,<br>                    11935,<br>                    11936,<br>                    11946,<br>                    11945,<br>                    11944,<br>                    11947,<br>                    11948,<br>                    11952,<br>                    11951,<br>                    11950,<br>                    11953,<br>                    11954,<br>                    11958,<br>                    11957,<br>                    11956,<br>                    11959,<br>                    11960,<br>                    11976,<br>                    11975,<br>                    11974,<br>                    11977,<br>                    11978,<br>                    11988,<br>                    11987,<br>                    11986,<br>                    11989,<br>                    11990,<br>                    12012,<br>                    12011,<br>                    12010,<br>                    12013,<br>                    12014,<br>                    12018,<br>                    12017,<br>                    12016,<br>                    12019,<br>                    12020,<br>                    12024,<br>                    12023,<br>                    12022,<br>                    12025,<br>                    12026,<br>                    12030,<br>                    12029,<br>                    12028,<br>                    12031,<br>                    12032,<br>                    12054,<br>                    12053,<br>                    12052,<br>                    12055,<br>                    12056,<br>                    12072,<br>                    12071,<br>                    12070,<br>                    12073,<br>                    12074,<br>                    12102,<br>                    12101,<br>                    12100,<br>                    12103,<br>                    12104,<br>                    12126,<br>                    12125,<br>                    12124,<br>                    12127,<br>                    12128<br>                ],<br>                "first_item": {<br>                    "cost": 450,<br>                    "currency": "USD"<br>                },<br>                "additional_items": {<br>                    "cost": 0,<br>                    "currency": "USD"<br>                },<br>                "countries": [<br>                    "US"<br>                ]<br>            },<br>            {<br>                "variant_ids": [<br>                    42716,<br>                    42717,<br>                    42718,<br>                    42719,<br>                    42720,<br>                    12144,<br>                    12143,<br>                    12142,<br>                    12145,<br>                    12146,<br>                    12150,<br>                    12149,<br>                    12148,<br>                    12151,<br>                    12152,<br>                    12162,<br>                    12161,<br>                    12160,<br>                    12163,<br>                    12164,<br>                    12180,<br>                    12179,<br>                    12178,<br>                    12181,<br>                    12182,<br>                    12192,<br>                    12191,<br>                    12190,<br>                    12193,<br>                    12194,<br>                    11874,<br>                    11873,<br>                    11872,<br>                    11875,<br>                    11876,<br>                    11892,<br>                    11891,<br>                    11890,<br>                    11893,<br>                    11894,<br>                    11898,<br>                    11897,<br>                    11896,<br>                    11899,<br>                    11900,<br>                    11934,<br>                    11933,<br>                    11932,<br>                    11935,<br>                    11936,<br>                    11946,<br>                    11945,<br>                    11944,<br>                    11947,<br>                    11948,<br>                    11952,<br>                    11951,<br>                    11950,<br>                    11953,<br>                    11954,<br>                    11958,<br>                    11957,<br>                    11956,<br>                    11959,<br>                    11960,<br>                    11976,<br>                    11975,<br>                    11974,<br>                    11977,<br>                    11978,<br>                    11988,<br>                    11987,<br>                    11986,<br>                    11989,<br>                    11990,<br>                    12012,<br>                    12011,<br>                    12010,<br>                    12013,<br>                    12014,<br>                    12018,<br>                    12017,<br>                    12016,<br>                    12019,<br>                    12020,<br>                    12024,<br>                    12023,<br>                    12022,<br>                    12025,<br>                    12026,<br>                    12030,<br>                    12029,<br>                    12028,<br>                    12031,<br>                    12032,<br>                    12054,<br>                    12053,<br>                    12052,<br>                    12055,<br>                    12056,<br>                    12072,<br>                    12071,<br>                    12070,<br>                    12073,<br>                    12074,<br>                    12102,<br>                    12101,<br>                    12100,<br>                    12103,<br>                    12104,<br>                    12126,<br>                    12125,<br>                    12124,<br>                    12127,<br>                    12128<br>                ],<br>                "first_item": {<br>                    "cost": 650,<br>                    "currency": "USD"<br>                },<br>                "additional_items": {<br>                    "cost": 0,<br>                    "currency": "USD"<br>                },<br>                "countries": [<br>                    "CA",<br>                    "AU",<br>                    "AT",<br>                    "BE",<br>                    "BG",<br>                    "HR",<br>                    "CY",<br>                    "CZ",<br>                    "DK",<br>                    "EE",<br>                    "FI",<br>                    "FR",<br>                    "DE",<br>                    "GR",<br>                    "HU",<br>                    "IS",<br>                    "IE",<br>                    "IT",<br>                    "LT",<br>                    "LV",<br>                    "LU",<br>                    "MT",<br>                    "NL",<br>                    "NO",<br>                    "PT",<br>                    "PL",<br>                    "RO",<br>                    "SK",<br>                    "SI",<br>                    "ES",<br>                    "SE",<br>                    "CH",<br>                    "TR",<br>                    "GB",<br>                    "GI",<br>                    "AX"<br>                ]<br>            },<br>            {<br>                "variant_ids": [<br>                    42716,<br>                    42717,<br>                    42718,<br>                    42719,<br>                    42720,<br>                    12144,<br>                    12143,<br>                    12142,<br>                    12145,<br>                    12146,<br>                    12150,<br>                    12149,<br>                    12148,<br>                    12151,<br>                    12152,<br>                    12162,<br>                    12161,<br>                    12160,<br>                    12163,<br>                    12164,<br>                    12180,<br>                    12179,<br>                    12178,<br>                    12181,<br>                    12182,<br>                    12192,<br>                    12191,<br>                    12190,<br>                    12193,<br>                    12194,<br>                    11874,<br>                    11873,<br>                    11872,<br>                    11875,<br>                    11876,<br>                    11892,<br>                    11891,<br>                    11890,<br>                    11893,<br>                    11894,<br>                    11898,<br>                    11897,<br>                    11896,<br>                    11899,<br>                    11900,<br>                    11934,<br>                    11933,<br>                    11932,<br>                    11935,<br>                    11936,<br>                    11946,<br>                    11945,<br>                    11944,<br>                    11947,<br>                    11948,<br>                    11952,<br>                    11951,<br>                    11950,<br>                    11953,<br>                    11954,<br>                    11958,<br>                    11957,<br>                    11956,<br>                    11959,<br>                    11960,<br>                    11976,<br>                    11975,<br>                    11974,<br>                    11977,<br>                    11978,<br>                    11988,<br>                    11987,<br>                    11986,<br>                    11989,<br>                    11990,<br>                    12012,<br>                    12011,<br>                    12010,<br>                    12013,<br>                    12014,<br>                    12018,<br>                    12017,<br>                    12016,<br>                    12019,<br>                    12020,<br>                    12024,<br>                    12023,<br>                    12022,<br>                    12025,<br>                    12026,<br>                    12030,<br>                    12029,<br>                    12028,<br>                    12031,<br>                    12032,<br>                    12054,<br>                    12053,<br>                    12052,<br>                    12055,<br>                    12056,<br>                    12072,<br>                    12071,<br>                    12070,<br>                    12073,<br>                    12074,<br>                    12102,<br>                    12101,<br>                    12100,<br>                    12103,<br>                    12104,<br>                    12126,<br>                    12125,<br>                    12124,<br>                    12127,<br>                    12128<br>                ],<br>                "first_item": {<br>                    "cost": 1100,<br>                    "currency": "USD"<br>                },<br>                "additional_items": {<br>                    "cost": 0,<br>                    "currency": "USD"<br>                },<br>                "countries": [<br>                    "REST_OF_THE_WORLD"<br>                ]<br>            }<br>        ]<br>}` |

#### Retrieve a list of available print providers

|     |     |
| --- | --- |
| GET | /v1/catalog/print\_providers.json |
| **Retrieve a list of available print providers**<br>`GET /v1/catalog/print_providers.json`<br>[View Response](https://developers.printify.com/#)`[<br>    {<br>        "id": 1,<br>        "title": "SPOKE Custom Products",<br>        "location": {<br>            "address1": "89 Weirfield St",<br>            "address2": null,<br>            "city": "Brooklyn",<br>            "country": "US",<br>            "region": "NY",<br>            "zip": "11221-5120"<br>        }<br>    },<br>    {<br>        "id": 2,<br>        "title": "CG Pro prints",<br>        "location": {<br>            "address1": "89 Weirfield St",<br>            "address2": null,<br>            "city": "Brooklyn",<br>            "country": "US",<br>            "region": "NY",<br>            "zip": "11221-5120"<br>        }<br>    },<br>    {<br>        "id": 3,<br>        "title": "The Dream Junction ",<br>        "location": {<br>            "address1": "89 Weirfield St",<br>            "address2": "",<br>            "city": "Brooklyn",<br>            "country": "US",<br>            "region": "NY",<br>            "zip": "11221-5120"<br>        }<br>    },<br>    {<br>        "id": 5,<br>        "title": "ArtGun",<br>        "location": {<br>            "address1": "89 Weirfield St",<br>            "address2": "",<br>            "city": "Brooklyn",<br>            "country": "US",<br>            "region": "NY",<br>            "zip": "11221-5120"<br>        }<br>    },<br>    {<br>        "id": 6,<br>        "title": "T shirt and Sons",<br>        "location": {<br>            "address1": "89 Weirfield St",<br>            "address2": null,<br>            "city": "Brooklyn",<br>            "country": "US",<br>            "region": "NY",<br>            "zip": "11221-5120"<br>        }<br>    },<br>    {<br>        "id": 7,<br>        "title": "Prodigi",<br>        "location": {<br>            "address1": "89 Weirfield St",<br>            "address2": null,<br>            "city": "Brooklyn",<br>            "country": "US",<br>            "region": "NY",<br>            "zip": "11221-5120"<br>        }<br>    },<br>    {<br>        "id": 8,<br>        "title": "Fifth Sun",<br>        "location": {<br>            "address1": "89 Weirfield St",<br>            "address2": null,<br>            "city": "Brooklyn",<br>            "country": "US",<br>            "region": "NY",<br>            "zip": "11221-5120"<br>        }<br>    },<br>    {<br>        "id": 9,<br>        "title": "WPaPS",<br>        "location": {<br>            "address1": "89 Weirfield St",<br>            "address2": null,<br>            "city": "Brooklyn",<br>            "country": "US",<br>            "region": "NY",<br>            "zip": "11221-5120"<br>        }<br>    },<br>    {<br>        "id": 10,<br>        "title": "MWW On Demand",<br>        "location": {<br>            "address1": "89 Weirfield St",<br>            "address2": null,<br>            "city": "Brooklyn",<br>            "country": "US",<br>            "region": "NY",<br>            "zip": "11221-5120"<br>        }<br>    },<br>    {<br>        "id": 14,<br>        "title": "ArtsAdd",<br>        "location": {<br>            "address1": "89 Weirfield St",<br>            "address2": null,<br>            "city": "Brooklyn",<br>            "country": "US",<br>            "region": "NY",<br>            "zip": "11221-5120"<br>        }<br>    },<br>    {<br>        "id": 16,<br>        "title": "MyLocker",<br>        "location": {<br>            "address1": "89 Weirfield St",<br>            "address2": null,<br>            "city": "Brooklyn",<br>            "country": "US",<br>            "region": "NY",<br>            "zip": "11221-5120"<br>        }<br>    },<br>    {<br>        "id": 20,<br>        "title": "Troupe Jewelry",<br>        "location": {<br>            "address1": "89 Weirfield St",<br>            "address2": null,<br>            "city": "Brooklyn",<br>            "country": "US",<br>            "region": "NY",<br>            "zip": "11221-5120"<br>        }<br>    },<br>    {<br>        "id": 23,<br>        "title": "WOYC",<br>        "location": {<br>            "address1": "89 Weirfield St",<br>            "address2": "",<br>            "city": "Brooklyn",<br>            "country": "US",<br>            "region": "NY",<br>            "zip": "11221-5120"<br>        }<br>    },<br>    {<br>        "id": 24,<br>        "title": "Inklocker",<br>        "location": {<br>            "address1": "89 Weirfield St",<br>            "address2": "",<br>            "city": "Brooklyn",<br>            "country": "US",<br>            "region": "NY",<br>            "zip": "11221-5120"<br>        }<br>    },<br>    {<br>        "id": 25,<br>        "title": "DTG2Go",<br>        "location": {<br>            "address1": "89 Weirfield St",<br>            "address2": "",<br>            "city": "Brooklyn",<br>            "country": "US",<br>            "region": "NY",<br>            "zip": "11221-5120"<br>        }<br>    }<br>]` |

#### Retrieve a specific print provider

|     |     |
| --- | --- |
| GET | /v1/catalog/print\_providers/{print\_provider\_id}.json |
| **Retrieve a specific print provider and a list of associated blueprint offerings**<br>`GET /v1/catalog/print_providers/{print_provider_id}.json`<br>[View Response](https://developers.printify.com/#)`{<br>    "id": 1,<br>    "title": "SPOKE Custom Products",<br>    "location": {<br>        "address1": "89 Weirfield St",<br>        "address2": null,<br>        "city": "Brooklyn",<br>        "country": "US",<br>        "region": "NY",<br>        "zip": "11221-5120"<br>    },<br>    "blueprints": [<br>        {<br>            "id": 265,<br>            "title": "Slim Iphone 8",<br>            "brand": "Case Mate",<br>            "model": "Slim Iphone 8",<br>            "images": [<br>                "https://images.printify.com/59b261c9b8e7e361c9147b1b.png"<br>            ]<br>        },<br>        {<br>            "id": 266,<br>            "title": "Tough Iphone 8",<br>            "brand": "Case Mate",<br>            "model": "Tough Iphone 8",<br>            "images": [<br>                "https://images.printify.com/59b26fbfb8e7e36254554a34.png"<br>            ]<br>        },<br>        {<br>            "id": 52,<br>            "title": "Slim Iphone 6/6s",<br>            "brand": "Case Mate",<br>            "model": "6/6s Slim",<br>            "images": [<br>                "https://images.printify.com/5853fe7dce46f30f8327f5eb.png",<br>                "https://images.printify.com/5853fe7dce46f30f8327f5ee.png"<br>            ]<br>        },<br>        {<br>            "id": 53,<br>            "title": "Tough Iphone 6/6s",<br>            "brand": "Case Mate",<br>            "model": "6/6s Tough",<br>            "images": [<br>                "https://images.printify.com/5853fe7dce46f30f8327f5f1.png",<br>                "https://images.printify.com/5853fe7dce46f30f8327f5f4.png"<br>            ]<br>        },<br>        {<br>            "id": 54,<br>            "title": "Slim Iphone 6/6s Plus",<br>            "brand": "Case Mate",<br>            "model": "6/6s Plus Slim",<br>            "images": [<br>                "https://images.printify.com/5853fe7dce46f30f8327f61b.png",<br>                "https://images.printify.com/5853fe7dce46f30f8327f61e.png"<br>            ]<br>        },<br>        {<br>            "id": 55,<br>            "title": "Tough Iphone 6/6s Plus",<br>            "brand": "Case Mate",<br>            "model": "6/6s Plus Tough",<br>            "images": [<br>                "https://images.printify.com/5853fe7dce46f30f8327f615.png",<br>                "https://images.printify.com/5853fe7dce46f30f8327f618.png"<br>            ]<br>        },<br>        {<br>            "id": 56,<br>            "title": "Slim Iphone 5/5s/5se",<br>            "brand": "Case Mate",<br>            "model": "5/5s/5se Slim",<br>            "images": [<br>                "https://images.printify.com/5853fe7dce46f30f8327f5f7.png",<br>                "https://images.printify.com/5853fe7dce46f30f8327f5fa.png"<br>            ]<br>        },<br>        {<br>            "id": 57,<br>            "title": "Tough Iphone 5/5s/5se",<br>            "brand": "Case Mate",<br>            "model": "5/5s/5se Tough",<br>            "images": [<br>                "https://images.printify.com/5853fe7dce46f30f8327f5fd.png",<br>                "https://images.printify.com/5853fe7dce46f30f8327f600.png"<br>            ]<br>        },<br>        {<br>            "id": 58,<br>            "title": "Slim Iphone 5C",<br>            "brand": "Case Mate",<br>            "model": "5C Slim",<br>            "images": [<br>                "https://images.printify.com/5853fe80ce46f30f8327f7cf.png",<br>                "https://images.printify.com/5853fe80ce46f30f8327f7d7.png"<br>            ]<br>        },<br>        {<br>            "id": 59,<br>            "title": "Slim Iphone 4/4s",<br>            "brand": "Case Mate",<br>            "model": "4/4s Slim",<br>            "images": [<br>                "https://images.printify.com/5853fe7ece46f30f8327f639.png",<br>                "https://images.printify.com/5853fe7ece46f30f8327f63c.png"<br>            ]<br>        },<br>        {<br>            "id": 60,<br>            "title": "Tough Iphone 4/4s",<br>            "brand": "Case Mate",<br>            "model": "4/4s Tough",<br>            "images": [<br>                "https://images.printify.com/5853fe7ece46f30f8327f63f.png",<br>                "https://images.printify.com/5853fe7ece46f30f8327f642.png"<br>            ]<br>        },<br>        {<br>            "id": 61,<br>            "title": "Slim Samsung Galaxy S7",<br>            "brand": "Case Mate",<br>            "model": "S7 Slim",<br>            "images": [<br>                "https://images.printify.com/5853fe7dce46f30f8327f621.png",<br>                "https://images.printify.com/5853fe7dce46f30f8327f624.png"<br>            ]<br>        },<br>        {<br>            "id": 62,<br>            "title": "Slim Samsung Galaxy S6",<br>            "brand": "Case Mate",<br>            "model": "S6 Slim",<br>            "images": [<br>                "https://images.printify.com/5853fe7dce46f30f8327f627.png",<br>                "https://images.printify.com/5853fe7ece46f30f8327f62a.png"<br>            ]<br>        },<br>        {<br>            "id": 63,<br>            "title": "Tough Samsung Galaxy S6",<br>            "brand": "Case Mate",<br>            "model": "S6 Tough",<br>            "images": [<br>                "https://images.printify.com/5853fe7ece46f30f8327f62d.png",<br>                "https://images.printify.com/5853fe7ece46f30f8327f630.png"<br>            ]<br>        },<br>        {<br>            "id": 64,<br>            "title": "Slim Samsung Galaxy S5",<br>            "brand": "Case Mate",<br>            "model": "S5 Slim",<br>            "images": [<br>                "https://images.printify.com/5853fe7ece46f30f8327f633.png",<br>                "https://images.printify.com/5853fe7ece46f30f8327f636.png"<br>            ]<br>        },<br>        {<br>            "id": 68,<br>            "title": "Mug 11oz",<br>            "brand": "Generic brand",<br>            "model": "",<br>            "images": [<br>                "https://images.printify.com/5d09e78c47045f00083cd10d.png",<br>                "https://images.printify.com/58ac5d64b2439213b51b25ff.png"<br>            ]<br>        },<br>        {<br>            "id": 69,<br>            "title": "Mug 15oz",<br>            "brand": "Generic brand",<br>            "model": "",<br>            "images": [<br>                "https://images.printify.com/5853fe7bce46f30f8327f4ff.png",<br>                "https://images.printify.com/5c5c1516a342bcb8e421d242.png"<br>            ]<br>        },<br>        {<br>            "id": 70,<br>            "title": "Stainless Steel Travel Mug",<br>            "brand": "Generic brand",<br>            "model": "",<br>            "images": [<br>                "https://images.printify.com/5d09f7e247045f00083cd110.png",<br>                "https://images.printify.com/5853fe7bce46f30f8327f502.png",<br>                "https://images.printify.com/58ac0e46b2439209155d3375.png",<br>                "https://images.printify.com/58ac5ac0b2439214ad09bd1b.png"<br>            ]<br>        },<br>        {<br>            "id": 71,<br>            "title": "Laptop Sleeve",<br>            "brand": "Generic brand",<br>            "model": "",<br>            "images": [<br>                "https://images.printify.com/5853fe7bce46f30f8327f4e2.png",<br>                "https://images.printify.com/58ac0dadb2439209e3265564.png",<br>                "https://images.printify.com/58ac0db9b24392090e55b2f8.png",<br>                "https://images.printify.com/58cbdd4eb24392676d7f6961.png",<br>                "https://images.printify.com/58cbdd67b243926fe26236c2.png"<br>            ]<br>        },<br>        {<br>            "id": 74,<br>            "title": "Spiral Notebook - Ruled Line",<br>            "brand": "Generic brand",<br>            "model": "",<br>            "images": [<br>                "https://images.printify.com/5d03643bd155b4000a00cae5.png",<br>                "https://images.printify.com/58cbed76b2439279864551c0.png",<br>                "https://images.printify.com/58cbf1ddb243926fe909d567.png"<br>            ]<br>        },<br>        {<br>            "id": 75,<br>            "title": "Journal - Ruled Line",<br>            "brand": "Generic brand",<br>            "model": "",<br>            "images": [<br>                "https://images.printify.com/5d03aa7dd155b400094c4d60.png",<br>                "https://images.printify.com/5853fe7bce46f30f8327f4de.png",<br>                "https://images.printify.com/5c49c395a342bc53475e5412.png"<br>            ]<br>        },<br>        {<br>            "id": 76,<br>            "title": "Journal - Blank",<br>            "brand": "Generic brand",<br>            "model": "",<br>            "images": [<br>                "https://images.printify.com/5d03aad4d155b4000a00cb82.png",<br>                "https://images.printify.com/585a7e24ce46f3416b5db1c7.png",<br>                "https://images.printify.com/5c49c3cba342bc53c0283808.png"<br>            ]<br>        },<br>        {<br>            "id": 84,<br>            "title": "Slim iPhone 7, iPhone 8",<br>            "brand": "Case Mate",<br>            "model": "Slim iPhone 7, iPhone 8",<br>            "images": [<br>                "https://images.printify.com/5853fe7dce46f30f8327f603.png",<br>                "https://images.printify.com/5853fe7dce46f30f8327f606.png"<br>            ]<br>        },<br>        {<br>            "id": 85,<br>            "title": "Tough iPhone 7, IPhone 8",<br>            "brand": "Case Mate",<br>            "model": "Tough iPhone 7, IPhone 8",<br>            "images": [<br>                "https://images.printify.com/5853fe7dce46f30f8327f5e5.png",<br>                "https://images.printify.com/5853fe7dce46f30f8327f5e8.png"<br>            ]<br>        },<br>        {<br>            "id": 86,<br>            "title": "Slim iPhone 7 Plus, iPhone 8 Plus",<br>            "brand": "Case Mate",<br>            "model": "Slim iPhone 7 Plus, , iPhone 8 Plus",<br>            "images": [<br>                "https://images.printify.com/5853fe7dce46f30f8327f609.png",<br>                "https://images.printify.com/5853fe7dce46f30f8327f60c.png"<br>            ]<br>        },<br>        {<br>            "id": 87,<br>            "title": "Tough iPhone 7 Plus, iPhone 8 Plus",<br>            "brand": "Case Mate",<br>            "model": "Tough iPhone 7 Plus, iPhone 8 Plus",<br>            "images": [<br>                "https://images.printify.com/5853fe7dce46f30f8327f60f.png",<br>                "https://images.printify.com/5853fe7dce46f30f8327f612.png"<br>            ]<br>        },<br>        {<br>            "id": 99,<br>            "title": "All US Phone cases",<br>            "brand": "Case Mate",<br>            "model": "",<br>            "images": [<br>                "https://images.printify.com/5853fe7dce46f30f8327f5eb.png",<br>                "https://images.printify.com/5853fe7dce46f30f8327f5ee.png",<br>                "https://images.printify.com/5853fe7dce46f30f8327f5f1.png",<br>                "https://images.printify.com/5853fe7dce46f30f8327f5f4.png",<br>                "https://images.printify.com/5853fe7dce46f30f8327f61b.png",<br>                "https://images.printify.com/5853fe7dce46f30f8327f61e.png",<br>                "https://images.printify.com/5853fe7dce46f30f8327f615.png",<br>                "https://images.printify.com/5853fe7dce46f30f8327f618.png",<br>                "https://images.printify.com/5853fe7dce46f30f8327f5f7.png",<br>                "https://images.printify.com/5853fe7dce46f30f8327f5fa.png",<br>                "https://images.printify.com/5853fe7dce46f30f8327f5fd.png",<br>                "https://images.printify.com/5853fe7dce46f30f8327f600.png",<br>                "https://images.printify.com/5853fe80ce46f30f8327f7cf.png",<br>                "https://images.printify.com/5853fe80ce46f30f8327f7d7.png",<br>                "https://images.printify.com/5853fe7ece46f30f8327f639.png",<br>                "https://images.printify.com/5853fe7ece46f30f8327f63c.png",<br>                "https://images.printify.com/5853fe7ece46f30f8327f63f.png",<br>                "https://images.printify.com/5853fe7ece46f30f8327f642.png",<br>                "https://images.printify.com/5853fe7dce46f30f8327f621.png",<br>                "https://images.printify.com/5853fe7dce46f30f8327f624.png",<br>                "https://images.printify.com/5853fe7dce46f30f8327f627.png",<br>                "https://images.printify.com/5853fe7ece46f30f8327f62a.png",<br>                "https://images.printify.com/5853fe7ece46f30f8327f62d.png",<br>                "https://images.printify.com/5853fe7ece46f30f8327f630.png",<br>                "https://images.printify.com/5853fe7ece46f30f8327f633.png",<br>                "https://images.printify.com/5853fe7ece46f30f8327f636.png",<br>                "https://images.printify.com/5853fe7dce46f30f8327f603.png",<br>                "https://images.printify.com/5853fe7dce46f30f8327f606.png",<br>                "https://images.printify.com/5853fe7dce46f30f8327f5e5.png",<br>                "https://images.printify.com/5853fe7dce46f30f8327f5e8.png",<br>                "https://images.printify.com/5853fe7dce46f30f8327f609.png",<br>                "https://images.printify.com/5853fe7dce46f30f8327f60c.png",<br>                "https://images.printify.com/5853fe7dce46f30f8327f60f.png",<br>                "https://images.printify.com/5853fe7dce46f30f8327f612.png"<br>            ]<br>        },<br>        {<br>            "id": 125,<br>            "title": "Mugs",<br>            "brand": "Generic brand",<br>            "model": "",<br>            "images": [<br>                "https://images.printify.com/5853fe7bce46f30f8327f4fc.png",<br>                "https://images.printify.com/58ac5d64b2439213b51b25ff.png",<br>                "https://images.printify.com/5853fe7bce46f30f8327f4ff.png",<br>                "https://images.printify.com/5c5c1516a342bcb8e421d242.png"<br>            ]<br>        },<br>        {<br>            "id": 268,<br>            "title": "Case Mate Slim Phone Cases",<br>            "brand": "Case Mate",<br>            "model": "",<br>            "images": [<br>                "https://images.printify.com/5d08c85847045f00097be5b3.png"<br>            ]<br>        },<br>        {<br>            "id": 269,<br>            "title": "Case Mate Tough Phone Cases",<br>            "brand": "Case Mate",<br>            "model": "",<br>            "images": [<br>                "https://images.printify.com/5d132242c1bdb8000a6e474c.png",<br>                "https://images.printify.com/5d131fadc1bdb800125d2efd.png"<br>            ]<br>        },<br>        {<br>            "id": 277,<br>            "title": "Wall clock",<br>            "brand": "Generic brand",<br>            "model": "",<br>            "images": [<br>                "https://images.printify.com/5d0b31f347045f01ae2eeb1f.png",<br>                "https://images.printify.com/5a033c07b8e7e328100d3c27.png"<br>            ]<br>        },<br>        {<br>            "id": 289,<br>            "title": "Latte mug",<br>            "brand": "Generic brand",<br>            "model": "",<br>            "images": [<br>                "https://images.printify.com/5d0a0e6047045f0189376682.png",<br>                "https://images.printify.com/5a325c76b8e7e355db3449e8.png"<br>            ]<br>        },<br>        {<br>            "id": 352,<br>            "title": "Beach Towel",<br>            "brand": "Generic brand",<br>            "model": "",<br>            "images": [<br>                "https://images.printify.com/5afeba40a342bcea7045d84e.png"<br>            ]<br>        },<br>        {<br>            "id": 353,<br>            "title": "Tumbler 20oz",<br>            "brand": "Generic brand",<br>            "model": "",<br>            "images": [<br>                "https://images.printify.com/5ad0a5baa342bc91115b6927.png"<br>            ]<br>        },<br>        {<br>            "id": 354,<br>            "title": "Tumbler 10oz",<br>            "brand": "Generic brand",<br>            "model": "",<br>            "images": [<br>                "https://images.printify.com/5ad0a68ca342bc911954d928.png"<br>            ]<br>        },<br>        {<br>            "id": 355,<br>            "title": "Can Holder",<br>            "brand": "Generic brand",<br>            "model": "",<br>            "images": [<br>                "https://images.printify.com/5ad0a53ca342bc9114070039.png"<br>            ]<br>        },<br>        {<br>            "id": 376,<br>            "title": "Sublimation Socks",<br>            "brand": "Generic brand",<br>            "model": "",<br>            "images": [<br>                "https://images.printify.com/5d13450ec1bdb800125d2f0d.png",<br>                "https://images.printify.com/5be1ae47a342bc3390628e22.png",<br>                "https://images.printify.com/5bbc8702a342bc24e4283e2c.png"<br>            ]<br>        },<br>        {<br>            "id": 384,<br>            "title": "Square Stickers",<br>            "brand": "Generic brand",<br>            "model": "",<br>            "images": [<br>                "https://images.printify.com/5cf4f606705f1900141a667c.png",<br>                "https://images.printify.com/5c6685a6a342bc4c6340bf82.png"<br>            ]<br>        },<br>        {<br>            "id": 400,<br>            "title": "Kiss-Cut Stickers",<br>            "brand": "Generic brand",<br>            "model": "",<br>            "images": [<br>                "https://images.printify.com/5cf4fabe705f190009393f38.png",<br>                "https://images.printify.com/5c48648aa342bc7e304661f2.png",<br>                "https://images.printify.com/5c4864a2a342bc7e256c1d6c.png"<br>            ]<br>        },<br>        {<br>            "id": 423,<br>            "title": "Alex' Test Product (do not delete)",<br>            "brand": "Bella+Canvas",<br>            "model": "9999",<br>            "images": [<br>                "https://images.printify.com/5c8bdf3d21a6ed001111c202.png",<br>                "https://images.printify.com/5c7565d51e58a3000964b4e2.png",<br>                "https://images.printify.com/5c8bdfa721a6ed000f1d19d2.png",<br>                "https://images.printify.com/5c8be08a21a6ed00102eaa97.png",<br>                "https://images.printify.com/5c8be09321a6ed0014663572.png"<br>            ]<br>        },<br>        {<br>            "id": 425,<br>            "title": "Mug 15oz",<br>            "brand": "Generic brand",<br>            "model": "",<br>            "images": [<br>                "https://images.printify.com/5d0a08d647045f00097be6cd.png",<br>                "https://images.printify.com/5d0a07b547045f00083cd116.png",<br>                "https://images.printify.com/5cab36e06b4a8300124cea40.png",<br>                "https://images.printify.com/5cab21ef6b4a83000970c497.png"<br>            ]<br>        },<br>        {<br>            "id": 427,<br>            "title": "Magnets",<br>            "brand": "Generic brand",<br>            "model": "",<br>            "images": [<br>                "https://images.printify.com/5d0b831a47045f02006b0b7a.png",<br>                "https://images.printify.com/5ce534113aa847000600d60c.png"<br>            ]<br>        },<br>        {<br>            "id": 429,<br>            "title": "Laptop Sleeve",<br>            "brand": "Generic brand",<br>            "model": "",<br>            "images": [<br>                "https://images.printify.com/5d2325ebce7a9c07c221c926.png",<br>                "https://images.printify.com/5d23233fce7a9c07c105f393.png",<br>                "https://images.printify.com/5d232340ce7a9c07c04f9aa7.png",<br>                "https://images.printify.com/5d23233ece7a9c07c04f9aa3.png"<br>            ]<br>        },<br>        {<br>            "id": 430,<br>            "title": "Pin Buttons",<br>            "brand": "Generic brand",<br>            "model": "",<br>            "images": [<br>                "https://images.printify.com/5cfa4880cf4eed002673c8c2.png",<br>                "https://images.printify.com/5cfa46a8cf4eed00101202d9.png",<br>                "https://images.printify.com/5cfa0db8cf4eed00101202d2.png"<br>            ]<br>        }<br>    ]<br>}` |

### Structure

Structure of Catalog resource with possible transitions between endpoints.

![catalog structure](https://developers.printify.com/images/CatalogStructure-f3350579.png)

## Products

The Product resource lets you list, create, update, delete and publish products to a store.

|     |     |
| --- | --- |
| ℹ | **Embroidery products are supported.**<br> See the [Create a new product](https://developers.printify.com/#create-a-new-product) endpoint for more details. |

|     |     |
| --- | --- |
| ⚠ | All product endpoints require a `{shop_id}` parameter. See [Retrieving Shop ID](https://developers.printify.com/#retrieving-shop-id) for instructions on how to obtain your shop ID. |

On this page:

- [What you can do with the product resource](https://developers.printify.com/#what-you-can-do-with-the-product-resource)
- [Product properties](https://developers.printify.com/#product-properties)
  - [Variant properties](https://developers.printify.com/#product-variant-properties)
  - [Placeholder properties](https://developers.printify.com/#product-placeholder-properties)
  - [Image properties](https://developers.printify.com/#image-properties)
  - [Image Pattern properties](https://developers.printify.com/#image-pattern-properties)
  - [Mock-up image properties](https://developers.printify.com/#mock-up-image-properties)
  - [Publishing properties](https://developers.printify.com/#publishing-properties)
- [Endpoints](https://developers.printify.com/#products-endpoints)
- [Products Structure](https://developers.printify.com/#products-structure)
- [Image positioning](https://developers.printify.com/#image-positioning)
- [Common error cases](https://developers.printify.com/#products-common-error-cases)

### What you can do with the product resource

The Printify Public API lets you do the following with the Product resource:

- [GET /v1/shops/{shop\_id}/products.json](https://developers.printify.com/#retrieve-a-list-of-products)

Retrieve a list of all products
- [GET /v1/shops/{shop\_id}/products/{product\_id}.json](https://developers.printify.com/#retrieve-a-product)

Retrieve a product
- [GET /v1/shops/{shop\_id}/products/{product\_id}/gpsr.json](https://developers.printify.com/#retrieve-product-gpsr-information)

Retrieve a product's GPSR information
- [POST /v1/shops/{shop\_id}/products.json](https://developers.printify.com/#create-a-new-product)

Create a new product
- [PUT /v1/shops/{shop\_id}/products/{product\_id}.json](https://developers.printify.com/#update-a-product)

Update a product
- [DELETE /v1/shops/{shop\_id}/products/{product\_id}.json](https://developers.printify.com/#delete-a-product)

Delete a product
- [POST /v1/shops/{shop\_id}/products/{product\_id}/publish.json](https://developers.printify.com/#publish-a-product)

Publish a product
- [POST /v1/shops/{shop\_id}/products/{product\_id}/publishing\_succeeded.json](https://developers.printify.com/#set-product-publish-status-to-succeeded)

Set product publish status to succeeded
- [POST /v1/shops/{shop\_id}/products/{product\_id}/publishing\_failed.json](https://developers.printify.com/#set-product-publish-status-to-failed)

Set product publish status to failed
- [POST /v1/shops/{shop\_id}/products/{product\_id}/unpublish.json](https://developers.printify.com/#notify-that-a-product-has-been-unpublished)

Notify that a product has been unpublished

### Product properties

|     |     |
| --- | --- |
| id<br> READ-ONLY | `"id": "5cb87a8cd490a2ccb256cec4"`<br> A unique string identifier for the product. Each id is unique across the Printify system. |
| title<br> REQUIRED | `"title": "Product's title"`<br> The name of the product. |
| description<br> REQUIRED | `"description": "Product's description"`<br> A description of the product. Supports HTML formatting for compatible sales channels. |
| safety\_information<br> OPTIONAL | `"safety_information": "GPSR information: John Doe, test@example.com, 123 Main St, Apt 1, New York, NY, 10001, US\nProduct information: Gildan, 5000, 2 year warranty in EU and UK as per Directive 1999/44/EC\nWarnings, Hazzard: No warranty, US\nCare instructions: Machine wash: warm (max 40C or 105F), Non-chlorine: bleach as needed, Tumble dry: medium, Do not iron, Do not dryclean"`<br> Safety information of the product. Can be retrieved using the GPSR endpoint. Supports HTML formatting for compatible sales channels. |
| tags<br> OPTIONAL | `"tags": ["T-shirt", "Men's"]`<br> Tags are also published to sales channel. |
| options<br> READ-ONLY | `"options": [{<br>    "name": "Colors",<br>    "type": "color",<br>    "values": [{<br>        "id": 751,<br>        "title": "Solid White",<br>        "colors": [<br>            "#F9F9F9"<br>        ]<br>    }]<br>}]`<br> Options are read only values and describes product options. There can be up to 3 options for a product. |
| variants<br> REQUIRED | `"variants": [{<br>    "id": 123,<br>    "price": 1000,<br>    "title": "Solid Dark Gray / S",<br>    "sku": "PRY-123",<br>    "grams": 120,<br>    "is_enabled": true,<br>    "is_default": false,<br>    "is_printify_express_eligible": true,<br>    "options": [751, 2]<br>}]<br>`<br> A list of all product variants, each representing a different version of the product. But during product creation, only the variant id and price are necessary. See [variant properties](https://developers.printify.com/#variant-properties) for reference. |
| images<br> READ-ONLY | `"images": [{<br>    "src": "http://example.com/tee.jpg",<br>    "variant_ids": [123, 124],<br>    "position": "front",<br>    "is_default" : false,<br>}]`<br> Mock-up images are read only values. The mock-up images are grouped by variants and position. See [mock-up image properties](https://developers.printify.com/#mock-up-image-properties) for reference. |
| created\_at<br> READ-ONLY | `"created_at": "2017-04-18 13:24:28+00:00"`<br> The date and time when a product was created. |
| update\_at<br> READ-ONLY | `"update_at": "2017-04-18 13:24:28+00:00"`<br> The date and time when a product was last updated. |
| visible<br> READ-ONLY | `"visible": true`<br> Used for publishing. Visibility in sales channel. Can be `true` or `false`, defaults to `true`. |
| blueprint\_id<br> REQUIREDREAD-ONLY | `"blueprint_id": 5`<br> Required when creating a product, but is read only after. See [catalog](https://developers.printify.com/#catalog) for how to get `blueprint_id`. |
| print\_provider\_id<br> REQUIREDREAD-ONLY | `"print_provider_id": 5`<br> Required when creating a product, but is read only after. See [catalog](https://developers.printify.com/#catalog) for how to get `print_provider_id`. |
| user\_id<br> READ-ONLY | `"user_id": 5`<br> User id that a product belongs to. |
| shop\_id<br> READ-ONLY | `"shop_id": 1`<br> Shop id that a product belongs to. |
| print\_areas<br> REQUIRED | `"print_areas": [{<br>    "variant_ids": [123, 124],<br>    "placeholders": [{<br>        "position": "front",<br>        "decoration_method": "dtg",<br>        "images": []<br>    }],<br>}]`<br> All print area properties are required. Each print area specifies the list of variants it applies to.<br> A print area contains placeholders that represent printable locations on the product,<br> such as the front or back of a t-shirt. Each placeholder defines the images<br> to be printed and their positioning within the printable area.<br> See [placeholder properties](https://developers.printify.com/#product-placeholder-properties) for more details. |
| print\_details<br> OPTIONAL | `"print_details": {<br>    "print_on_side": "regular"<br>}`<br> The `print_on_side` property defines the side printing type for canvases.<br> The following values are supported:<br> <br>- `regular` — to extend the print area to the sides of canvas<br>- `mirror` — to keep the original print area and mirror it to the sides<br>- `off` — stop printing on the sides |
| external<br> CONDITIONAL | `"external": [{<br>    "id": "A123abceASd",<br>    "handle": "/path/to/product",<br>    "shipping_template_id": "B123abceASd"<br>}]`<br> Updated by sales channel with publishing succeeded endpoint. Id and handle are external references in the sales channel. See [publishing succeeded](https://developers.printify.com/#set-product-publish-status-to-succeeded) endpoint for more reference.<br> <br> Shipping Template ID is optional and can be passed during product creation or update. |
| is\_locked<br> READ-ONLY | `"is_locked": true`<br> A product is locked during publishing. Locked products can't be updated until unlocked. |
| is\_printify\_express\_eligible<br> READ-ONLY | `"is_printify_express_eligible": true`<br> Flag to indicate if product could be eligible for [Printify Express Delivery](https://help.printify.com/hc/en-us/sections/9116968124689-Printify-Express-Delivery), depending on selection of its variant. |
| is\_economy\_shipping\_eligible<br> READ-ONLY | `"is_economy_shipping_eligible": true`<br> Flag to indicate if product could be eligible for [Economy Shipping](https://help.printify.com/hc/en-us/sections/22109518886161-Economy-Shipping), depending on selection of its variant. |
| is\_printify\_express\_enabled<br> OPTIONAL | `"is_printify_express_enabled": true`<br> Flag to indicate if [Printify Express Delivery](https://help.printify.com/hc/en-us/sections/9116968124689-Printify-Express-Delivery) is enabled for the product. Printify Express Delivery can be enabled only for eligible products (see `is_printify_express_eligible` flag). Defaults to `false`. |
| is\_economy\_shipping\_enabled<br> READ-ONLY | `"is_economy_shipping_enabled": true`<br> Flag to indicate if [Economy Shipping](https://help.printify.com/hc/en-us/sections/22109518886161-Economy-Shipping) is enabled for the product. Economy Shipping can be enabled only for eligible products (see `is_economy_shipping_eligible` flag). Defaults to `false`. |
| sales\_channel\_properties<br> OPTIONAL | Lists product properties specific to the sales channel associated with the product, if the sales channel has such custom properties, the attributes are listed in the object and may be actionable, but for all custom integrations, it will either be null or an empty array.<br> <br>**Amazon**`"sales_channel_properties": {<br>      "free_shipping": false,<br>      "bullet_points": [<br>          "Machine-washable",<br>          "100% cotton"<br>      ],<br>      "no_variation_parent": false,<br>      "brand_name": "Some Amazon approved brand name that has been set on the Printify store"<br>}` **Etsy**`"sales_channel_properties": {<br>      "free_shipping": false,<br>      "personalisation": {<br>          "instructions": "Please provide the name you would like to be printed on the mug",<br>          "buyer_response_limit": 30<br>      }<br>}` **Big Commerce**`"sales_channel_properties": {<br>      "categories": [1, 2, 3],<br>      "free_shipping": false<br>}` **eBay**`"sales_channel_properties": {<br>      "free_shipping": false<br>}` **Shopify**`"sales_channel_properties": {<br>      "collections": ["T-shirts", "Red Clothing"],<br>      "free_shipping": false<br>}` **Squarespace**`"sales_channel_properties": {<br>      "store_page": "https://some-store.squarespace.com"<br>}` **TikTok**`"sales_channel_properties": {<br>      "delivery_service_id": "123",<br>      "warehouse_id": "456",<br>      "free_shipping": false,<br>      "personalisation": "Personalisation instructions"<br>}` |
| views<br> READ-ONLY | `"views": [<br>      {<br>          "id": 34395,<br>          "label": "Front side",<br>          "position": "front",<br>          "files": [<br>              {<br>                  "src": "https://images.printify.com/api/catalog/618e1792f80e2001a840687b.svg",<br>                  "variant_ids": [<br>                      76255<br>                  ]<br>              },<br>          ]<br>      }<br>    ]`<br> Lists blank blueprint images with dedicated print areas. Each view has a label, position, and files source url for a list of variants. |

### Variant properties

|     |     |
| --- | --- |
| id<br> REQUIREDREAD-ONLY | `"id": 123`<br> A unique int identifier for the product variant from the blueprint. Each id is unique across the Printify system. See catalog for instructions on how to get variant ids. |
| sku<br> OPTIONAL | `"sku": "SKU-123"`<br> Optional unique string identifier for the product variant. If one is not provided, one will be generated by Printify. |
| price<br> REQUIRED | `"price": 1000`<br> Price in cents, integer value. |
| cost<br> READ-ONLY | `"cost": 400`<br> Product variant's fulfillment cost in cents, integer value. |
| title<br> READ-ONLY | `"title": "Solid Dark Gray / S"`<br> Variant title. |
| grams<br> READ-ONLY | `"grams": 120`<br> Weight in grams for a product variant |
| is\_enabled<br> OPTIONAL | `"is_enabled": true`<br> Used for publishing, the value is true if one has the variant in question selected as an offering and wants it published. |
| is\_default<br> OPTIONAL | `"is_default": true`<br> Only one variant can be default. Used when publishing to sales channel. Default variant's image will be the title image of the product. |
| is\_available<br> READ-ONLY | `"is_available": true`<br> Actual stock status of the variant, if false, the variant is out of stock and vice versa. |
| is\_printify\_express\_eligible<br> READ-ONLY | `"is_printify_express_eligible": true`<br> Flag to indicate if product's variant is eligible for [Printify Express](https://help.printify.com/hc/en-us/sections/9116968124689-Printify-Express-Delivery) delivery. |
| options<br> READ-ONLY | `"options": [751, 2]`<br> Reference to options by id. |

### Placeholder properties

|     |     |
| --- | --- |
| position<br> REQUIRED | `"position": "front"`<br> Select one of the available positions returned by the<br> [Retrieve a list of variants of a blueprint from a specific print provider](https://developers.printify.com/#retrieve-a-list-of-variants)<br> endpoint. See [blueprint variant properties](https://developers.printify.com/#catalog-variant-properties) for details on retrieving<br> available positions and supported decoration methods for a blueprint and print provider.<br> Each position is associated with a specific decoration method. By selecting a position for your images,<br> you also select the decoration method used for printing. For example, a blueprint may provide multiple<br> front positions, such as `large_center_embroidery` for embroidery or `front_dtf`<br> for the DTF decoration method.<br> When using positions with embroidery, follow the<br> [Embroidery Guide](https://printify.com/guide/embroidery-guide/ "Embroidery Guide")<br> to ensure high-quality results and proper file preparation. |
| decoration\_method<br> READ-ONLY | `"decoration_method": "dtg"`<br> The `decoration_method` property is returned when retrieving product information.<br> Each placeholder is associated with a single decoration method, which is defined by the system<br> and cannot be modified during product creation. To use a specific decoration method, add images<br> to the placeholder that corresponds to the desired decoration method. See `position` for<br> reference. |
| images<br> REQUIRED | `"images": []`<br> Array of images. See [image properties](https://developers.printify.com/#image-properties) for reference. |

### Image properties

|     |     |
| --- | --- |
| id<br> REQUIRED | `"id": 123`<br> See [upload images](https://developers.printify.com/#uploads) for reference on how to upload images and get all needed properties. |
| src<br> READ-ONLY | `"src": https://example.com/5c7665205342af161e1cb26e`<br> Full image source url. |
| name<br> READ-ONLY | `"name": "image.jpg"`<br> Name of an image file. |
| type<br> READ-ONLY | `"type": "image/png"`<br> Type of an image. Valid image types are `image/png`, `image/jpg`, `image/jpeg`. |
| height<br> READ-ONLY | `"height": 100`<br> Float value for image height in pixels. See [upload images](https://developers.printify.com/#uploads) for reference on how to upload images and get all needed properties. |
| width<br> READ-ONLY | `"width": 100`<br> Float value for image width in pixels. See [upload images](https://developers.printify.com/#uploads) for reference on how to upload images and get all needed properties. |
| x<br> REQUIRED | `"x": 100`<br> Float value to position an image on the x axis. See [image positioning](https://developers.printify.com/#image-positioning) for reference on how to position images. |
| y<br> REQUIRED | `"y": 100`<br> Float value to position an image on the y axis. See [image positioning](https://developers.printify.com/#image-positioning) for reference on how to position images. |
| scale<br> REQUIRED | `"scale": 1`<br> Float value to scale image up or down. See [image positioning](https://developers.printify.com/#image-positioning) for reference on how to position images. |
| angle<br> REQUIRED | `"angle": 180`<br> Integer value used to rotate image. See [image positioning](https://developers.printify.com/#image-positioning) for reference on how to position images. |
| pattern<br> OPTIONAL | Object value used to field defines a repeating graphical design applied to a product image. It includes properties to adjust spacing, rotation, and positioning of the pattern. See [image pattern properties](https://developers.printify.com/#image-pattern-properties) |
| font\_family<br> READ-ONLY | `"font_family": "Arial"`<br> Font family used for text layer. |
| font\_size<br> READ-ONLY | `"font_size": 12`<br> Font size used for text layer. |
| font\_weight<br> READ-ONLY | `"font_weight": "bold"`<br> Font weight used for text layer. |
| font\_color<br> READ-ONLY | `"font_color": "#000000"`<br> Font color used for text layer. |
| font\_style<br> READ-ONLY | `"font_style": "italic"`<br> Font style used for text layer. |
| input\_text<br> READ-ONLY | `"input_text": "Hello World"`<br> Text value used for text layer. |
| text\_align<br> READ-ONLY | `"text_align": "left"`<br> Text alignment used for text layer. |

### Image pattern properties

|     |     |
| --- | --- |
| spacing\_x<br> REQUIRED | `"spacing_x": 0.5`<br> Float value. Horizontal Spacing expressed relative to width, where 0.5 would mean the item should repeat each half-width of image, and 1 means no spacing, 1.5 would mean 50% spacing etc. |
| spacing\_y<br> REQUIRED | `"spacing_y": 0.5`<br> Float value. Vertical Spacing expressed relative to height, where 0.5 would mean the item should repeat each half-height of image, and 1 means no spacing, 1.5 would mean 50% spacing etc. |
| angle<br> REQUIRED | `"angle": 0`<br> Float value. Allows changing the axis along which items repeat. 0 means horizontal. Accepts values from -45 to +45 (Because the result of all other angles can already be achieved by staying within this range). |
| offset<br> REQUIRED | `"offset": 0.5`<br> Float value. Allows specifying offset between 2 lines. Setting this to 0.5 will produce a "brick" pattern. Accepts values between -1 and 1. |

### Mock-up image properties

|     |     |
| --- | --- |
| src<br> READ-ONLY | `"src": "https://images.printify.com/mockup/5d39b159e7c48c000728c89f/33719/145/mug-11oz.jpg"`<br> Url of a mock-up image. |
| variant\_ids<br> READ-ONLY | `"variant_ids": [<br>    61618,<br>    61619,<br>    61620,<br>    61621,<br>    61622<br>]`<br> Array of integer ids for variants illustrated by the mock-up image. |
| position<br> READ-ONLY | `"position": "front"`<br> Camera position of a mockup (i.e. what part of the product is being displayed). |
| is\_default<br> READ-ONLY | `"is_default": true`<br> Used by the sales channel. If set to `true`, The specific mockup is the title image. Can be used to decide the first image displayed when a product's page is accessed. |

### Publishing properties

The "publish" button in the Printify app only locks the product on the Printify app and triggers the product:publish:started event if you are subscribed to it, see See [Product events](https://developers.printify.com/#product-events) for reference. To publish a product, you need to create it manually on your store from the data you can obtain from the product resource or develop a system to automate that. Once done, you can use the [Publish succeeded endpoint](https://developers.printify.com/#set-product-publish-status-to-succeeded) or [Publish failed endpoint](https://developers.printify.com/#set-product-publish-status-to-failed) to unlock the product.

|     |     |
| --- | --- |
| images<br> REQUIRED | `"images": true`<br> Used by the sales channel. If set to `false`, Images will not be published, and existing images will be used instead. |
| variants<br> REQUIRED | `"variants": true`<br> Used by the sales channel. If set to `false`, product variations will not be published. |
| title<br> REQUIRED | `"title": true`<br> Used by sales channel. If set to `false`, product title will not be updated. |
| description<br> REQUIRED | `"description": true`<br> Used by sales channel. If set to `false`, product description will not be updated. |
| tags<br> REQUIRED | `"tags": true`<br> Used by sales channel. If set to `false`, product tags will not be updated. |
| shipping\_template<br> OPTIONAL | `"shipping_template": true`<br> Used by Etsy and Amazon sales channels only. If set to `false`, product shipping template will not be updated. |

### Endpoints

### Retrieve a list of products

|     |     |
| --- | --- |
| GET | /v1/shops/{shop\_id}/products.json |
| limit<br> OPTIONAL | Results per page<br>(default: 10, maximum: 50) |
| page<br> OPTIONAL | Paginate through list of results |
| **Retrieve all products**<br>`GET /v1/shops/{shop_id}/products.json`<br>[View Response](https://developers.printify.com/#)`{<br>    "current_page": 1,<br>    "data": [<br>        {<br>            "id": "5d39b159e7c48c000728c89f",<br>            "title": "Mug 11oz",<br>            "description": "Perfect for coffee, tea and hot chocolate, this classic shape white, durable<br>            ceramic mug in the most popular size. High quality sublimation printing makes it an<br>            appreciated gift to every true hot beverage lover.Perfect for coffee, tea and hot<br>            chocolate, this classic shape white, durable ceramic mug in the most popular size.<br>            High quality sublimation printing makes it an appreciated gift to every true hot beverage lover.<br>            .: White ceramic<br>            .: 11 oz (0.33 l)<br>            .: Rounded corners<br>            .: C-Handle",<br>            "safety_information": "GPSR information: John Doe, test@example.com, 123 Main St, Apt 1, New York, NY, 10001, US<br>            Product information: Gildan, 5000, 2 year warranty in EU and UK as per Directive 1999/44/EC<br>            Warnings, Hazzard: No warranty, US<br>            Care instructions: Machine wash: warm (max 40C or 105F), Non-chlorine: bleach as needed, Tumble dry: medium, Do not iron, Do not dryclean",<br>            "tags": [<br>                "Home & Living",<br>                "Mugs",<br>                "11 oz",<br>                "White base",<br>                "Sublimation"<br>            ],<br>            "options": [<br>                {<br>                    "name": "Sizes",<br>                    "type": "size",<br>                    "values": [<br>                        {<br>                            "id": 1189,<br>                            "title": "11oz"<br>                        }<br>                    ]<br>                }<br>            ],<br>            "variants": [<br>                {<br>                    "id": 33719,<br>                    "sku": "866366009",<br>                    "cost": 516,<br>                    "price": 860,<br>                    "title": "11oz",<br>                    "grams": 460,<br>                    "is_enabled": true,<br>                    "is_default": true,<br>                    "is_available": true,<br>                    "is_printify_express_eligible": true,<br>                    "options": [<br>                        1189<br>                    ]<br>                }<br>            ],<br>            "images": [<br>                {<br>                    "src": "https://images.printify.com/mockup/5d39b159e7c48c000728c89f/33719/145/mug-11oz.jpg",<br>                    "variant_ids": [<br>                        33719<br>                    ],<br>                    "position": "front",<br>                    "is_default": false<br>                },<br>                {<br>                    "src": "https://images.printify.com/mockup/5d39b159e7c48c000728c89f/33719/146/mug-11oz.jpg",<br>                    "variant_ids": [<br>                        33719<br>                    ],<br>                    "position": "other",<br>                    "is_default": false<br>                },<br>                {<br>                    "src": "https://images.printify.com/mockup/5d39b159e7c48c000728c89f/33719/147/mug-11oz.jpg",<br>                    "variant_ids": [<br>                        33719<br>                    ],<br>                    "position": "other",<br>                    "is_default": true<br>                }<br>            ],<br>            "created_at": "2019-07-25 13:40:41+00:00",<br>            "updated_at": "2019-07-25 13:40:59+00:00",<br>            "visible": true,<br>            "is_locked": false,<br>            "is_printify_express_eligible": true,<br>            "is_printify_express_enabled": true,<br>            "is_economy_shipping_eligible": true,<br>            "is_economy_shipping_enabled": true,<br>            "blueprint_id": 68,<br>            "user_id": 1337,<br>            "shop_id": 1337,<br>            "print_provider_id": 9,<br>            "print_areas": [<br>                {<br>                    "variant_ids": [<br>                        33719<br>                    ],<br>                    "placeholders": [<br>                        {<br>                            "position": "front",<br>                            "images": [<br>                                {<br>                                    "id": "5c7665205342af161e1cb26e",<br>                                    "src": "https://image-storage.example.com/5d39b159e7c48c000728c89f",<br>                                    "name": "Test.png",<br>                                    "type": "image/png",<br>                                    "height": 5850,<br>                                    "width": 4350,<br>                                    "x": 0.5,<br>                                    "y": 0.5,<br>                                    "scale": 1.01,<br>                                    "angle": 0<br>                                }<br>                            ]<br>                        }<br>                    ],<br>                    "background": "#ffffff"<br>                }<br>            ],<br>            "views": [<br>                {<br>                    "id": 34395,<br>                    "label": "Front side",<br>                    "position": "front",<br>                    "files": [<br>                        {<br>                            "src": "https://images.printify.com/api/catalog/618e1792f80e2001a840687b.svg",<br>                            "variant_ids": [<br>                                33719<br>                            ]<br>                        },<br>                    ]<br>                }<br>            ],<br>            "sales_channel_properties": []<br>        }<br>    ],<br>    "first_page_url": "/?page=1",<br>    "from": 1,<br>    "last_page": 22,<br>    "last_page_url": "/?page=22",<br>    "next_page_url": "/?page=2",<br>    "path": "/",<br>    "per_page": 1,<br>    "prev_page_url": null,<br>    "to": 1,<br>    "total": 22<br>}` |
| **Retrieve specific page from results**<br>`GET /v1/shops/{shop_id}/products.json?page=2`<br>[View Response](https://developers.printify.com/#)`{<br>    "current_page": 2,<br>    "data": [<br>        {<br>             "id": "5d39b159e7c48c000728c89f",<br>             "title": "Mug 11oz",<br>             "description": "Perfect for coffee, tea and hot chocolate, this classic shape white, durable<br>            ceramic mug in the most popular size. High quality sublimation printing makes it an<br>            appreciated gift to every true hot beverage lover.Perfect for coffee, tea and hot<br>            chocolate, this classic shape white, durable ceramic mug in the most popular size.<br>            High quality sublimation printing makes it an appreciated gift to every true hot beverage lover.<br>            .: White ceramic<br>            .: 11 oz (0.33 l)<br>            .: Rounded corners<br>            .: C-Handle",<br>            "safety_information": "GPSR information: John Doe, test@example.com, 123 Main St, Apt 1, New York, NY, 10001, US<br>            Product information: Gildan, 5000, 2 year warranty in EU and UK as per Directive 1999/44/EC<br>            Warnings, Hazzard: No warranty, US<br>            Care instructions: Machine wash: warm (max 40C or 105F), Non-chlorine: bleach as needed, Tumble dry: medium, Do not iron, Do not dryclean",<br>             "tags": [<br>                 "Home & Living",<br>                 "Mugs",<br>                 "11 oz",<br>                 "White base",<br>                 "Sublimation"<br>             ],<br>             "options": [<br>                 {<br>                     "name": "Sizes",<br>                     "type": "size",<br>                     "values": [<br>                         {<br>                             "id": 1189,<br>                             "title": "11oz"<br>                         }<br>                     ]<br>                 }<br>             ],<br>             "variants": [<br>                 {<br>                     "id": 33719,<br>                     "sku": "866366009",<br>                     "cost": 516,<br>                     "price": 860,<br>                     "title": "11oz",<br>                     "grams": 460,<br>                     "is_enabled": true,<br>                     "is_default": true,<br>                     "is_available": true,<br>                     "is_printify_express_eligible": true,<br>                     "options": [<br>                         1189<br>                     ]<br>                 }<br>             ],<br>             "images": [<br>                 {<br>                     "src": "https://images.printify.com/mockup/5d39b159e7c48c000728c89f/33719/145/mug-11oz.jpg",<br>                     "variant_ids": [<br>                         33719<br>                     ],<br>                     "position": "front",<br>                     "is_default": false<br>                 },<br>                 {<br>                     "src": "https://images.printify.com/mockup/5d39b159e7c48c000728c89f/33719/146/mug-11oz.jpg",<br>                     "variant_ids": [<br>                         33719<br>                     ],<br>                     "position": "other",<br>                     "is_default": false<br>                 },<br>                 {<br>                     "src": "https://images.printify.com/mockup/5d39b159e7c48c000728c89f/33719/147/mug-11oz.jpg",<br>                     "variant_ids": [<br>                         33719<br>                     ],<br>                     "position": "other",<br>                     "is_default": true<br>                 }<br>             ],<br>             "created_at": "2019-07-25 13:40:41+00:00",<br>             "updated_at": "2019-07-25 13:40:59+00:00",<br>             "visible": true,<br>             "is_locked": false,<br>             "is_printify_express_eligible": true,<br>             "is_printify_express_enabled": true,<br>             "is_economy_shipping_eligible": true,<br>             "is_economy_shipping_enabled": true,<br>             "blueprint_id": 68,<br>             "user_id": 1337,<br>             "shop_id": 1337,<br>             "print_provider_id": 9,<br>             "print_areas": [<br>                 {<br>                     "variant_ids": [<br>                         33719<br>                     ],<br>                     "placeholders": [<br>                         {<br>                             "position": "front",<br>                             "images": [<br>                                 {<br>                                     "id": "5c7665205342af161e1cb26e",<br>                                     "src": "https://image-storage.example.com/5d39b159e7c48c000728c89f",<br>                                     "name": "Test.png",<br>                                     "type": "image/png",<br>                                     "height": 5850,<br>                                     "width": 4350,<br>                                     "x": 0.5,<br>                                     "y": 0.5,<br>                                     "scale": 1.01,<br>                                     "angle": 0<br>                                 }<br>                             ]<br>                         }<br>                     ],<br>                     "background": "#ffffff"<br>                 }<br>             ],<br>             "views": [<br>                 {<br>                     "id": 34395,<br>                     "label": "Front side",<br>                     "position": "front",<br>                     "files": [<br>                         {<br>                             "src": "https://images.printify.com/api/catalog/618e1792f80e2001a840687b.svg",<br>                             "variant_ids": [<br>                                 33719<br>                             ]<br>                         },<br>                     ]<br>                 }<br>             ],<br>             "sales_channel_properties": []<br>        }<br>    ],<br>    "first_page_url": "/?page=1",<br>    "from": 2,<br>    "last_page": 22,<br>    "last_page_url": "/?page=22",<br>    "next_page_url": "/?page=3",<br>    "path": "/",<br>    "per_page": 1,<br>    "prev_page_url": "/?page=1",<br>    "to": 2,<br>    "total": 22<br>}` |
| **Retrieve limited results**<br>`GET /v1/shops/{shop_id}/products.json?limit=1`<br>[View Response](https://developers.printify.com/#)`{<br>    "current_page": 1,<br>    "data": [<br>        {<br>             "id": "5d39b159e7c48c000728c89f",<br>             "title": "Mug 11oz",<br>             "description": "Perfect for coffee, tea and hot chocolate, this classic shape white, durable<br>            ceramic mug in the most popular size. High quality sublimation printing makes it an<br>            appreciated gift to every true hot beverage lover.Perfect for coffee, tea and hot<br>            chocolate, this classic shape white, durable ceramic mug in the most popular size.<br>            High quality sublimation printing makes it an appreciated gift to every true hot beverage lover.<br>            .: White ceramic<br>            .: 11 oz (0.33 l)<br>            .: Rounded corners<br>            .: C-Handle",<br>            "safety_information": "GPSR information: John Doe, test@example.com, 123 Main St, Apt 1, New York, NY, 10001, US<br>            Product information: Gildan, 5000, 2 year warranty in EU and UK as per Directive 1999/44/EC<br>            Warnings, Hazzard: No warranty, US<br>            Care instructions: Machine wash: warm (max 40C or 105F), Non-chlorine: bleach as needed, Tumble dry: medium, Do not iron, Do not dryclean",<br>             "tags": [<br>                 "Home & Living",<br>                 "Mugs",<br>                 "11 oz",<br>                 "White base",<br>                 "Sublimation"<br>             ],<br>             "options": [<br>                 {<br>                     "name": "Sizes",<br>                     "type": "size",<br>                     "values": [<br>                         {<br>                             "id": 1189,<br>                             "title": "11oz"<br>                         }<br>                     ]<br>                 }<br>             ],<br>             "variants": [<br>                 {<br>                     "id": 33719,<br>                     "sku": "866366009",<br>                     "cost": 516,<br>                     "price": 860,<br>                     "title": "11oz",<br>                     "grams": 460,<br>                     "is_enabled": true,<br>                     "is_default": true,<br>                     "is_available": true,<br>                     "is_printify_express_eligible": true,<br>                     "options": [<br>                         1189<br>                     ]<br>                 }<br>             ],<br>             "images": [<br>                 {<br>                     "src": "https://images.printify.com/mockup/5d39b159e7c48c000728c89f/33719/145/mug-11oz.jpg",<br>                     "variant_ids": [<br>                         33719<br>                     ],<br>                     "position": "front",<br>                     "is_default": false<br>                 },<br>                 {<br>                     "src": "https://images.printify.com/mockup/5d39b159e7c48c000728c89f/33719/146/mug-11oz.jpg",<br>                     "variant_ids": [<br>                         33719<br>                     ],<br>                     "position": "other",<br>                     "is_default": false<br>                 },<br>                 {<br>                     "src": "https://images.printify.com/mockup/5d39b159e7c48c000728c89f/33719/147/mug-11oz.jpg",<br>                     "variant_ids": [<br>                         33719<br>                     ],<br>                     "position": "other",<br>                     "is_default": true<br>                 }<br>             ],<br>             "created_at": "2019-07-25 13:40:41+00:00",<br>             "updated_at": "2019-07-25 13:40:59+00:00",<br>             "visible": true,<br>             "is_locked": false,<br>             "is_printify_express_eligible": true,<br>             "is_printify_express_enabled": true,<br>             "is_economy_shipping_eligible": true,<br>             "is_economy_shipping_enabled": true,<br>             "blueprint_id": 68,<br>             "user_id": 1337,<br>             "shop_id": 1337,<br>             "print_provider_id": 9,<br>             "print_areas": [<br>                 {<br>                     "variant_ids": [<br>                         33719<br>                     ],<br>                     "placeholders": [<br>                         {<br>                             "position": "front",<br>                             "images": [<br>                                 {<br>                                     "id": "5c7665205342af161e1cb26e",<br>                                     "src": "https://image-storage.example.com/5d39b159e7c48c000728c89f",<br>                                     "name": "Test.png",<br>                                     "type": "image/png",<br>                                     "height": 5850,<br>                                     "width": 4350,<br>                                     "x": 0.5,<br>                                     "y": 0.5,<br>                                     "scale": 1.01,<br>                                     "angle": 0<br>                                 }<br>                             ]<br>                         }<br>                     ],<br>                     "background": "#ffffff"<br>                 }<br>             ],<br>             "views": [<br>                 {<br>                     "id": 34395,<br>                     "label": "Front side",<br>                     "position": "front",<br>                     "files": [<br>                         {<br>                             "src": "https://images.printify.com/api/catalog/618e1792f80e2001a840687b.svg",<br>                             "variant_ids": [<br>                                 33719<br>                             ]<br>                         },<br>                     ]<br>                 }<br>             ],<br>             "sales_channel_properties": []<br>        }<br>    ],<br>    "first_page_url": "/?page=1",<br>     "from": 1,<br>     "last_page": 10,<br>     "last_page_url": "/?page=10",<br>     "next_page_url": "/?page=2",<br>     "path": "/",<br>     "per_page": 1,<br>     "prev_page_url": null,<br>     "to": 1,<br>     "total": 10<br>}` |

#### Retrieve a product

|     |     |
| --- | --- |
| GET | /v1/shops/{shop\_id}/products/{product\_id}.json |
| **Retrieve a product**<br>`GET /v1/shops/{shop_id}/products/{product_id}.json`<br>[View Response](https://developers.printify.com/#)`{<br>    "id": "5d39b159e7c48c000728c89f",<br>       "title": "Mug 11oz",<br>       "description": "Perfect for coffee, tea and hot chocolate, this classic shape white, durable<br>        ceramic mug in the most popular size. High quality sublimation printing makes it an<br>        appreciated gift to every true hot beverage lover.Perfect for coffee, tea and hot<br>        chocolate, this classic shape white, durable ceramic mug in the most popular size.<br>        High quality sublimation printing makes it an appreciated gift to every true hot beverage lover.<br>        .: White ceramic<br>        .: 11 oz (0.33 l)<br>        .: Rounded corners<br>        .: C-Handle",<br>        "safety_information": "GPSR information: John Doe, test@example.com, 123 Main St, Apt 1, New York, NY, 10001, US<br>        Product information: Gildan, 5000, 2 year warranty in EU and UK as per Directive 1999/44/EC<br>        Warnings, Hazzard: No warranty, US<br>        Care instructions: Machine wash: warm (max 40C or 105F), Non-chlorine: bleach as needed, Tumble dry: medium, Do not iron, Do not dryclean",<br>       "tags": [<br>           "Home & Living",<br>           "Mugs",<br>           "11 oz",<br>           "White base",<br>           "Sublimation"<br>       ],<br>       "options": [<br>           {<br>               "name": "Sizes",<br>               "type": "size",<br>               "values": [<br>                   {<br>                       "id": 1189,<br>                       "title": "11oz"<br>                   }<br>               ]<br>           }<br>       ],<br>       "variants": [<br>           {<br>               "id": 33719,<br>               "sku": "866366009",<br>               "cost": 516,<br>               "price": 860,<br>               "title": "11oz",<br>               "grams": 460,<br>               "is_enabled": true,<br>               "is_default": true,<br>               "is_available": true,<br>               "is_printify_express_eligible": true,<br>               "options": [<br>                   1189<br>               ]<br>           }<br>       ],<br>       "images": [<br>           {<br>               "src": "https://images.printify.com/mockup/5d39b159e7c48c000728c89f/33719/145/mug-11oz.jpg",<br>               "variant_ids": [<br>                   33719<br>               ],<br>               "position": "front",<br>               "is_default": false<br>           },<br>           {<br>               "src": "https://images.printify.com/mockup/5d39b159e7c48c000728c89f/33719/146/mug-11oz.jpg",<br>               "variant_ids": [<br>                   33719<br>               ],<br>               "position": "other",<br>               "is_default": false<br>           },<br>           {<br>               "src": "https://images.printify.com/mockup/5d39b159e7c48c000728c89f/33719/147/mug-11oz.jpg",<br>               "variant_ids": [<br>                   33719<br>               ],<br>               "position": "other",<br>               "is_default": true<br>           }<br>       ],<br>       "created_at": "2019-07-25 13:40:41+00:00",<br>       "updated_at": "2019-07-25 13:40:59+00:00",<br>       "visible": true,<br>       "is_locked": false,<br>       "is_printify_express_eligible": true,<br>       "is_printify_express_enabled": true,<br>       "is_economy_shipping_eligible": true,<br>       "is_economy_shipping_enabled": true,<br>       "blueprint_id": 68,<br>       "user_id": 1337,<br>       "shop_id": 1337,<br>       "print_provider_id": 9,<br>       "print_areas": [<br>           {<br>               "variant_ids": [<br>                   33719<br>               ],<br>               "placeholders": [<br>                   {<br>                       "position": "front",<br>                       "images": [<br>                           {<br>                               "id": "5c7665205342af161e1cb26e",<br>                               "name": "Test.png",<br>                               "type": "image/png",<br>                               "height": 5850,<br>                               "width": 4350,<br>                               "x": 0.5,<br>                               "y": 0.5,<br>                               "scale": 1.01,<br>                               "angle": 0,<br>                               "src": "https://image-storage.example.com/5d39b159e7c48c000728c89f"<br>                           },<br>                           {<br>                               "id": "0bd183ab-7bd0-e327-8329-7f77ee2a3f51",<br>                               "name": "",<br>                               "type": "text/svg",<br>                               "height": 1,<br>                               "width": 1,<br>                               "x": 0.5,<br>                               "y": 0.5000090815098948,<br>                               "scale": 0.7444,<br>                               "angle": 345,<br>                               "font_family": "ABeeZee",<br>                               "font_size": 200,<br>                               "font_weight": 400,<br>                               "font_color": "#ffffff",<br>                               "font_style": "normal",<br>                               "input_text": "Text example",<br>                               "text_align": "left"<br>                           }<br>                       ]<br>                   }<br>               ],<br>               "background": "#ffffff"<br>           }<br>       ],<br>       "views": [<br>           {<br>               "id": 34395,<br>               "label": "Front side",<br>               "position": "front",<br>               "files": [<br>                   {<br>                       "src": "https://images.printify.com/api/catalog/618e1792f80e2001a840687b.svg",<br>                       "variant_ids": [<br>                           33719<br>                       ]<br>                   },<br>               ]<br>           }<br>       ],<br>       "sales_channel_properties": []<br>}` |

#### Retrieve product GPSR information

|     |     |
| --- | --- |
| GET | /v1/shops/{shop\_id}/products/{product\_id}/gpsr.json |
| **Retrieve a product's GPSR information**<br>`GET /v1/shops/{shop_id}/products/{product_id}/gpsr.json`<br>[View Response](https://developers.printify.com/#)`[<br>    {<br>        "title": "GPSR information",<br>        "text": "John Doe, test@example.com, 123 Main St, Apt 1, New York, NY, 10001, US"<br>    },<br>    {<br>        "title": "Product information",<br>        "text": "Gildan, 5000, 2 year warranty in EU and UK as per Directive 1999/44/EC"<br>    },<br>    {<br>        "title": "Warnings, Hazzard",<br>        "text": "No warranty, US"<br>    },<br>    {<br>        "title": "Care instructions",<br>        "text": "Machine wash: warm (max 40C or 105F), Non-chlorine: bleach as needed, Tumble dry: medium, Do not iron, Do not dryclean"<br>    }<br>]` |

#### Create a new product

|     |     |
| --- | --- |
| ⚠ | **Embroidery is supported.** To create an embroidery product, choose one of the<br> [embroidery products](https://printify.com/app/products/embroidery) available in the catalog.<br> Confirm that embroidery is supported for the selected blueprint variant and print provider using the<br> [Retrieve a list of variants of a blueprint from a specific print provider](https://developers.printify.com/#retrieve-a-list-of-variants)<br> endpoint.<br> See [blueprint variant properties](https://developers.printify.com/#catalog-variant-properties) to check available positions<br> and supported decoration methods, and [product placeholder properties](https://developers.printify.com/#product-placeholder-properties)<br> to learn how to use positions when creating a product with embroidery.<br> For best results, follow the<br> [Embroidery Guide](https://printify.com/guide/embroidery-guide/ "Embroidery Guide")<br> to ensure proper file preparation and high-quality embroidery output. |

|     |     |
| --- | --- |
| POST | /v1/shops/{shop\_id}/products.json |
| **Create a new product**<br>`POST /v1/shops/{shop_id}/products.json`<br>`{<br>    "title": "Product",<br>    "description": "Good product",<br>    "safety_information": "GPSR information: John Doe, test@example.com, 123 Main St, Apt 1, New York, NY, 10001, US<br>    Product information: Gildan, 5000, 2 year warranty in EU and UK as per Directive 1999/44/EC<br>    Warnings, Hazzard: No warranty, US<br>    Care instructions: Machine wash: warm (max 40C or 105F), Non-chlorine: bleach as needed, Tumble dry: medium, Do not iron, Do not dryclean",<br>    "blueprint_id": 384,<br>    "print_provider_id": 1,<br>    "variants": [<br>          {<br>              "id": 45740,<br>              "price": 400,<br>              "is_enabled": true<br>          },<br>          {<br>              "id": 45742,<br>              "price": 400,<br>              "is_enabled": true<br>          },<br>          {<br>              "id": 45744,<br>              "price": 400,<br>              "is_enabled": false<br>          },<br>          {<br>              "id": 45746,<br>              "price": 400,<br>              "is_enabled": false<br>          }<br>      ],<br>      "print_areas": [<br>        {<br>          "variant_ids": [45740,45742,45744,45746],<br>          "placeholders": [<br>            {<br>              "position": "front",<br>              "images": [<br>                  {<br>                    "id": "5d15ca551163cde90d7b2203",<br>                    "x": 0.5,<br>                    "y": 0.5,<br>                    "scale": 1,<br>                    "angle": 0,<br>                    "pattern": {<br>                      "spacing_x": 1,<br>                      "spacing_y": 2,<br>                      "scale": 3,<br>                      "offset": 4<br>                    }<br>                  }<br>              ]<br>            }<br>          ]<br>        }<br>      ]<br>  }<br>` [View Response](https://developers.printify.com/#)`{<br>     "id": "5d39b411749d0a000f30e0f4",<br>     "title": "Product",<br>     "description": "Good product",<br>     "safety_information": "GPSR information: John Doe, test@example.com, 123 Main St, Apt 1, New York, NY, 10001, US<br>     Product information: Gildan, 5000, 2 year warranty in EU and UK as per Directive 1999/44/EC<br>     Warnings, Hazzard: No warranty, US<br>     Care instructions: Machine wash: warm (max 40C or 105F), Non-chlorine: bleach as needed, Tumble dry: medium, Do not iron, Do not dryclean",<br>     "tags": [<br>         "Home & Living",<br>         "Stickers"<br>     ],<br>     "options": [<br>         {<br>             "name": "Size",<br>             "type": "size",<br>             "values": [<br>                 {<br>                     "id": 2017,<br>                     "title": "2x2\""<br>                 },<br>                 {<br>                     "id": 2018,<br>                     "title": "3x3\""<br>                 },<br>                 {<br>                     "id": 2019,<br>                     "title": "4x4\""<br>                 },<br>                 {<br>                     "id": 2020,<br>                     "title": "6x6\""<br>                 }<br>             ]<br>         },<br>         {<br>             "name": "Type",<br>             "type": "surface",<br>             "values": [<br>                 {<br>                     "id": 2114,<br>                     "title": "White"<br>                 }<br>             ]<br>         }<br>     ],<br>     "variants": [<br>         {<br>             "id": 45740,<br>             "sku": "866375988",<br>             "cost": 134,<br>             "price": 400,<br>             "title": "2x2\" / White",<br>             "grams": 10,<br>             "is_enabled": true,<br>             "is_default": true,<br>             "is_available": true,<br>             "is_printify_express_eligible": true,<br>             "options": [<br>                 2017,<br>                 2114<br>             ]<br>         },<br>         {<br>             "id": 45742,<br>             "sku": "866375989",<br>             "cost": 149,<br>             "price": 400,<br>             "title": "3x3\" / White",<br>             "grams": 10,<br>             "is_enabled": true,<br>             "is_default": false,<br>             "is_available": true,<br>             "is_printify_express_eligible": true,<br>             "options": [<br>                 2018,<br>                 2114<br>             ]<br>         },<br>         {<br>             "id": 45744,<br>             "sku": "866375990",<br>             "cost": 187,<br>             "price": 400,<br>             "title": "4x4\" / White",<br>             "grams": 10,<br>             "is_enabled": true,<br>             "is_default": false,<br>             "is_available": true,<br>             "is_printify_express_eligible": true,<br>             "options": [<br>                 2019,<br>                 2114<br>             ]<br>         },<br>         {<br>             "id": 45746,<br>             "sku": "866375991",<br>             "cost": 216,<br>             "price": 400,<br>             "title": "6x6\" / White",<br>             "grams": 10,<br>             "is_enabled": true,<br>             "is_default": false,<br>             "is_available": true,<br>             "is_printify_express_eligible": true,<br>             "options": [<br>                 2020,<br>                 2114<br>             ]<br>         }<br>     ],<br>     "images": [<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45740/2187/product.jpg",<br>             "variant_ids": [<br>                 45740<br>             ],<br>             "position": "front",<br>             "is_default": true<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45740/2188/product.jpg",<br>             "variant_ids": [<br>                 45740<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45740/2189/product.jpg",<br>             "variant_ids": [<br>                 45740<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45740/2190/product.jpg",<br>             "variant_ids": [<br>                 45740<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45740/2191/product.jpg",<br>             "variant_ids": [<br>                 45740<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45740/2192/product.jpg",<br>             "variant_ids": [<br>                 45740<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45740/2193/product.jpg",<br>             "variant_ids": [<br>                 45740<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45740/2194/product.jpg",<br>             "variant_ids": [<br>                 45740<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45740/2195/product.jpg",<br>             "variant_ids": [<br>                 45740<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45740/2196/product.jpg",<br>             "variant_ids": [<br>                 45740<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45740/2197/product.jpg",<br>             "variant_ids": [<br>                 45740<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45740/2198/product.jpg",<br>             "variant_ids": [<br>                 45740<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45740/2199/product.jpg",<br>             "variant_ids": [<br>                 45740<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45740/2200/product.jpg",<br>             "variant_ids": [<br>                 45740<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45740/2201/product.jpg",<br>             "variant_ids": [<br>                 45740<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45740/2202/product.jpg",<br>             "variant_ids": [<br>                 45740<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45742/2187/product.jpg",<br>             "variant_ids": [<br>                 45742<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45742/2188/product.jpg",<br>             "variant_ids": [<br>                 45742<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45742/2189/product.jpg",<br>             "variant_ids": [<br>                 45742<br>             ],<br>             "position": "front",<br>             "is_default": true<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45742/2190/product.jpg",<br>             "variant_ids": [<br>                 45742<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45742/2191/product.jpg",<br>             "variant_ids": [<br>                 45742<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45742/2192/product.jpg",<br>             "variant_ids": [<br>                 45742<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45742/2193/product.jpg",<br>             "variant_ids": [<br>                 45742<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45742/2194/product.jpg",<br>             "variant_ids": [<br>                 45742<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45742/2195/product.jpg",<br>             "variant_ids": [<br>                 45742<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45742/2196/product.jpg",<br>             "variant_ids": [<br>                 45742<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45742/2197/product.jpg",<br>             "variant_ids": [<br>                 45742<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45742/2198/product.jpg",<br>             "variant_ids": [<br>                 45742<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45742/2199/product.jpg",<br>             "variant_ids": [<br>                 45742<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45742/2200/product.jpg",<br>             "variant_ids": [<br>                 45742<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45742/2201/product.jpg",<br>             "variant_ids": [<br>                 45742<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45742/2202/product.jpg",<br>             "variant_ids": [<br>                 45742<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45744/2187/product.jpg",<br>             "variant_ids": [<br>                 45744<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45744/2188/product.jpg",<br>             "variant_ids": [<br>                 45744<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45744/2189/product.jpg",<br>             "variant_ids": [<br>                 45744<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45744/2190/product.jpg",<br>             "variant_ids": [<br>                 45744<br>             ],<br>             "position": "front",<br>             "is_default": true<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45744/2191/product.jpg",<br>             "variant_ids": [<br>                 45744<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45744/2192/product.jpg",<br>             "variant_ids": [<br>                 45744<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45744/2193/product.jpg",<br>             "variant_ids": [<br>                 45744<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45744/2194/product.jpg",<br>             "variant_ids": [<br>                 45744<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45744/2195/product.jpg",<br>             "variant_ids": [<br>                 45744<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45744/2196/product.jpg",<br>             "variant_ids": [<br>                 45744<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45744/2197/product.jpg",<br>             "variant_ids": [<br>                 45744<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45744/2198/product.jpg",<br>             "variant_ids": [<br>                 45744<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45744/2199/product.jpg",<br>             "variant_ids": [<br>                 45744<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45744/2200/product.jpg",<br>             "variant_ids": [<br>                 45744<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45744/2201/product.jpg",<br>             "variant_ids": [<br>                 45744<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45744/2202/product.jpg",<br>             "variant_ids": [<br>                 45744<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45746/2187/product.jpg",<br>             "variant_ids": [<br>                 45746<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45746/2188/product.jpg",<br>             "variant_ids": [<br>                 45746<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45746/2189/product.jpg",<br>             "variant_ids": [<br>                 45746<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45746/2190/product.jpg",<br>             "variant_ids": [<br>                 45746<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45746/2191/product.jpg",<br>             "variant_ids": [<br>                 45746<br>             ],<br>             "position": "front",<br>             "is_default": true<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45746/2192/product.jpg",<br>             "variant_ids": [<br>                 45746<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45746/2193/product.jpg",<br>             "variant_ids": [<br>                 45746<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45746/2194/product.jpg",<br>             "variant_ids": [<br>                 45746<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45746/2195/product.jpg",<br>             "variant_ids": [<br>                 45746<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45746/2196/product.jpg",<br>             "variant_ids": [<br>                 45746<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45746/2197/product.jpg",<br>             "variant_ids": [<br>                 45746<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45746/2198/product.jpg",<br>             "variant_ids": [<br>                 45746<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45746/2199/product.jpg",<br>             "variant_ids": [<br>                 45746<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45746/2200/product.jpg",<br>             "variant_ids": [<br>                 45746<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45746/2201/product.jpg",<br>             "variant_ids": [<br>                 45746<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45746/2202/product.jpg",<br>             "variant_ids": [<br>                 45746<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         }<br>     ],<br>     "created_at": "2019-07-25 13:52:17+00:00",<br>     "updated_at": "2019-07-25 13:52:18+00:00",<br>     "visible": true,<br>     "is_locked": false,<br>     "is_printify_express_eligible": true,<br>     "is_printify_express_enabled": true,<br>     "is_economy_shipping_eligible": true,<br>     "is_economy_shipping_enabled": true,<br>     "blueprint_id": 384,<br>     "user_id": 1337,<br>     "shop_id": 1337,<br>     "print_provider_id": 1,<br>     "print_areas": [<br>         {<br>             "variant_ids": [<br>                 45740,<br>                 45742,<br>                 45744,<br>                 45746<br>             ],<br>             "placeholders": [<br>                 {<br>                     "position": "front",<br>                     "decoration_method": "dtg",<br>                     "images": [<br>                         {<br>                             "id": "5d15ca551163cde90d7b2203",<br>                             "src": "https://image-storage.example.com/5d39b159e7c48c000728c89f",<br>                             "name": "Asset 65@3x.png",<br>                             "type": "image/png",<br>                             "height": 1200,<br>                             "width": 1200,<br>                             "x": 0.5,<br>                             "y": 0.5,<br>                             "scale": 1,<br>                             "angle": 0<br>                         }<br>                     ]<br>                 }<br>             ],<br>             "background": "#ffffff"<br>         }<br>     ],<br>     "views": [<br>           {<br>               "id": 34395,<br>               "label": "Front side",<br>               "position": "front",<br>               "files": [<br>                   {<br>                       "src": "https://images.printify.com/api/catalog/618e1792f80e2001a840687b.svg",<br>                       "variant_ids": [<br>                           45740,<br>                           45742,<br>                           45744,<br>                           45746<br>                       ]<br>                   },<br>               ]<br>           }<br>     ],<br>     "sales_channel_properties": []<br>  }` |

#### Update a product

A product can be updated partially or as a whole document. When updating variants, all variants must be present in the request.

|     |     |
| --- | --- |
| PUT | /v1/shops/{shop\_id}/products/{product\_id}.json |
| **Update a product**<br>`PUT /v1/shops/{shop_id}/products/{product_id}.json`<br>`{<br>    "title": "Product"<br>}` [View Response](https://developers.printify.com/#)`{<br>     "id": "5d39b411749d0a000f30e0f4",<br>     "title": "Product",<br>     "description": "Good product",<br>     "safety_information": "GPSR information: John Doe, test@example.com, 123 Main St, Apt 1, New York, NY, 10001, US<br>     Product information: Gildan, 5000, 2 year warranty in EU and UK as per Directive 1999/44/EC<br>     Warnings, Hazzard: No warranty, US<br>     Care instructions: Machine wash: warm (max 40C or 105F), Non-chlorine: bleach as needed, Tumble dry: medium, Do not iron, Do not dryclean",<br>     "tags": [<br>         "Home & Living",<br>         "Stickers"<br>     ],<br>     "options": [<br>         {<br>             "name": "Size",<br>             "type": "size",<br>             "values": [<br>                 {<br>                     "id": 2017,<br>                     "title": "2x2\""<br>                 },<br>                 {<br>                     "id": 2018,<br>                     "title": "3x3\""<br>                 },<br>                 {<br>                     "id": 2019,<br>                     "title": "4x4\""<br>                 },<br>                 {<br>                     "id": 2020,<br>                     "title": "6x6\""<br>                 }<br>             ]<br>         },<br>         {<br>             "name": "Type",<br>             "type": "surface",<br>             "values": [<br>                 {<br>                     "id": 2114,<br>                     "title": "White"<br>                 }<br>             ]<br>         }<br>     ],<br>     "variants": [<br>         {<br>             "id": 45740,<br>             "sku": "866375988",<br>             "cost": 134,<br>             "price": 400,<br>             "title": "2x2\" / White",<br>             "grams": 10,<br>             "is_enabled": true,<br>             "is_default": true,<br>             "is_available": true,<br>             "is_printify_express_eligible": true,<br>             "options": [<br>                 2017,<br>                 2114<br>             ]<br>         },<br>         {<br>             "id": 45742,<br>             "sku": "866375989",<br>             "cost": 149,<br>             "price": 400,<br>             "title": "3x3\" / White",<br>             "grams": 10,<br>             "is_enabled": true,<br>             "is_default": false,<br>             "is_available": true,<br>             "is_printify_express_eligible": true,<br>             "options": [<br>                 2018,<br>                 2114<br>             ]<br>         },<br>         {<br>             "id": 45744,<br>             "sku": "866375990",<br>             "cost": 187,<br>             "price": 400,<br>             "title": "4x4\" / White",<br>             "grams": 10,<br>             "is_enabled": true,<br>             "is_default": false,<br>             "is_available": true,<br>             "is_printify_express_eligible": true,<br>             "options": [<br>                 2019,<br>                 2114<br>             ]<br>         },<br>         {<br>             "id": 45746,<br>             "sku": "866375991",<br>             "cost": 216,<br>             "price": 400,<br>             "title": "6x6\" / White",<br>             "grams": 10,<br>             "is_enabled": true,<br>             "is_default": false,<br>             "is_available": true,<br>             "is_printify_express_eligible": true,<br>             "options": [<br>                 2020,<br>                 2114<br>             ]<br>         }<br>     ],<br>     "images": [<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45740/2187/product.jpg",<br>             "variant_ids": [<br>                 45740<br>             ],<br>             "position": "front",<br>             "is_default": true<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45740/2188/product.jpg",<br>             "variant_ids": [<br>                 45740<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45740/2189/product.jpg",<br>             "variant_ids": [<br>                 45740<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45740/2190/product.jpg",<br>             "variant_ids": [<br>                 45740<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45740/2191/product.jpg",<br>             "variant_ids": [<br>                 45740<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45740/2192/product.jpg",<br>             "variant_ids": [<br>                 45740<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45740/2193/product.jpg",<br>             "variant_ids": [<br>                 45740<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45740/2194/product.jpg",<br>             "variant_ids": [<br>                 45740<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45740/2195/product.jpg",<br>             "variant_ids": [<br>                 45740<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45740/2196/product.jpg",<br>             "variant_ids": [<br>                 45740<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45740/2197/product.jpg",<br>             "variant_ids": [<br>                 45740<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45740/2198/product.jpg",<br>             "variant_ids": [<br>                 45740<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45740/2199/product.jpg",<br>             "variant_ids": [<br>                 45740<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45740/2200/product.jpg",<br>             "variant_ids": [<br>                 45740<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45740/2201/product.jpg",<br>             "variant_ids": [<br>                 45740<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45740/2202/product.jpg",<br>             "variant_ids": [<br>                 45740<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45742/2187/product.jpg",<br>             "variant_ids": [<br>                 45742<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45742/2188/product.jpg",<br>             "variant_ids": [<br>                 45742<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45742/2189/product.jpg",<br>             "variant_ids": [<br>                 45742<br>             ],<br>             "position": "front",<br>             "is_default": true<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45742/2190/product.jpg",<br>             "variant_ids": [<br>                 45742<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45742/2191/product.jpg",<br>             "variant_ids": [<br>                 45742<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45742/2192/product.jpg",<br>             "variant_ids": [<br>                 45742<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45742/2193/product.jpg",<br>             "variant_ids": [<br>                 45742<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45742/2194/product.jpg",<br>             "variant_ids": [<br>                 45742<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45742/2195/product.jpg",<br>             "variant_ids": [<br>                 45742<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45742/2196/product.jpg",<br>             "variant_ids": [<br>                 45742<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45742/2197/product.jpg",<br>             "variant_ids": [<br>                 45742<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45742/2198/product.jpg",<br>             "variant_ids": [<br>                 45742<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45742/2199/product.jpg",<br>             "variant_ids": [<br>                 45742<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45742/2200/product.jpg",<br>             "variant_ids": [<br>                 45742<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45742/2201/product.jpg",<br>             "variant_ids": [<br>                 45742<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45742/2202/product.jpg",<br>             "variant_ids": [<br>                 45742<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45744/2187/product.jpg",<br>             "variant_ids": [<br>                 45744<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45744/2188/product.jpg",<br>             "variant_ids": [<br>                 45744<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45744/2189/product.jpg",<br>             "variant_ids": [<br>                 45744<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45744/2190/product.jpg",<br>             "variant_ids": [<br>                 45744<br>             ],<br>             "position": "front",<br>             "is_default": true<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45744/2191/product.jpg",<br>             "variant_ids": [<br>                 45744<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45744/2192/product.jpg",<br>             "variant_ids": [<br>                 45744<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45744/2193/product.jpg",<br>             "variant_ids": [<br>                 45744<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45744/2194/product.jpg",<br>             "variant_ids": [<br>                 45744<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45744/2195/product.jpg",<br>             "variant_ids": [<br>                 45744<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45744/2196/product.jpg",<br>             "variant_ids": [<br>                 45744<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45744/2197/product.jpg",<br>             "variant_ids": [<br>                 45744<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45744/2198/product.jpg",<br>             "variant_ids": [<br>                 45744<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45744/2199/product.jpg",<br>             "variant_ids": [<br>                 45744<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45744/2200/product.jpg",<br>             "variant_ids": [<br>                 45744<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45744/2201/product.jpg",<br>             "variant_ids": [<br>                 45744<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45744/2202/product.jpg",<br>             "variant_ids": [<br>                 45744<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45746/2187/product.jpg",<br>             "variant_ids": [<br>                 45746<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45746/2188/product.jpg",<br>             "variant_ids": [<br>                 45746<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45746/2189/product.jpg",<br>             "variant_ids": [<br>                 45746<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45746/2190/product.jpg",<br>             "variant_ids": [<br>                 45746<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45746/2191/product.jpg",<br>             "variant_ids": [<br>                 45746<br>             ],<br>             "position": "front",<br>             "is_default": true<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45746/2192/product.jpg",<br>             "variant_ids": [<br>                 45746<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45746/2193/product.jpg",<br>             "variant_ids": [<br>                 45746<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45746/2194/product.jpg",<br>             "variant_ids": [<br>                 45746<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45746/2195/product.jpg",<br>             "variant_ids": [<br>                 45746<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45746/2196/product.jpg",<br>             "variant_ids": [<br>                 45746<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45746/2197/product.jpg",<br>             "variant_ids": [<br>                 45746<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45746/2198/product.jpg",<br>             "variant_ids": [<br>                 45746<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45746/2199/product.jpg",<br>             "variant_ids": [<br>                 45746<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45746/2200/product.jpg",<br>             "variant_ids": [<br>                 45746<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45746/2201/product.jpg",<br>             "variant_ids": [<br>                 45746<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         },<br>         {<br>             "src": "https://images.printify.com/mockup/5d39b411749d0a000f30e0f4/45746/2202/product.jpg",<br>             "variant_ids": [<br>                 45746<br>             ],<br>             "position": "front",<br>             "is_default": false<br>         }<br>     ],<br>     "created_at": "2019-07-25 13:52:17+00:00",<br>     "updated_at": "2019-07-25 13:52:18+00:00",<br>     "visible": true,<br>     "is_locked": false,<br>     "is_printify_express_eligible": true,<br>     "is_printify_express_enabled": true,<br>     "is_economy_shipping_eligible": true,<br>     "is_economy_shipping_enabled": true,<br>     "blueprint_id": 384,<br>     "user_id": 1337,<br>     "shop_id": 1337,<br>     "print_provider_id": 1,<br>     "print_areas": [<br>         {<br>             "variant_ids": [<br>                 45740,<br>                 45742,<br>                 45744,<br>                 45746<br>             ],<br>             "placeholders": [<br>                 {<br>                     "position": "front",<br>                     "decoration_method": "dtg",<br>                     "images": [<br>                         {<br>                             "id": "5d15ca551163cde90d7b2203",<br>                             "src": "https://image-storage.example.com/5d39b159e7c48c000728c89f",<br>                             "name": "Asset 65@3x.png",<br>                             "type": "image/png",<br>                             "height": 1200,<br>                             "width": 1200,<br>                             "x": 0.5,<br>                             "y": 0.5,<br>                             "scale": 1,<br>                             "angle": 0<br>                         }<br>                     ]<br>                 }<br>             ],<br>             "background": "#ffffff"<br>         }<br>     ],<br>     "views": [<br>         {<br>             "id": 34395,<br>             "label": "Front side",<br>             "position": "front",<br>             "files": [<br>                 {<br>                     "src": "https://images.printify.com/api/catalog/618e1792f80e2001a840687b.svg",<br>                     "variant_ids": [<br>                         45740,<br>                         45742,<br>                         45744,<br>                         45746<br>                     ]<br>                 },<br>             ]<br>         }<br>     ],<br>     "sales_channel_properties": []<br>}` |

#### Delete a product

|     |     |
| --- | --- |
| DELETE | /v1/shops/{shop\_id}/products/{product\_id}.json |
| **Delete a product**<br>`DELETE /v1/shops/{shop_id}/products/{product_id}.json`<br>[View Response](https://developers.printify.com/#)`{}` |

#### Publish a product

This does not implement any publishing action unless the Printify store is connected to one of our other supported sales channel integrations, if your store is custom and is subscribed to the product::pubish::started event, that event will be triggered and the properties that are set in the request body will be set in the event payload for your store to react to if implemented. The case is the same for attempting to publish a product from the Printify app. See [product events](https://developers.printify.com/#product-events) for reference.

|     |     |
| --- | --- |
| POST | /v1/shops/{shop\_id}/products/{product\_id}/publish.json |
| **Publish a product**<br>`POST /v1/shops/{shop_id}/products/{product_id}/publish.json`<br>`{<br>    "title": true,<br>    "description": true,<br>    "images": true,<br>    "variants": true,<br>    "tags": true,<br>    "keyFeatures": true,<br>    "shipping_template": true<br>}` [View Response](https://developers.printify.com/#)`{}` |

#### Set product publish status to succeeded

Using this endpoint removes the product from the locked status on the Printify app and sets the the it's external property with the handle you provide in the request body.

|     |     |
| --- | --- |
| POST | /v1/shops/{shop\_id}/products/{product\_id}/publishing\_succeeded.json |
| **Set product publish status to succeeded**<br>`POST /v1/shops/{shop_id}/products/{product_id}/publishing_succeeded.json`<br>`{<br>    "external": {<br>        "id": "5941187eb8e7e37b3f0e62e5",<br>        "handle": "https://example.com/path/to/product"<br>    }<br>}` [View Response](https://developers.printify.com/#)`{}` |

#### Set product publish status to failed

Using this endpoint removes the product from the locked status on the Printify app.

|     |     |
| --- | --- |
| POST | /v1/shops/{shop\_id}/products/{product\_id}/publishing\_failed.json |
| **Set product publish status to failed**<br>`POST /v1/shops/{shop_id}/products/{product_id}/publishing_failed.json`<br>`{<br>    "reason": "Request timed out"<br>}` [View Response](https://developers.printify.com/#)`{}` |

#### Notify that a product has been unpublished

|     |     |
| --- | --- |
| POST | /v1/shops/{shop\_id}/products/{product\_id}/unpublish.json |
| **Notify that a product has been unpublished**<br>`POST /v1/shops/{shop_id}/products/{product_id}/unpublish.json`<br>[View Response](https://developers.printify.com/#)`{}` |

### Structure

Structure of Product resource with possible transitions between endpoints.

![products structure](https://developers.printify.com/images/ProductsStructure-4217fa4a.png)

#### Image positioning

- Coordinate system

![coordinate system](https://developers.printify.com/images/PrintifyCoordinates-1e0f89a3.png)


Printify uses the `[0,00; 0,00] .. [1,00; 1,00]` cartesian coordinate system, with the placeholder center being
`x=0,5`, `y=0,5`.
- Artwork scale

![scale 1,00](https://developers.printify.com/images/PrintifyScaling100-800703b4.png)![scale 0,5](https://developers.printify.com/images/PrintifyScaling50-64af13c5.png)

The scale of the image (width) relative to the print area placeholder (width).
Scale can be anything from `0,00` to infinity.

- `1,00` \- scale image to fill the print area fully
- `0,5` \- scale image to fill 1/2 of the the print area

  - Artwork angle - 360° angle

Rule of thumb: if you use artwork with width equal to print area placeholder width, set scale to `1,00` and position it
at `x=0,5``y=0,5` \- your design will be horizontally and vertically aligned and fill all the print area fully.

### Creating Products

Flow of transitions between resources for making the product - with two possible paths of coming from Blueprint or Print Provider.

![creating product by blueprint](https://developers.printify.com/images/CreatingProductByBlueprint-72e34fca.png)

![creating product by blueprint](https://developers.printify.com/images/CreatingProductByPrintProvider-7a01e0e6.png)

### Common error cases

You may receive errors when trying to create or update a product. A common error is due failing dpi validation because the image is low quality. If this happens, you will receive a detailed error message similar to the one shown here.

|     |     |
| --- | --- |
| POST | /v1/shops/{shop\_id}/products.json |
| **Common error cases**<br>`POST /v1/shops/{shop_id}/products.json`<br>400 Image has low quality error example (See HTTP Status Codes below) [View Response](https://developers.printify.com/#)`{<br>    "status": "error",<br>    // Exact error codes and messages are subject to change.<br>    "code": 8203,<br>    "message": "Validation failed.",<br>    "errors": {<br>      "reason": "Image has low quality",<br>      "code": 8203<br>    }<br>}` |

|     |     |
| --- | --- |
| PUT | /v1/shops/{shop\_id}/products/{product\_id}.json |
| **Common error cases**<br>`PUT /v1/shops/{shop_id}/products/{product_id}.json`<br>400 Image has low quality error example (See HTTP Status Codes below) [View Response](https://developers.printify.com/#)`{<br>    "status": "error",<br>    // Exact error codes and messages are subject to change.<br>    "code": 8203,<br>    "message": "Validation failed.",<br>    "errors": {<br>      "reason": "Image has low quality",<br>      "code": 8203<br>    }<br>}` |

## Orders

The Printify APl lets your application manage orders in a Merchant's shop. You can submit orders for existing products in a merchant's shop, or you can create new products **on-the-fly** with every order, as in the case of merchandise created with customizable user-generated content.

|     |     |
| --- | --- |
| ℹ | **Embroidery products are supported.**<br> See the [Create a new product](https://developers.printify.com/#create-a-new-product) endpoint for more details. |

|     |     |
| --- | --- |
| ⚠ | All order endpoints require a `{shop_id}` parameter. See [Retrieving Shop ID](https://developers.printify.com/#retrieving-shop-id) for instructions on how to obtain your shop ID. |

|     |     |
| --- | --- |
| ⚠ | **On-the-fly** product creation is a time-consuming operation and may lead to timeouts.<br> For better reliability, create products in advance whenever possible. This functionality will be deprecated<br> in the future in favor of dedicated product creation endpoints. |

Ordering existing products or creating products with orders will require different line item entries so that should be kept in mind.

|     |     |
| --- | --- |
| ⚠ | By default, new stores have **automatic order approval** enabled (24 hours). If auto-approval is active, orders will be sent to production automatically once imported/created, without calling the [Send to production](https://developers.printify.com/#send-an-existing-order-to-production) API endpoint.<br> If you prefer to control when orders are sent to production:<br> <br>1. Check each store's [Order approval settings](https://help.printify.com/hc/en-us/articles/4483625253265-How-can-I-set-up-store-details-and-order-approval-settings) and set them to **Manual** to avoid unintended production.<br>2. When ready, explicitly trigger production via the [Send to production](https://developers.printify.com/#send-an-existing-order-to-production) endpoint. |

On this page:

- [What you can do with the order resource](https://developers.printify.com/#what-you-can-do-with-the-order-resource)
- [Order properties](https://developers.printify.com/#order-properties)
  - [Line item properties](https://developers.printify.com/#line-item-properties)
  - [Line item metadata properties](https://developers.printify.com/#line-item-metadata-properties)
  - [Metadata properties](https://developers.printify.com/#metadata-properties)
  - [Shipment properties](https://developers.printify.com/#shipment-properties)
  - [Order submission properties](https://developers.printify.com/#order-submission-properties)
  - [Print area properties](https://developers.printify.com/#print-area-properties)
  - [Print details properties](https://developers.printify.com/#print-details-properties)
  - [Personalisation properties](https://developers.printify.com/#personalisation-properties)
- [Endpoints](https://developers.printify.com/#orders-endpoints)
- [Structure](https://developers.printify.com/#orders-structure)
- [Making Order](https://developers.printify.com/#making-order)
- [Common error cases](https://developers.printify.com/#orders-common-error-cases)

### What you can do with the order resource

The Printify Public API lets you do the following with the Order resource:

- [GET /v1/shops/{shop\_id}/orders.json](https://developers.printify.com/#retrieve-a-list-of-orders)

Retrieve a list of orders
- [GET /v1/shops/{shop\_id}/orders/{order\_id}.json](https://developers.printify.com/#get-order-details-by-id)

Get order details by id
- [POST /v1/shops/{shop\_id}/orders.json](https://developers.printify.com/#submit-an-order)

Submit an order
- [POST /v1/shops/{shop\_id}/express.json](https://developers.printify.com/#submit-a-printify-express-order)

Submit a Printify Express order
- [POST /v1/shops/{shop\_id}/orders/{order\_id}/send\_to\_production.json](https://developers.printify.com/#send-an-existing-order-to-production)

Send an existing order to production
- [POST /v1/shops/{shop\_id}/orders/shipping.json](https://developers.printify.com/#calculate-the-shipping-cost-of-an-order)

Calculate the shipping cost of an order
- [POST /v1/shops/{shop\_id}/orders/{order\_id}/cancel.json](https://developers.printify.com/#cancel-an-order)

Cancel an unpaid order

### Order properties

| id<br> READ-ONLY | `"id": "5a96f649b2439217d070f507"`<br> A unique string identifier for the order. Each id is unique across the Printify system. |
| app\_order\_id<br> READ-ONLY | `"app_order_id": "215014.44"`<br> The Web app Printify order ID for the order. Present only in responses (read-only), and cannot be used for searching or filtering. |
| address\_to<br> REQUIREDREAD-ONLY | `"address_to": {<br>    "first_name": "John",<br>    "last_name": "Smith",<br>    "region": "",<br>    "address1": "ExampleBaan 121",<br>    "city": "Retie",<br>    "zip": "2470",<br>    "email": "example@msn.com",<br>    "phone": "0574 69 21 90",<br>    "country": "BE",<br>    "company": "MSN"<br>}`<br> The delivery details of the order's recipient. |
| line\_items<br> REQUIREDREAD-ONLY | `"line_items": [{<br>      "product_id": "5b05842f3921c9547531758d",<br>      "quantity": 1,<br>      "variant_id": 17887,<br>      "print_provider_id": 5,<br>      "cost": 1050,<br>      "shipping_cost": 400,<br>      "status": "pending",<br>      "metadata": {<br>        "title": "18K gold plated Necklace",<br>        "price": 2200,<br>        "variant_label": "Golden indigocoin",<br>        "sku": "168699843",<br>        "country": "United States"<br>      },<br>      "sent_to_production_at": "2017-04-18 13:24:28+00:00",<br>      "fulfilled_at": "2017-04-18 13:24:28+00:00"<br>}]`<br> A list of all line items in the order. See [line item properties](https://developers.printify.com/#line-item-properties) for reference. |
| metadata<br> READ-ONLY | `"metadata": {<br>    "order_type": "external",<br>    "shop_order_id": 1370762297,<br>    "shop_order_label": "1370762297",<br>    "shop_fulfilled_at": "2017-04-18 13:24:28+00:00",<br>    "is_reprint": true,<br>    "reprinted_order_ids": ["6a72ef76c6503ada3c069ecc"],<br>    "child_reprinted_order_ids": ["6a72f40c351dc156610b500a"]<br>}`<br> Other data about the order. See [metadata properties](https://developers.printify.com/#metadata-properties) for reference. |
| total\_price<br> READ-ONLY | `"total_price": 2200`<br> Retail price in cents, integer value. |
| total\_shipping<br> READ-ONLY | `"total_shipping": 400`<br> Shipping price in cents, integer value. |
| total\_tax<br> READ-ONLY | `"total_tax": 0`<br> Tax cost in cents, integer value. |
| status<br> READ-ONLY | `"status": "pending"`

Production status of the entire order in string format, it can be any of the following:

| Status | Definition |
| --- | --- |
| `pending` | An order is created in the `pending` status. Orders should not stay in this status for a long time. |
| `on-hold` | The order is ready to handle user actions. Users can edit orders in this status. The order gets this status at later stages for various reasons:<br>- Line items are discontinued during the order processing<br>- Line items go out of stock during the order processing<br>- The order contains items with shipping restricted line items<br>User needs to take actions upon orders that got the status during the submission. |
| `sending-to-production` | Order is picked for sending to production. The status should be changed when the system receives updates from print providers. |
| `in-production` | Order has been received by the print providers successfully. Print providers start the fulfillment process on their side. |
| `canceled` | The order is canceled. No actions can be taken towards the order by the user. |
| `fulfilled` | All line items are fulfilled by all print providers. The last status for successful order fulfillment. |
| `partially-fulfilled` | At least one of the line items is fulfilled, but not all of them. |
| `payment-not-received` | The order could not be charged during the submission in our system. It can be retried by the merchant. The order waits for merchant actions. |
| `has-issues` | If an order encounters any issue during its lifecycle it will get this status. For instance, the shipping address is invalid. |
| `cost-calculation` | Cost calculation is in progress. |
| `unfulfillable` | Order cannot be fulfilled due to inventory or technical issues. |
| `sending_to_production_delegate` | Order delegated for external production handling. |
| `sending_to_production_delegate_sync` | Order delegated for synchronous production handling. |
| `source-check-failed` | Source file validation failed. | |
| shipping\_method<br> REQUIRED | `"shipping_method": 1`

Method of shipping selected for the order, "1" is for standard shipping and "2" is for ~~express~~ priority shipping, "3" is for [Printify Express](https://help.printify.com/hc/en-us/sections/9116968124689-Printify-Express-Delivery) shipping and "4" is for [Economy](https://help.printify.com/hc/en-us/sections/22109518886161-Economy-Shipping) shipping. Please note, that express order can only contain products eligible for express delivery. Similarly, economy order can only contain products eligible for economy delivery. More about shipping methods can be read here: [Printify's shipping options](https://help.printify.com/hc/en-us/articles/4483626155409-What-are-Printify-s-shipping-options)

|     |     |
| --- | --- |
| ⚠ | Please be aware that Printify Express Delivery is using carriers that might not be supported by all sales channels (e.g. Amazon, Tik Tok). |

|     |     |
| --- | --- |
| ⚠ | Please be aware that only the [Product's](https://developers.printify.com/#product-properties) and the [Variant's](https://developers.printify.com/#product-variant-properties) eligibility (`is_printify_express_eligible` flag) is taken into account. Eligible but disabled products (`is_printify_express_enabled` flag) can still be ordered with [Printify Express Delivery](https://help.printify.com/hc/en-us/sections/9116968124689-Printify-Express-Delivery). |

|     |     |
| --- | --- |
| ⚠ | Please be aware that shipping method 4 (`economy`) will not be usable when creating a product with an order. Therefore, for this shipping method the product must already exist before placing an order on it. |

Property value should be decoded based on the following table:

| Code | Old version | Transitional version \[active\] | Final version |
| --- | --- | --- | --- |
| 1 | standard | standard | standard |
| 2 | express | express<br>priority | priority |
| 3 |  | printify\_express | express |
| 4 | economy | economy | economy |

The **printify\_express** is a new shipping option that will later in the future change its name to the **express**. Current **express** option will be renamed to the **priority** name. |
| is\_printify\_express<br> READ-ONLY | `"is_printify_express": true`<br>Boolean value that indicates if the order is using [Printify Express](https://help.printify.com/hc/en-us/sections/9116968124689-Printify-Express-Delivery) shipping. |
| is\_economy\_shipping<br> READ-ONLY | `"is_economy_shipping": true`<br>Boolean value that indicates if the order is using [Economy](https://help.printify.com/hc/en-us/sections/22109518886161-Economy-Shipping) shipping. |
| shipments<br> READ-ONLY | `"shipments": [{<br>      "carrier": "usps",<br>      "number": "94001116990045395649372",<br>      "url": "http://example.com/94001116990045395649372",<br>      "delivered_at": "2017-04-18 13:24:28+00:00"<br>}]`<br> Tracking details of the order after fulfillment. See [shipment properties](https://developers.printify.com/#shipment-properties) for reference. |
| created\_at<br> READ-ONLY | `"created_at": "2017-04-18 13:24:28+00:00"`<br> The date and time the order was created. It is stored in ISO date format. |
| sent\_to\_production\_at<br> READ-ONLY | `"sent_to_production_at": "2017-04-18 13:24:28+00:00"`<br> The date and time the order was sent to production. It is stored in ISO date format. |
| fulfilled\_at<br> READ-ONLY | `"fulfilled_at": "2017-04-18 13:24:28+00:00"`<br> The date and time the order was fulfilled. It is stored in ISO date format. |
| printify\_connect<br> READ-ONLY | `"printify_connect": {<br>      "url": "https://example.com/printify_connect_hash",<br>      "id": "printify_connect_hash"<br>}`<br> Printify Connect data containing link to the order in the Printify Connect page and the unique hash for the order.<br> More about Printify Connect can be read in our [Help Center](https://help.printify.com/hc/en-us/articles/7810118238097-What-is-Printify-Connect-) or [Blog](https://printify.com/blog/introducing-printify-connect/). |

### Line item properties

| product\_id<br> READ-ONLY | `"product_id": "5b05842f3921c9547531758d"`<br> A unique string identifier for the product. Each id is unique across the Printify system. |
| external\_id<br> OPTIONAL | `"external_id": "abc-1234"`<br> Unique identifier of the line item from the external system. Preserved during replacements and routing. |
| variant\_id<br> REQUIREDREAD-ONLY | `"variant_id": 17887`<br> A unique int identifier for the product variant from the blueprint. Each id is unique across the Printify system. |
| quantity<br> REQUIRED | `"quantity": 1`<br> Describes the number of said product ordered as an integer. |
| print\_provider\_id<br> REQUIREDREAD-ONLY | `"print_provider_id": 5`<br> A unique int identifier for the print provider. Each id is unique across the Printify system. |
| cost<br> READ-ONLY | `"cost": 1050`<br> Product variant's fulfillment cost in cents, integer value. |
| shipping\_cost<br> READ-ONLY | `"shipping_cost": 400`<br> Product variant's shipment cost in cents, integer value. |
| status<br> READ-ONLY | `"status": "in-production"`

Specific line item fulfillment status:

| Status | Definition |
| --- | --- |
| `on-hold` | The item waits for user actions. Items get this status when:<br>- The order is created.<br>- The order fails at one of the checks in the submission process.<br>- The order fails with payments. |
| `in-production` | Print provider received the item for production. |
| `sending-to-production` | Says that the order is picked for sending to production. The status is changed once the system receives updates from print providers. |
| `has-issues` | Line item encountered an issue during its lifecycle. |
| `fulfilled` | The item is fulfilled by the print provider. |
| `canceled` | The item is canceled. | |
| metadata<br> READ-ONLY | `"metadata": {<br>        "title": "18K gold plated Necklace",<br>        "price": 2200,<br>        "variant_label": "Golden indigocoin",<br>        "sku": "168699843",<br>        "country": "United States"<br>}`<br> Other details about the specific product variant. See [line item metadata properties](https://developers.printify.com/#line-item-metadata-properties) for reference. |
| sent\_to\_production\_at<br> READ-ONLY | `"sent_to_production_at": "2017-04-18 13:24:28+00:00"`<br> The date and time the product variant was sent to production. It is stored in ISO date format. |
| fulfilled\_at<br> READ-ONLY | `"fulfilled_at": "2017-04-18 13:24:28+00:00"`<br> The date and time the product variant was fulfilled. It is stored in ISO date format. |

#### Line item metadata properties

|     |     |
| --- | --- |
| title<br> READ-ONLY | `"title": "Product's title"`<br> The name of the product. |
| price<br> READ-ONLY | `"price": 1000`<br> Retail price in cents, integer value. |
| variant\_label<br> READ-ONLY | `"variant_label": "Golden indigocoin"`<br> Name of the product variant. |
| sku<br> READ-ONLY | `"sku": "168699843"`<br> A unique string identifier for the product variant. |
| country<br> READ-ONLY | `"country": "United States"`<br> Location of print provider handling fulfillment. |
| external\_id<br> READ-ONLY | `"external_id": "abc-1234"`<br> The external identifier provided when submitting the order. |

### Metadata properties

|     |     |
| --- | --- |
| order\_type<br> READ-ONLY | `"order_type": "external"`<br> Describes the order type, can be external, manual, or sample. |
| shop\_order\_id<br> READ-ONLY | `"shop_order_id": 1370762297`<br> A unique integer identifier for the order in the external sales channel. |
| shop\_order\_label<br> READ-ONLY | `"shop_order_id": "1370762297"`<br> A unique string identifier for the order in the external sales channel. |
| shop\_fulfilled\_at<br> READ-ONLY | `"shop_fulfilled_at": "2017-04-18 13:24:28+00:00"`<br> The date and time the order was fulfilled. It is stored in ISO date format. |
| is\_reprint<br> READ-ONLY | `"is_reprint": false`<br> Whether this order was created as a reprint of one or more other orders. |
| reprinted\_order\_ids<br> READ-ONLY | `"reprinted_order_ids": ["6a72ef76c6503ada3c069ecc"]`<br> IDs of the original orders that this order reprints. Populated only when `is_reprint` is true. |
| child\_reprinted\_order\_ids<br> READ-ONLY | `"child_reprinted_order_ids": ["6a72f40c351dc156610b500a"]`<br> IDs of the reprint orders that were created from this order. |

### Shipment properties

|     |     |
| --- | --- |
| carrier<br> READ-ONLY | `"carrier": "usps"`<br> Name of the shipping courier used to deliver the order to its recipient. |
| number<br> READ-ONLY | `"number": "123"`<br> A unique string tracking number from the shipping courier used to track the status of the shipment. |
| url<br> READ-ONLY | `"url": "http://example.com/94001116990045395649372"`<br> A unique string tracking link from the shipping courier used to track the status of the shipment. |
| delivered\_at<br> READ-ONLY | `"delivered_at": "2017-04-18 13:24:28+00:00"`<br> The date and time the order was delivered. It is stored in ISO date format. |

### Order submission properties

|     |     |
| --- | --- |
| external\_id<br> REQUIRED | `"external_id": "2750e210-39bb-11e9-a503-452618153e4a"`<br> A unique string identifier from the sales channel specifying the order name or id. |
| label<br> OPTIONAL | `"label": "000012"`<br> Optional value to specify order label instead of using "external\_id" |
| line\_items<br> REQUIRED | `"line_items": [{<br>      "product_id": "5bfd0b66a342bcc9b5563216",<br>      "variant_id": 17887,<br>      "quantity": 1,<br>      "external_id": "line-item-abc-001"<br>}]`<br> Required for ordering existing products. Provide the product\_id (Printify Product ID), variant\_id (selected variant, e.g. 'White / XXL') and desired item quantity. If creating a product from the order is required, then additional attributes will need to be provided, specifically the blueprint\_id and print\_areas.<br> `"line_items": [{<br>      "print_provider_id": 5,<br>      "blueprint_id": 9,<br>      "variant_id": 17887,<br>      "print_areas": {<br>        "front": "https://images.example.com/image.png"<br>      },<br>      "quantity": 1,<br>      "external_id": "line-item-abc-001"<br>}]`<br> See [product properties](https://developers.printify.com/#product-properties) and [variant properties](https://developers.printify.com/#product-variant-properties) for reference. Also, see [print area properties](https://developers.printify.com/#print-area-properties) for reference on print\_areas for product creation during order submission. It is also possible to order existing products by providing the product variant's SKU alone.<br> `"line_items": [{<br>      "sku": "MY-SKU",<br>      "quantity": 1,<br>      "external_id": "line-item-abc-001"<br>}]`<br> See [variant properties](https://developers.printify.com/#product-variant-properties) for reference.<br> A line item can also carry a personalization created via the [Create a personalization configuration](https://developers.printify.com/#create-a-personalization-configuration) endpoint:<br> `"line_items": [{<br>      "product_id": "5bfd0b66a342bcc9b5563216",<br>      "variant_id": 17887,<br>      "quantity": 1,<br>      "personalisation": {<br>        "personalisation_strategy": "pstudio_pre_order_headless",<br>        "personalisation_instructions": "3fa85f64-5717-4562-b3fc-2c963f66afa6"<br>      }<br>}]`<br> See [personalisation properties](https://developers.printify.com/#personalisation-properties) for reference. |
| shipping\_method<br> REQUIRED | `"shipping_method": 1`<br> Required to specify what method of shipping is desired, "1" means standard shipping, "2" means priority shipping, "3" means printify express shipping and "4" means economy shipping. It is stored as an integer. |
| send\_shipping\_notification<br> BOOLEAN | `"send_shipping_notification": false`<br> A boolean for choosing whether or not to receive email notifications after an order is shipped. |
| address\_to<br> REQUIRED | `"address_to": {<br>    "first_name": "John",<br>    "last_name": "Smith",<br>    "email": "example@msn.com",<br>    "phone": "0574 69 21 90",<br>    "country": "BE",<br>    "region": "",<br>    "address1": "ExampleBaan 121",<br>    "address2": "45",<br>    "city": "Retie",<br>    "zip": "2470"<br>}`<br> The delivery details of the order's recipient. |

### Print area properties

|     |     |
| --- | --- |
| placeholder position and image url<br> REQUIRED | `"print_areas": {<br>        "front": "https://images.example.com/image.png",<br>        "back": "https://images.example.com/image.png"<br>}`<br> Required for creating products during order submission, See [placeholder properties](https://developers.printify.com/#placeholder-properties) for reference. <br> <br> Instead of specifing the url, it is also possible to provide an array with image objects that have additional keys for the advanced positioning: <br> `<br>        "print_areas": {<br>          "front": [<br>            {<br>                "src": "https://images.example.com/image.png",<br>                "scale": 0.15,<br>                "x": 0.80,<br>                "y": 0.34,<br>                "angle": 215<br>            },<br>            {<br>                "src": "https://images.example.com/image2.png",<br>                "scale": 1,<br>                "x": 0.5,<br>                "y": 0.5,<br>                "angle": 0<br>            }<br>          ],<br>          "back": [<br>            {<br>                "src": "https://images.example.com/image3.png",<br>                "scale": 1,<br>                "x": 0.5,<br>                "y": 0.5,<br>                "angle": 0<br>            }<br>          ]<br>        }<br>` |

### Print details properties

|     |     |
| --- | --- |
| Special print options<br> OPTIONAL | `<br>        "print_details": {<br>            "print_on_side": "mirror"<br>        }<br>`<br> Used to store properties for special cases like printing on canvas sides or clock separators, See [print details properties](https://developers.printify.com/#print-details-properties) for reference. |

### Personalisation properties

|     |     |
| --- | --- |
| personalisation\_strategy<br> OPTIONAL | `"personalisation_strategy": "pstudio_pre_order_headless"`<br> The personalization strategy to apply to this line item. Pass the value exactly as returned by<br> [Create a personalization configuration](https://developers.printify.com/#create-a-personalization-configuration) — it's an opaque<br> value and shouldn't be constructed manually.<br> The one value worth knowing about explicitly is `manual`, which indicates a mapping issue caused by a<br> label inconsistency (the personalizable product was changed). The order will require manual adjustment from the<br> merchant and won't be sent to production automatically. |
| personalisation\_instructions<br> OPTIONAL | `"personalisation_instructions": "3fa85f64-5717-4562-b3fc-2c963f66afa6"`<br> The instructions to apply, paired with `personalisation_strategy` and also returned by<br> [Create a personalization configuration](https://developers.printify.com/#create-a-personalization-configuration). Pass it through<br> as-is — it's an opaque reference token for most strategies, or human-readable free text when<br> `personalisation_strategy` is `manual` (e.g. `"Please update the print manually."`).<br> A deprecated, top-level `line_items[].personalisation_instructions` field is still accepted for<br> backward compatibility, but is superseded by this nested value when both are present. New integrations should<br> use this nested field instead. |
| buyer\_request<br> OPTIONAL | `"buyer_request": "Please use John as first name"`<br> A free-text note from the buyer about the requested personalization. |
| layers<br> OPTIONAL | `"layers": [<br>    {<br>        "personalisation_id": "123",<br>        "name": "front",<br>        "layer_type": "text",<br>        "text_input": "John"<br>    },<br>    {<br>        "personalisation_id": "456",<br>        "name": "back",<br>        "layer_type": "image",<br>        "image_id": "789"<br>    }<br>]`<br> An array describing the personalized layers for this line item. `personalisation_id` identifies the<br> personalization field/layer (matching the `field_id` used when creating the personalization), not a<br> standalone personalization resource. `name` and `layer_type` are required; `text_input`<br> and `image_id` are used depending on the layer type. |
| personalisation\_buyer\_confirmation<br> OPTIONAL | `"personalisation_buyer_confirmation": {<br>    "approved": true,<br>    "source": "storefront",<br>    "date": "2017-04-18T13:24:28+00:00",<br>    "ip_address": "192.168.1.100",<br>    "user_agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/126.0.0.0 Safari/537.36"<br>}`<br> Records the buyer's confirmation of the personalized preview: whether it was `approved`, its<br> `source`, the confirmation `date` (ISO-8601), and optionally the buyer's `ip_address`<br> and `user_agent`. |

### Endpoints

#### Retrieve a list of orders

|     |     |
| --- | --- |
| GET | /v1/shops/{shop\_id}/orders.json |
| limit<br> OPTIONAL | Results per page<br>(default: 10, maximum: 10) |
| page<br> OPTIONAL | Paginate through list of results |
| status<br> OPTIONAL | Filter results by order status |
| sku<br> OPTIONAL | Filter results by product SKU - response will contain only those orders that have at least one product with passed SKU |
| **Retrieve all orders**<br>`GET /v1/shops/{shop_id}/orders.json`<br>[View Response](https://developers.printify.com/#)`{<br>    "current_page": 1,<br>    "data": [<br>          {<br>            "id": "5a96f649b2439217d070f507",<br>            "app_order_id": "215014.44",<br>            "address_to": {<br>              "first_name": "John",<br>              "last_name": "Smith",<br>              "region": "",<br>              "address1": "ExampleBaan 121",<br>              "city": "Retie",<br>              "zip": "2470",<br>              "email": "example@msn.com",<br>              "phone": "0574 69 21 90",<br>              "country": "BE",<br>              "company": "MSN"<br>            },<br>            "line_items": [<br>              {<br>                "product_id": "5b05842f3921c9547531758d",<br>                "quantity": 1,<br>                "variant_id": 17887,<br>                "print_provider_id": 5,<br>                "cost": 1050,<br>                "shipping_cost": 400,<br>                "status": "fulfilled",<br>                "metadata": {<br>                  "title": "18K gold plated Necklace",<br>                  "price": 2200,<br>                  "variant_label": "Golden indigocoin",<br>                  "sku": "168699843",<br>                  "country": "United States"<br>                },<br>                "sent_to_production_at": "2017-04-18 13:24:28+00:00",<br>                "fulfilled_at": "2017-04-18 13:24:28+00:00"<br>              }<br>            ],<br>            "metadata": {<br>              "order_type": "external",<br>              "shop_order_id": 1370762297,<br>              "shop_order_label": "1370762297",<br>              "shop_fulfilled_at": "2017-04-18 13:24:28+00:00",<br>              "is_reprint": true,<br>              "reprinted_order_ids": ["6a72ef76c6503ada3c069ecc"],<br>              "child_reprinted_order_ids": ["6a72f40c351dc156610b500a"]<br>            },<br>            "total_price": 2200,<br>            "total_shipping": 400,<br>            "total_tax": 0,<br>            "status": "fulfilled",<br>            "shipping_method": 1,<br>            "is_printify_express": false,<br>            "is_economy_shipping": false,<br>            "shipments": [<br>              {<br>                "carrier": "usps",<br>                "number": "94001116990045395649372",<br>                "url": "http://example.com/94001116990045395649372",<br>                "delivered_at": "2017-04-18 13:24:28+00:00"<br>              }<br>            ],<br>            "created_at": "2017-04-18 13:24:28+00:00",<br>            "sent_to_production_at": "2017-04-18 13:24:28+00:00",<br>            "fulfilled_at": "2017-04-18 13:24:28+00:00",<br>            "printify_connect": {<br>              "url": "https://example.com/printify_connect_hash",<br>              "id": "printify_connect_hash"<br>            },<br>          }<br>      ]<br>}` |
| **Retrieve limited results**<br>`GET /v1/shops/{shop_id}/orders.json?limit=1`<br>[View Response](https://developers.printify.com/#)`{<br>    "current_page": 1,<br>    "data": [<br>          {<br>            "id": "5a6e03bd2f7d8055768923c8",<br>            "app_order_id": "215014.44",<br>            "address_to": {<br>              "first_name": "Jane",<br>              "last_name": "Smith",<br>              "region": "",<br>              "address1": "ExampleBaan 121",<br>              "city": "Retie",<br>              "zip": "2470",<br>              "email": "example@msn.com",<br>              "phone": "0574 69 21 90",<br>              "country": "BE",<br>              "company": "MSN"<br>            },<br>            "line_items": [<br>              {<br>                "product_id": "5b05842f3921c9547531758d",<br>                "quantity": 1,<br>                "variant_id": 17887,<br>                "print_provider_id": 5,<br>                "cost": 1050,<br>                "shipping_cost": 400,<br>                "status": "fulfilled",<br>                "metadata": {<br>                  "title": "18K gold plated Necklace",<br>                  "price": 2200,<br>                  "variant_label": "Golden indigocoin",<br>                  "sku": "168699843",<br>                  "country": "United States"<br>                },<br>                "sent_to_production_at": "2017-04-18 13:24:28+00:00",<br>                "fulfilled_at": "2017-04-18 13:24:28+00:00"<br>              }<br>            ],<br>            "metadata": {<br>              "order_type": "external",<br>              "shop_order_id": 1370762297,<br>              "shop_order_label": "1370762297",<br>              "shop_fulfilled_at": "2017-04-18 13:24:28+00:00",<br>              "is_reprint": true,<br>              "reprinted_order_ids": ["6a72ef76c6503ada3c069ecc"],<br>              "child_reprinted_order_ids": ["6a72f40c351dc156610b500a"]<br>            },<br>            "total_price": 2200,<br>            "total_shipping": 400,<br>            "total_tax": 0,<br>            "status": "fulfilled",<br>            "shipping_method": 1,<br>            "is_printify_express": false,<br>            "is_economy_shipping": false,<br>            "shipments": [<br>              {<br>                "carrier": "usps",<br>                "number": "94001116990045395649372",<br>                "url": "http://example.com/94001116990045395649372",<br>                "delivered_at": "2017-04-18 13:24:28+00:00"<br>              }<br>            ],<br>            "created_at": "2017-04-18 13:24:28+00:00",<br>            "sent_to_production_at": "2017-04-18 13:24:28+00:00",<br>            "fulfilled_at": "2017-04-18 13:24:28+00:00"<br>            "printify_connect": {<br>              "url": "https://example.com/printify_connect_hash",<br>              "id": "printify_connect_hash"<br>            },<br>          }<br>      ]<br>}` |
| **Retrieve specific page from results.**<br>`GET /v1/shops/{shop_id}/orders.json?page=2`<br>[View Response](https://developers.printify.com/#)`{<br>    "current_page": 2,<br>    "data": [<br>          {<br>            "id": "5a6e03bd2f7d8055768923c8",<br>            "app_order_id": "215014.44",<br>            "address_to": {<br>              "first_name": "Jack",<br>              "last_name": "Smith",<br>              "region": "",<br>              "address1": "ExampleBaan 121",<br>              "city": "A city",<br>              "zip": "4321",<br>              "email": "example@msn.com",<br>              "phone": "0574 69 21 90",<br>              "country": "SW",<br>              "company": "MSN"<br>            },<br>            "line_items": [<br>              {<br>                "product_id": "5b05842f3921c9547531758d",<br>                "quantity": 1,<br>                "variant_id": 17887,<br>                "print_provider_id": 5,<br>                "cost": 1050,<br>                "shipping_cost": 400,<br>                "status": "fulfilled",<br>                "metadata": {<br>                  "title": "18K gold plated Necklace",<br>                  "price": 2200,<br>                  "variant_label": "Golden indigocoin",<br>                  "sku": "168699843",<br>                  "country": "United States"<br>                },<br>                "sent_to_production_at": "2017-04-18 13:24:28+00:00",<br>                "fulfilled_at": "2017-04-18 13:24:28+00:00"<br>              }<br>            ],<br>            "metadata": {<br>              "order_type": "external",<br>              "shop_order_id": 1370762297,<br>              "shop_order_label": "1370762297",<br>              "shop_fulfilled_at": "2017-04-18 13:24:28+00:00",<br>              "is_reprint": true,<br>              "reprinted_order_ids": ["6a72ef76c6503ada3c069ecc"],<br>              "child_reprinted_order_ids": ["6a72f40c351dc156610b500a"]<br>            },<br>            "total_price": 2200,<br>            "total_shipping": 400,<br>            "total_tax": 0,<br>            "status": "fulfilled",<br>            "shipping_method": 1,<br>            "is_printify_express": false,<br>            "is_economy_shipping": false,<br>            "shipments": [<br>              {<br>                "carrier": "usps",<br>                "number": "94001116990045395649372",<br>                "url": "http://example.com/94001116990045395649372",<br>                "delivered_at": "2017-04-18 13:24:28+00:00"<br>              }<br>            ],<br>            "created_at": "2017-04-18 13:24:28+00:00",<br>            "sent_to_production_at": "2017-04-18 13:24:28+00:00",<br>            "fulfilled_at": "2017-04-18 13:24:28+00:00"<br>            "printify_connect": {<br>              "url": "https://example.com/printify_connect_hash",<br>              "id": "printify_connect_hash"<br>            },<br>          }<br>      ]<br>}` |
| **Filter results by order status.**<br>`GET /v1/shops/{shop_id}/orders.json?status=fulfilled`<br>[View Response](https://developers.printify.com/#)`{<br>    "current_page": 2,<br>    "data": [<br>          {<br>            "id": "5a6e03bd2f7d8055768923c8",<br>            "app_order_id": "215014.44",<br>            "address_to": {<br>              "first_name": "John",<br>              "last_name": "Smith",<br>              "region": "",<br>              "address1": "ExampleBaan 121",<br>              "city": "A city",<br>              "zip": "4321",<br>              "email": "example@msn.com",<br>              "phone": "0574 69 21 90",<br>              "country": "SW",<br>              "company": "MSN"<br>            },<br>            "line_items": [<br>              {<br>                "product_id": "5b05842f3921c9547531758d",<br>                "quantity": 1,<br>                "variant_id": 17887,<br>                "print_provider_id": 5,<br>                "cost": 1050,<br>                "shipping_cost": 400,<br>                "status": "fulfilled",<br>                "metadata": {<br>                  "title": "18K gold plated Necklace",<br>                  "price": 2200,<br>                  "variant_label": "Golden indigocoin",<br>                  "sku": "168699843",<br>                  "country": "United States"<br>                },<br>                "sent_to_production_at": "2017-04-18 13:24:28+00:00",<br>                "fulfilled_at": "2017-04-18 13:24:28+00:00"<br>              }<br>            ],<br>            "metadata": {<br>              "order_type": "external",<br>              "shop_order_id": 1370762297,<br>              "shop_order_label": "1370762297",<br>              "shop_fulfilled_at": "2017-04-18 13:24:28+00:00",<br>              "is_reprint": true,<br>              "reprinted_order_ids": ["6a72ef76c6503ada3c069ecc"],<br>              "child_reprinted_order_ids": ["6a72f40c351dc156610b500a"]<br>            },<br>            "total_price": 2200,<br>            "total_shipping": 400,<br>            "total_tax": 0,<br>            "status": "fulfilled",<br>            "shipping_method": 1,<br>            "is_printify_express": false,<br>            "is_economy_shipping": false,<br>            "shipments": [<br>              {<br>                "carrier": "usps",<br>                "number": "94001116990045395649372",<br>                "url": "http://example.com/94001116990045395649372",<br>                "delivered_at": "2017-04-18 13:24:28+00:00"<br>              }<br>            ],<br>            "created_at": "2017-04-18 13:24:28+00:00",<br>            "sent_to_production_at": "2017-04-18 13:24:28+00:00",<br>            "fulfilled_at": "2017-04-18 13:24:28+00:00"<br>            "printify_connect": {<br>              "url": "https://example.com/printify_connect_hash",<br>              "id": "printify_connect_hash"<br>            },<br>          }<br>      ]<br>}` |
| **Filter results by product SKU.**<br>`GET /v1/shops/{shop_id}/orders.json?sku=168699843`<br>[View Response](https://developers.printify.com/#)`{<br>    "current_page": 2,<br>    "data": [<br>          {<br>            "id": "5a6e03bd2f7d8055768923c8",<br>            "app_order_id": "215014.44",<br>            "address_to": {<br>              "first_name": "John",<br>              "last_name": "Smith",<br>              "region": "",<br>              "address1": "ExampleBaan 121",<br>              "city": "A city",<br>              "zip": "4321",<br>              "email": "example@msn.com",<br>              "phone": "0574 69 21 90",<br>              "country": "SW",<br>              "company": "MSN"<br>            },<br>            "line_items": [<br>              {<br>                "product_id": "5b05842f3921c9547531758d",<br>                "quantity": 1,<br>                "variant_id": 17887,<br>                "print_provider_id": 5,<br>                "cost": 1050,<br>                "shipping_cost": 400,<br>                "status": "fulfilled",<br>                "metadata": {<br>                  "title": "18K gold plated Necklace",<br>                  "price": 2200,<br>                  "variant_label": "Golden indigocoin",<br>                  "sku": "168699843",<br>                  "country": "United States"<br>                },<br>                "sent_to_production_at": "2017-04-18 13:24:28+00:00",<br>                "fulfilled_at": "2017-04-18 13:24:28+00:00"<br>              }<br>            ],<br>            "metadata": {<br>              "order_type": "external",<br>              "shop_order_id": 1370762297,<br>              "shop_order_label": "1370762297",<br>              "shop_fulfilled_at": "2017-04-18 13:24:28+00:00",<br>              "is_reprint": true,<br>              "reprinted_order_ids": ["6a72ef76c6503ada3c069ecc"],<br>              "child_reprinted_order_ids": ["6a72f40c351dc156610b500a"]<br>            },<br>            "total_price": 2200,<br>            "total_shipping": 400,<br>            "total_tax": 0,<br>            "status": "fulfilled",<br>            "shipping_method": 1,<br>            "is_printify_express": false,<br>            "is_economy_shipping": false,<br>            "shipments": [<br>              {<br>                "carrier": "usps",<br>                "number": "94001116990045395649372",<br>                "url": "http://example.com/94001116990045395649372",<br>                "delivered_at": "2017-04-18 13:24:28+00:00"<br>              }<br>            ],<br>            "created_at": "2017-04-18 13:24:28+00:00",<br>            "sent_to_production_at": "2017-04-18 13:24:28+00:00",<br>            "fulfilled_at": "2017-04-18 13:24:28+00:00"<br>            "printify_connect": {<br>              "url": "https://example.com/printify_connect_hash",<br>              "id": "printify_connect_hash"<br>            },<br>          }<br>      ]<br>}` |

#### Get order details by ID

|     |     |
| --- | --- |
| GET | /v1/shops/{shop\_id}/orders/{order\_id}.json |
| **Get order details by ID**<br>`GET /v1/shops/{shop_id}/orders/{order_id}.json`<br>[View Response](https://developers.printify.com/#)`{<br>      "id": "5a96f649b2439217d070f507",<br>      "app_order_id": "215014.44",<br>      "address_to": {<br>        "first_name": "John",<br>        "last_name": "Smith",<br>        "region": "",<br>        "address1": "ExampleBaan 121",<br>        "city": "Retie",<br>        "zip": "2470",<br>        "email": "example@msn.com",<br>        "phone": "0574 69 21 90",<br>        "country": "BE",<br>        "company": "MSN"<br>      },<br>      "line_items": [<br>        {<br>          "product_id": "5b05842f3921c9547531758d",<br>          "quantity": 1,<br>          "variant_id": 17887,<br>          "print_provider_id": 5,<br>          "cost": 1050,<br>          "shipping_cost": 400,<br>          "status": "fulfilled",<br>          "metadata": {<br>            "title": "18K gold plated Necklace",<br>            "price": 2200,<br>            "variant_label": "Golden indigocoin",<br>            "sku": "168699843",<br>            "country": "United States",<br>            "external_id": "line-item-abc-001"<br>          },<br>          "sent_to_production_at": "2017-04-18 13:24:28+00:00",<br>          "fulfilled_at": "2017-04-18 13:24:28+00:00"<br>        }<br>      ],<br>      "metadata": {<br>        "order_type": "external",<br>        "shop_order_id": 1370762297,<br>        "shop_order_label": "1370762297",<br>        "shop_fulfilled_at": "2017-04-18 13:24:28+00:00",<br>        "is_reprint": true,<br>        "reprinted_order_ids": ["6a72ef76c6503ada3c069ecc"],<br>        "child_reprinted_order_ids": ["6a72f40c351dc156610b500a"]<br>      },<br>      "total_price": 2200,<br>      "total_shipping": 400,<br>      "total_tax": 0,<br>      "status": "fulfilled",<br>      "shipping_method": 1,<br>      "is_printify_express": false,<br>      "is_economy_shipping": false,<br>      "shipments": [<br>        {<br>          "carrier": "usps",<br>          "number": "94001116990045395649372",<br>          "url": "http://example.com/94001116990045395649372",<br>          "delivered_at": "2017-04-18 13:24:28+00:00"<br>        }<br>      ],<br>      "created_at": "2017-04-18 13:24:28+00:00",<br>      "sent_to_production_at": "2017-04-18 13:24:28+00:00",<br>      "fulfilled_at": "2017-04-18 13:24:28+00:00"<br>      "printify_connect": {<br>        "url": "https://example.com/printify_connect_hash",<br>        "id": "printify_connect_hash"<br>      },<br>}` |

#### Submit an order

|     |     |
| --- | --- |
| POST | /v1/shops/{shop\_id}/orders.json |
| **Order an existing product**<br>`POST /v1/shops/{shop_id}/orders.json`<br>`{<br>    "external_id": "2750e210-39bb-11e9-a503-452618153e4a",<br>    "label": "00012",<br>    "line_items": [<br>      {<br>        "product_id": "5bfd0b66a342bcc9b5563216",<br>        "variant_id": 17887,<br>        "quantity": 1,<br>        "external_id": "line-item-abc-001"<br>      }<br>    ],<br>    "shipping_method": 1,<br>    "is_printify_express": false,<br>    "is_economy_shipping": false,<br>    "send_shipping_notification": false,<br>    "address_to": {<br>      "first_name": "John",<br>      "last_name": "Smith",<br>      "email": "example@msn.com",<br>      "phone": "0574 69 21 90",<br>      "country": "BE",<br>      "region": "",<br>      "address1": "ExampleBaan 121",<br>      "address2": "45",<br>      "city": "Retie",<br>      "zip": "2470"<br>    }<br>  }<br>` [View Response](https://developers.printify.com/#)`{<br>          "id": "5a96f649b2439217d070f507"<br>}` |
| **Create a product with an order (simple image positioning)**<br>`POST /v1/shops/{shop_id}/orders.json`<br>`{<br>    "external_id": "2750e210-39bb-11e9-a503-452618153e5a",<br>    "label": "00012",<br>    "line_items": [<br>      {<br>        "print_provider_id": 5,<br>        "blueprint_id": 9,<br>        "variant_id": 17887,<br>        "print_areas": {<br>          "front": "https://images.example.com/image.png"<br>        },<br>        "quantity": 1,<br>        "external_id": "line-item-abc-001"<br>      }<br>    ],<br>    "shipping_method": 1,<br>    "is_printify_express": false,<br>    "is_economy_shipping": false,<br>    "send_shipping_notification": false,<br>    "address_to": {<br>      "first_name": "John",<br>      "last_name": "Smith",<br>      "email": "example@msn.com",<br>      "phone": "0574 69 21 90",<br>      "country": "BE",<br>      "region": "",<br>      "address1": "ExampleBaan 121",<br>      "address2": "45",<br>      "city": "Retie",<br>      "zip": "2470"<br>    }<br>  }` [View Response](https://developers.printify.com/#)`{<br>          "id": "5a96f649b2439217d070f508"<br>}` |
| **Create a product with an order (advanced image positioning)**<br>`POST /v1/shops/{shop_id}/orders.json`<br>`{<br>    "external_id": "2750e210-39bb-11e9-a503-452618153e5a",<br>    "label": "00012",<br>    "line_items": [<br>      {<br>        "print_provider_id": 5,<br>        "blueprint_id": 9,<br>        "variant_id": 17887,<br>        "print_areas": {<br>          "front": [<br>            {<br>                "src": "https://images.example.com/image.png",<br>                "scale": 0.15,<br>                "x": 0.80,<br>                "y": 0.34,<br>                "angle": 0.34<br>            },<br>            {<br>                "src": "https://images.example.com/image.png",<br>                "scale": 1,<br>                "x": 0.5,<br>                "y": 0.5,<br>                "angle": 1<br>            }<br>          ]<br>        },<br>        "quantity": 1<br>      }<br>    ],<br>    "shipping_method": 1,<br>    "is_printify_express": false,<br>    "is_economy_shipping": false,<br>    "send_shipping_notification": false,<br>    "address_to": {<br>      "first_name": "John",<br>      "last_name": "Smith",<br>      "email": "example@msn.com",<br>      "phone": "0574 69 21 90",<br>      "country": "BE",<br>      "region": "",<br>      "address1": "ExampleBaan 121",<br>      "address2": "45",<br>      "city": "Retie",<br>      "zip": "2470"<br>    }<br>  }` [View Response](https://developers.printify.com/#)`{<br>          "id": "5a96f649b2439217d070f508"<br>}` |
| **Create a product with an order (with specifying print details for printing on sides)**<br>`POST /v1/shops/{shop_id}/orders.json`<br>`<br>    {<br>        "external_id": "2750e210-39bb-11e9-a503-452618153e5a",<br>        "label": "00012",<br>        "line_items": [<br>          {<br>            "print_provider_id": 5,<br>            "blueprint_id": 9,<br>            "variant_id": 17887,<br>            "print_areas": {<br>              "front": "https://images.example.com/image.png"<br>            },<br>            "print_details": {<br>                "print_on_side": "mirror"<br>            },<br>            "quantity": 1,<br>            "external_id": "line-item-abc-001"<br>          }<br>        ],<br>        "shipping_method": 1,<br>        "is_printify_express": false,<br>        "is_economy_shipping": false,<br>        "send_shipping_notification": false,<br>        "address_to": {<br>          "first_name": "John",<br>          "last_name": "Smith",<br>          "email": "example@msn.com",<br>          "phone": "0574 69 21 90",<br>          "country": "BE",<br>          "region": "",<br>          "address1": "ExampleBaan 121",<br>          "address2": "45",<br>          "city": "Retie",<br>          "zip": "2470"<br>    }<br>  }` [View Response](https://developers.printify.com/#)`{<br>          "id": "5a96f649b2439217d070f508"<br>}` |
| **Order an existing product using only an SKU**<br>`POST /v1/shops/{shop_id}/orders.json`<br>`"external_id": "2750e210-39bb-11e9-a503-452618153e6a",<br>    "label": "00012",<br>    "line_items": [<br>      {<br>        "sku": "MY-SKU",<br>        "quantity": 1<br>      }<br>    ],<br>    "shipping_method": 1,<br>    "is_printify_express": false,<br>    "is_economy_shipping": false,<br>    "send_shipping_notification": false,<br>    "address_to": {<br>      "first_name": "John",<br>      "last_name": "Smith",<br>      "email": "example@msn.com",<br>      "phone": "0574 69 21 90",<br>      "country": "BE",<br>      "region": "",<br>      "address1": "ExampleBaan 121",<br>      "address2": "45",<br>      "city": "Retie",<br>      "zip": "2470"<br>    }<br>}` [View Response](https://developers.printify.com/#)`{<br>          "id": "5a96f649b2439217d070f509"<br>}` |

#### Submit a Printify Express order

|     |     |
| --- | --- |
| POST | /v1/shops/{shop\_id}/orders/express.json |
| **Order an existing product with Printify Express Delivery**

This API method creates one or two separate orders using the following logic:


1. If **none** of the line items are Printify Express eligible: one order with `"fulfilment_type": "ordinary"`
2. If **all** of the line items are Printify Express eligible: one order with `"fulfilment_type": "express"`
3. If at least one line item is Printify Express eligible, and at least one isn't: two separate orders, one `express`, and one `ordinary`

Read more about Printify Express Delivery in [a dedicated Help center section](https://help.printify.com/hc/en-us/sections/9116968124689-Printify-Express-Delivery).


|     |     |
| --- | --- |
| ⚠ | `address_to.email` and `address_to.phone` fields are required for Printify Express eligibility. |

|     |     |
| --- | --- |
| ⚠ | The endpoint works only with already existing products.<br>Please be aware that Printify Express Delivery is using carriers that might not be supported by all sales channels (e.g. Amazon, Tik Tok). |

|     |     |
| --- | --- |
| ⚠ | Please be aware that only the [Product's](https://developers.printify.com/#product-properties) and the [Variant's](https://developers.printify.com/#product-variant-properties) eligibility (`is_printify_express_eligible` flag) is taken into account. Eligible but disabled products (`is_printify_express_enabled` flag) can still be ordered with [Printify Express Delivery](https://help.printify.com/hc/en-us/sections/9116968124689-Printify-Express-Delivery). |

`POST /v1/shops/{shop_id}/orders/express.json`

`{
"external_id": "2750e210-39bb-11e9-a503-452618153e4a",
"label": "00012",
"line_items": [\
    {\
      "product_id": "5b05842f3921c9547531758d",\
      "variant_id": 12359,\
      "quantity": 1\
    },\
    {\
      "product_id": "5b05842f3921c34764fa478bc",\
      "variant_id": 17887,\
      "quantity": 1\
    }\
],
"shipping_method": 3,
"send_shipping_notification": false,
"address_to": {
    "first_name": "John",
    "last_name": "Smith",
    "email": "example@example.com",
    "phone": "0574 69 21 90",
    "country": "BE",
    "region": "",
    "address1": "ExampleBaan 121",
    "address2": "45",
    "city": "Retie",
    "zip": "2470"
}
}` [View Response](https://developers.printify.com/#)`{
"data": [\
    {\
      "type": "order",\
      "id": "5a96f649b2439217d070f508",\
      "attributes": {\
        "app_order_id": "215014.44",\
        "fulfilment_type": "express",\
        "line_items": [\
          {\
            "product_id": "5b05842f3921c9547531758d",\
            "quantity": 1,\
            "variant_id": 12359,\
            "print_provider_id": 5,\
            "cost": 2200,\
            "shipping_cost": 799,\
            "status": "pending",\
            "metadata": {\
              "title": "T-shirt",\
              "price": 2200,\
              "variant_label": "Blue / S",\
              "sku": "168699843",\
              "country": "United States"\
            },\
            "sent_to_production_at": "2023-10-18 13:24:28+00:00",\
            "fulfilled_at": null\
          }\
        ]\
      }\
    },\
    {\
      "type": "order",\
      "id": "5a96f649b2439597d020a9b4",\
      "attributes": {\
        "fulfilment_type": "ordinary",\
        "line_items": [\
          {\
            "product_id": "5b05842f3921c34764fa478bc",\
            "quantity": 1,\
            "variant_id": 17887,\
            "print_provider_id": 5,\
            "cost": 1050,\
            "shipping_cost": 400,\
            "status": "pending",\
            "metadata": {\
              "title": "Mug 11oz",\
              "price": 1050,\
              "variant_label": "11oz",\
              "sku": "168699843",\
              "country": "United States"\
            },\
            "sent_to_production_at": "2023-10-18 13:24:28+00:00",\
            "fulfilled_at": null\
          }\
        ]\
      }\
    }\
]
}` |

#### Send an existing order to production

|     |     |
| --- | --- |
| POST | /v1/shops/{shop\_id}/orders/{order\_id}/send\_to\_production.json |
| **Send an existing order to production**<br>`POST /v1/shops/{shop_id}/orders/{order_id}/send_to_production.json`<br>[View Response](https://developers.printify.com/#)`{<br>          "id": "5a96f649b2439217d070f507"<br>    }` |

#### Calculate the shipping cost of an order

| POST | /v1/shops/{shop\_id}/orders/shipping.json |
| **Calculate the shipping cost of an order**

`POST /v1/shops/{shop_id}/orders/shipping.json`

`{
    "line_items": [{\
        "product_id": "5bfd0b66a342bcc9b5563216",\
        "variant_id": 17887,\
        "quantity": 1,\
        "external_id": "line-item-abc-001"\
    },{\
        "print_provider_id": 5,\
        "blueprint_id": 9,\
        "variant_id": 17887,\
        "quantity": 1,\
        "external_id": "line-item-abc-001"\
    },{\
        "sku": "MY-SKU",\
        "quantity": 1,\
        "external_id": "line-item-abc-001"\
    }],
    "address_to": {
        "first_name": "John",
        "last_name": "Smith",
        "email": "example@msn.com",
        "phone": "0574 69 21 90",
        "country": "BE",
        "region": "",
        "address1": "ExampleBaan 121",
        "address2": "45",
        "city": "Retie",
        "zip": "2470"
    }
}
`

Response

`
{
    "standard": 1000,
    "express": 5000,
    "priority": 5000,
    "printify_express": 799,
    "economy": 399
}
`

Response contains the shipping options that are defined in the following table:

| Code | Old version | Transitional version \[active\] | Final version |
| --- | --- | --- | --- |
| 1 | standard | standard | standard |
| 2 | express | express<br>priority | priority |
| 3 |  | printify\_express | express |
| 4 | economy | economy | economy |

The **printify\_express** is a new shipping option that will later in the future change its name to the **express**. Current **express** option will be renamed to the **priority** name. |

#### Cancel an order

This request will only be accepted if the order to be canceled has the status "on-hold" or "payment-not-received".

|     |     |
| --- | --- |
| POST | /v1/shops/{shop\_id}/orders/{order\_id}/cancel.json |
| **Cancel an order**<br>`POST /v1/shops/{shop_id}/orders/{order_id}/cancel.json`<br>[View Response](https://developers.printify.com/#)`{<br>    "id": "5dee261dc400914833007902",<br>    "app_order_id": "215014.44",<br>    "address_to": {<br>        "first_name": "John",<br>        "last_name": "Smith",<br>        "email": "example@msn.com",<br>        "country": "United States",<br>        "region": "CA",<br>        "address1": "31677 Virginia Way",<br>        "city": "Laguna Beach",<br>        "zip": "92653"<br>    },<br>    "line_items": [<br>        {<br>            "quantity": 1,<br>            "product_id": "5de6593ebff03b5313567d22",<br>            "variant_id": 34509,<br>            "print_provider_id": 6,<br>            "shipping_cost": 450,<br>            "cost": 0,<br>            "status": "canceled",<br>            "metadata": {<br>                "title": "Men's Organic Tee - Product 1",<br>                "variant_label": "S / Red",<br>                "sku": "3640",<br>                "country": "United Kingdom"<br>            }<br>        }<br>    ],<br>    "metadata": {<br>        "order_type": "api",<br>        "shop_order_id": "2750e210-39bb-11e9-a503-452618153e4a",<br>        "shop_order_label": "2750e210-39bb-11e9-a503-452618153e4a",<br>        "shop_fulfilled_at": "1970-01-01 00:00:00+00:00",<br>        "is_reprint": true,<br>        "reprinted_order_ids": ["6a72ef76c6503ada3c069ecc"],<br>        "child_reprinted_order_ids": ["6a72f40c351dc156610b500a"]<br>    },<br>    "total_price": 0,<br>    "total_shipping": 0,<br>    "total_tax": 0,<br>    "status": "canceled",<br>    "shipping_method": 1,<br>    "is_printify_express": false,<br>    "is_economy_shipping": false,<br>    "created_at": "2019-12-09 10:46:53+00:00"<br>}` |

### Structure

Structure of Orders resource with possible transitions between endpoints.

![orders structure](https://developers.printify.com/images/OrdersStructure-9ccc7b1a.png)

### Making Order

Flow of transitions between resources for making an order.

![making order](https://developers.printify.com/images/MakingOrder-1a3f539b.png)

### Common error cases

|     |     |
| --- | --- |
| POST | /v1/shops/{shop\_id}/orders.json |
| **Common error cases**<br>`POST /v1/shops/{shop_id}/orders.json`<br>400 Invalid address validation error example (See HTTP Status Codes below) [View Response](https://developers.printify.com/#)`{<br>    "status": "error",<br>    // Exact error codes and messages are subject to change.<br>    "code": 8103,<br>    "message": "Validation failed.",<br>    "errors": {<br>      "reason": "{\"zip\":[\"The zip field is required.\"]}",<br>      "code": 8103<br>    }<br>}` |

## Personalization

The personalization resource lets you configure custom, per-buyer options for a product — such as custom text or
an uploaded photo — and generate mockup previews of the personalized product before it's added to an order. Use it
to build an on-site personalization experience (e.g. "Add your name", "Upload your photo") ahead of checkout.

On this page:

- [What you can do with the personalization resource](https://developers.printify.com/#what-you-can-do-with-the-personalization-resource)
- [Personalization option properties](https://developers.printify.com/#personalization-option-properties)
- [Personalization preview task properties](https://developers.printify.com/#personalization-preview-task-properties)
- [Endpoints](https://developers.printify.com/#personalization-endpoints)

### What you can do with the personalization resource

- [GET /v1/shops/{shop\_id}/products/{product\_id}/personalization\_options.json](https://developers.printify.com/#retrieve-personalization-options)

Retrieve the personalization fields configured for a product
- [POST /v1/shops/{shop\_id}/products/{product\_id}/personalization.json](https://developers.printify.com/#create-a-personalization-configuration)

Create a personalization configuration for a product variant
- [POST /v1/shops/{shop\_id}/products/{product\_id}/personalization\_previews.json](https://developers.printify.com/#request-a-personalization-preview)

Request rendered mockup previews for a personalization input
- [GET /v1/shops/{shop\_id}/products/{product\_id}/personalization\_previews/tasks/{task\_id}.json](https://developers.printify.com/#retrieve-a-personalization-preview-task-status)

Check the status of a personalization preview task

### Personalization option properties

|     |     |
| --- | --- |
| field\_id<br> READ-ONLY | `"field_id": "front_text"`<br> A unique string identifier for the personalization field. Use this value when submitting personalization input. |
| label<br> READ-ONLY | `"label": "Front text"`<br> A human-readable label for the field, suitable for displaying in a buyer-facing form. |
| type<br> READ-ONLY | `"type": "textbox"`<br> The kind of input this field accepts. Possible values are `"image"` for a photo upload field and<br> `"textbox"` for a free-text field. |
| text\_options<br> OPTIONAL | `"text_options": { "character_limit": 40 }`<br> Present only when `type` is `"textbox"`. Contains a `character_limit`<br> describing the maximum number of characters accepted for this field. |

### Personalization preview task properties

Requesting a personalization preview queues an asynchronous task. Poll the task status endpoint, or subscribe to
the `personalization-preview-task:processed` webhook event (see [Personalization events](https://developers.printify.com/#personalization-events)),
to find out when it's done.

|     |     |
| --- | --- |
| task\_id<br> READ-ONLY | `"task_id": "e12eb4c7-c3bd-4ce5-8dad-d782e9450708"`<br> A unique identifier for the preview task. |
| status<br> READ-ONLY | `"status": "completed"`<br> The current state of the task. See [task status reference](https://developers.printify.com/#personalization-preview-task-status-reference) below. |
| preview\_count<br> OPTIONAL | `"preview_count": 2`<br> Present when `status` is `"completed"`. The number of mockups generated for this task. |
| mockups<br> OPTIONAL | `"mockups": [<br>    {<br>      "variant_id": 38191,<br>      "mockup_id": "Front",<br>      "src": "https://dsaujk5puqrkx.cloudfront.net/buyer-preview/145/buyer-preview/38191/97992/4715046825664400772_2048.jpeg"<br>    }<br>]`<br> Present only when `status` is `"completed"`. An array of rendered mockups, one per<br> variant/view combination. `mockup_id` labels which view is shown (e.g. `"Front"`, `"Back"`). |
| error<br> OPTIONAL | Present only when `status` is `"failed"` or `"corrupt"`.<br> For `"failed"`, `message` is a generic, non-sensitive description of the stage that failed — safe to retry:<br> `"error": { "message": "Designer API request failed", "code": 500 }`<br> For `"corrupt"`, `message` describes the actual problem with the input — retrying with the same input will not help:<br> `"error": { "message": "Requested variant_id \"99999999\" does not exist on this product.", "code": 422 }` |

#### Task status reference

|     |     |
| --- | --- |
| `pending` | The task is queued and has not started processing yet. |
| `processing` | A worker has picked up the task and is generating previews. |
| `completed` | Previews were generated successfully. See `mockups`. |
| `failed` | A transient error occurred while generating previews. The task can be retried by submitting the same request again. |
| `corrupt` | The personalization input was invalid or misconfigured. This is terminal and will not be retried. |

### Endpoints

#### Retrieve personalization options

|     |     |
| --- | --- |
| ⚠ | This endpoint requires `{shop_id}` and `{product_id}` parameters. See [Retrieving Shop ID](https://developers.printify.com/#retrieving-shop-id) for instructions on how to obtain your shop ID. |

|     |     |
| --- | --- |
| GET | /v1/shops/{shop\_id}/products/{product\_id}/personalization\_options.json |
| **Retrieve the personalization fields configured for a product**<br>`GET /v1/shops/{shop_id}/products/{product_id}/personalization_options.json`<br>[View Response](https://developers.printify.com/#)`[<br>    {<br>      "field_id": "front_text",<br>      "label": "Front text",<br>      "type": "textbox",<br>      "text_options": { "character_limit": 40 }<br>    },<br>    {<br>      "field_id": "back_image",<br>      "label": "Back image",<br>      "type": "image"<br>    }<br>]` |

**Error codes**

| Status | Description |
| --- | --- |
| 400 | Validation failed. See the `errors` object in the response for details. |

#### Create a personalization configuration

Configures personalization for a product variant before it's added to an order (e.g. selecting a manual
personalization strategy or a Personalization Studio configuration). The `personalisation_strategy` and
`personalisation_instructions` returned below are then passed into an order line item — see
[personalisation properties](https://developers.printify.com/#personalisation-properties) for reference.

|     |     |
| --- | --- |
| ⚠ | This endpoint requires `{shop_id}` and `{product_id}` parameters. See [Retrieving Shop ID](https://developers.printify.com/#retrieving-shop-id) for instructions on how to obtain your shop ID. |

|     |     |
| --- | --- |
| POST | /v1/shops/{shop\_id}/products/{product\_id}/personalization.json |
| **Create a personalization configuration**<br>`POST /v1/shops/{shop_id}/products/{product_id}/personalization.json`<br> Request body:<br> `{<br>    "variant_id": 17887,<br>    "items": [<br>        {<br>            "field_id": "front_text",<br>            "type": "textbox",<br>            "input": { "text": "Happy Birthday!" }<br>        }<br>    ]<br>}` [View Response](https://developers.printify.com/#)`{<br>    "personalisation_strategy": "pstudio_pre_order_headless",<br>    "personalisation_instructions": "3fa85f64-5717-4562-b3fc-2c963f66afa6"<br>}` |

Attach this response's `personalisation_strategy` and `personalisation_instructions` to a `personalisation` object on
the order line item — see [personalisation properties](https://developers.printify.com/#personalisation-properties) for reference.

**Error codes**

| Status | Description |
| --- | --- |
| 400 | Validation failed. See the `errors` object in the response for details. |
| 503 | The personalization service is temporarily unavailable. |

#### Request a personalization preview

Queues an asynchronous task that renders mockup previews for the given personalization input. Poll the returned
`task_id` via the [task status endpoint](https://developers.printify.com/#retrieve-a-personalization-preview-task-status), or subscribe to the
`personalization-preview-task:processed` webhook event (see [Personalization events](https://developers.printify.com/#personalization-events)),
to retrieve the rendered mockups.

|     |     |
| --- | --- |
| ⚠ | This endpoint requires `{shop_id}` and `{product_id}` parameters. See [Retrieving Shop ID](https://developers.printify.com/#retrieving-shop-id) for instructions on how to obtain your shop ID. |

|     |     |
| --- | --- |
| POST | /v1/shops/{shop\_id}/products/{product\_id}/personalization\_previews.json |
| **Request a personalization preview**<br>`POST /v1/shops/{shop_id}/products/{product_id}/personalization_previews.json`<br> Request body:<br> `{<br>    "external_id": "preview-abc-001",<br>    "variant_ids": [17887],<br>    "personalization": [<br>        {<br>            "field_id": "front_text",<br>            "type": "textbox",<br>            "input": { "text": "Happy Birthday!" }<br>        }<br>    ]<br>}` [View Response](https://developers.printify.com/#)`{<br>    "task_id": "e12eb4c7-c3bd-4ce5-8dad-d782e9450708",<br>    "status": "pending",<br>    "external_id": "preview-abc-001"<br>}` |

**Error codes**

| Status | Description |
| --- | --- |
| 400 | Validation failed. See the `errors` object in the response for details. |
| 403 | Forbidden. Personalization previews are not enabled for this shop. |
| 422 | An unknown `field_id` or `variant_id` was supplied. |
| 503 | The personalization service is temporarily unavailable. |

#### Retrieve a personalization preview task status

|     |     |
| --- | --- |
| ⚠ | This endpoint requires `{shop_id}`, `{product_id}` and `{task_id}` parameters. See [Retrieving Shop ID](https://developers.printify.com/#retrieving-shop-id) for instructions on how to obtain your shop ID. |

|     |     |
| --- | --- |
| GET | /v1/shops/{shop\_id}/products/{product\_id}/personalization\_previews/tasks/{task\_id}.json |
| **Retrieve a personalization preview task status**<br>`GET /v1/shops/{shop_id}/products/{product_id}/personalization_previews/tasks/{task_id}.json`<br>[View Response](https://developers.printify.com/#)`{<br>    "task_id": "e12eb4c7-c3bd-4ce5-8dad-d782e9450708",<br>    "status": "completed",<br>    "preview_count": 1,<br>    "mockups": [<br>        {<br>            "variant_id": 38191,<br>            "mockup_id": "Front",<br>            "src": "https://dsaujk5puqrkx.cloudfront.net/buyer-preview/145/buyer-preview/38191/97992/4715046825664400772_2048.jpeg"<br>        }<br>    ]<br>}` |

**Error codes**

| Status | Description |
| --- | --- |
| 403 | Forbidden. Personalization previews are not enabled for this shop. |
| 404 | Task not found. |

|     |     |
| --- | --- |
| ⚠ | This feature also emits a `personalization-preview-task:processed` webhook event when a preview task reaches a terminal state.<br> See [Personalization events](https://developers.printify.com/#personalization-events) for its payload. |

## Uploads

Artwork added to a Printify Product can be saved in the Media library to be reused on additional products.

You can use this API to directly add files to the media library, and later use image IDs when creating or modifying
products.

On this page:

- [What you can do with the uploads resource](https://developers.printify.com/#what-you-can-do-with-the-uploads-resource)
- [Image properties](https://developers.printify.com/#uploads-image-properties)
- [Endpoints](https://developers.printify.com/#uploads-endpoints)
- [Structure](https://developers.printify.com/#uploads-structure)
- [Common Error cases](https://developers.printify.com/#uploads-common-error-cases)

### What you can do with the uploads resource

The Printify Public API lets you do the following with the Uploads resource:

- [GET /v1/uploads.json](https://developers.printify.com/#retrieve-a-list-of-uploaded-images)

Retrieve a list of uploaded images
- [GET /v1/uploads/{image\_id}.json](https://developers.printify.com/#retrieve-an-uploaded-image-by-id)

Retrieve an uploaded image by id
- [POST /v1/uploads/images.json](https://developers.printify.com/#upload-an-image)

Upload an image
- [POST /v1/uploads/{image\_id}/archive.json](https://developers.printify.com/#archive-an-uploaded-image)

Archive an uploaded image

### Image properties

|     |     |
| --- | --- |
| id<br> READ-ONLY | `"id": "5e16d66791287a0006e522b2"`<br> A unique string identifier for the image. Each id is unique across the Printify system. |
| file\_name<br> READ-ONLY | `"file_name": "Image's file name"`<br> The file name of the image. |
| height<br> READ-ONLY | `"height": 5979`<br> The height of the image in pixels. |
| width<br> READ-ONLY | `"width": 17045`<br> The width of the image in pixels. |
| size<br> READ-ONLY | `"size": 1138575`<br> The file size of the image in bytes. |
| mime\_type<br> READ-ONLY | `"mime_type": "image/png"`<br> The media type of the image file. |
| preview\_url<br> READ-ONLY | `"preview_url": "https://example.com/artwork"`<br> A url to preview the image. |
| upload\_time<br> READ-ONLY | `"upload_time": "2020-01-09 07:29:43"`<br> The date and time the image was uploaded in ISO date format. |

### Endpoints

#### Retrieve a list of uploaded images

|     |     |
| --- | --- |
| GET | /v1/uploads.json |
| limit<br> OPTIONAL | Results per page<br>(default: 10, maximum: 100) |
| page<br> OPTIONAL | Paginate through list of results |
| **Retrieve all uploaded images**<br>`GET /v1/uploads.json`<br>[View Response](https://developers.printify.com/#)`{<br>    "current_page": 1,<br>    "data": [<br>        {<br>            "id": "5e16d66791287a0006e522b2",<br>            "file_name": "png-images-logo-1.jpg",<br>            "height": 5979,<br>            "width": 17045,<br>            "size": 1138575,<br>            "mime_type": "image/png",<br>            "preview_url": "https://example.com/image-storage/uuid1",<br>            "upload_time": "2020-01-09 07:29:43"<br>        },<br>        {<br>            "id": "5de50bf612c348000892b366",<br>            "file_name": "png-images-logo-2.jpg",<br>            "height": 360,<br>            "width": 360,<br>            "size": 19589,<br>            "mime_type": "image/jpeg",<br>            "preview_url": "https://example.com/image-storage/uuid2",<br>            "upload_time": "2019-12-02 13:04:54"<br>        }<br>    ],<br>    "first_page_url": "/?page=1",<br>    "from": 1,<br>    "last_page": 1,<br>    "last_page_url": "/?page=1",<br>    "next_page_url": null,<br>    "path": "/",<br>    "per_page": 10,<br>    "prev_page_url": null,<br>    "to": 2,<br>    "total": 2<br>}` |
| **Retrieve specific page from results**<br>`GET /v1/uploads.json?page=2`<br>[View Response](https://developers.printify.com/#)`{<br>    "current_page": 2,<br>    "data": [<br>        {<br>            "id": "5e16d66791287a0006e522b2",<br>            "file_name": "png-images-logo-1.jpg",<br>            "height": 5979,<br>            "width": 17045,<br>            "size": 1138575,<br>            "mime_type": "image/png",<br>            "preview_url": "https://example.com/image-storage/uuid1",<br>            "upload_time": "2020-01-09 07:29:43"<br>        },<br>        {<br>            "id": "5de50bf612c348000892b366",<br>            "file_name": "png-images-logo-2.jpg",<br>            "height": 360,<br>            "width": 360,<br>            "size": 19589,<br>            "mime_type": "image/jpeg",<br>            "preview_url": "https://example.com/image-storage/uuid2",<br>            "upload_time": "2019-12-02 13:04:54"<br>        }<br>    ],<br>    "first_page_url": "/?page=1",<br>    "from": 1,<br>    "last_page": 2,<br>    "last_page_url": "/?page=2",<br>    "next_page_url": null,<br>    "path": "/",<br>    "per_page": 10,<br>    "prev_page_url": 1,<br>    "to": 2,<br>    "total": 2<br>}` |
| **Retrieve limited results**<br>`GET /v1/uploads.json?limit=1`<br>[View Response](https://developers.printify.com/#)`{<br>    "current_page": 1,<br>    "data": [<br>        {<br>            "id": "5e16d66791287a0006e522b2",<br>            "file_name": "png-images-logo-1.jpg",<br>            "height": 5979,<br>            "width": 17045,<br>            "size": 1138575,<br>            "mime_type": "image/png",<br>            "preview_url": "https://example.com/image-storage/uuid1",<br>            "upload_time": "2020-01-09 07:29:43"<br>        }<br>    ],<br>    "first_page_url": "/?page=1",<br>    "from": 1,<br>    "last_page": 2,<br>    "last_page_url": "/?page=2",<br>    "next_page_url": /?page=2,<br>    "path": "/",<br>    "per_page": 1,<br>    "prev_page_url": null,<br>    "to": 2,<br>    "total": 2<br>}` |

#### Retrieve an uploaded image by id

|     |     |
| --- | --- |
| GET | /v1/uploads/{image\_id}.json |
| **Retrieve an uploaded image by id**<br>`GET /v1/uploads/{image_id}.json`<br>[View Response](https://developers.printify.com/#)`{<br>    "id": "5e16d66791287a0006e522b2",<br>    "file_name": "png-images-logo-1.jpg",<br>    "height": 5979,<br>    "width": 17045,<br>    "size": 1138575,<br>    "mime_type": "image/png",<br>    "preview_url": "https://example.com/image-storage/uuid1",<br>    "upload_time": "2020-01-09 07:29:43"<br>}` |

#### Upload an image

Upload image files either via image URL or image file base64-encoded contents. The file will be stored in the Merchant's account
Media Library.

|     |     |
| --- | --- |
| ⚠ | We highly recommend using upload via image URL for files larger than 5MB.<br> Upload via image URL is the future-proof solution, as we plan to drop support for base64-encoded content uploads larger than 5MB in the future. |

|     |     |
| --- | --- |
| POST | /v1/uploads/images.json |
| **Upload image to a Printify account's media library**<br>`POST /v1/uploads/images.json`Body parameter (upload image by URL)`{<br>    "file_name": "1x1-ff00007f.png",<br>    "url": "http://png-pixel.com/1x1-ff00007f.png"<br>}`Body parameter (upload image by base64-encoded contents)`{<br>    "file_name": "image.png",<br>    "contents": "base-64-encoded-content"<br>}` [View Response](https://developers.printify.com/#)`{<br>    "id": "5941187eb8e7e37b3f0e62e5",<br>    "file_name": "image.png",<br>    "height": 200,<br>    "width": 400,<br>    "size": 1021,<br>    "mime_type": "image/png",<br>    "preview_url": "https://example.com/image-storage/uuid3",<br>    "upload_time": "2020-01-09 07:29:43"<br>}` |

#### Archive an uploaded image

|     |     |
| --- | --- |
| POST | /v1/uploads/{image\_id}/archive.json |
| **Archive an uploaded image**<br>`POST /v1/uploads/{image_id}/archive.json`<br>[View Response](https://developers.printify.com/#)`{}` |

### Structure

Structure of Image Uploads resource with possible transitions between endpoints.

![uploads structure](https://developers.printify.com/images/UploadsStructure-40ee12f4.png)

### Common Error cases

When uploading images to the library, you may encounter errors. These are commonly due to download errors, incorrect file formats, or your image being too large. If these are the case, you will receive messages similar to these outlined here.

|     |     |
| --- | --- |
| POST | /v1/uploads/images.json |
| **Common error cases**<br>`POST /v1/uploads/images.json`400 Image download error example (See HTTP Status Codes below) [View Response](https://developers.printify.com/#)`{<br>    "status": "error",<br>    // Exact error codes and messages are subject to change.<br>    "code": 10300,<br>    "message": "Operation failed.",<br>    "errors": {<br>      "reason": "cURL error 6: Could not resolve host: png1-pixel.com",<br>      "code": 10300<br>    }<br>}`<br>400 Image too large error example (See HTTP Status Codes below) [View Response](https://developers.printify.com/#)`{<br>    "status": "error",<br>    // Exact error codes and messages are subject to change.<br>    "code": 8201,<br>    "message": "Validation failed.",<br>    "errors": {<br>      "reason": "Failed to upload image. Cause: {\"code\":\"error.file.size.limit.exceeded\"}",<br>      "code": 8201<br>    }<br>}`<br>400 Unsupported file format error example (See HTTP Status Codes below) [View Response](https://developers.printify.com/#)`{<br>    "status": "error",<br>    // Exact error codes and messages are subject to change.<br>    "code": 8201,<br>    "message": "Validation failed.",<br>    "errors": {<br>      "reason": "Failed to upload image. Cause: {\"code\":\"error.file.wrong.format\"}",<br>      "code": 8201<br>    }<br>}` |

## Events

Events are generated by some resources when certain actions are completed, such as the creation of a product, the fulfillment of an order. By requesting events, your app can know when certain actions have occurred in the shop.

On this page:

- [Shop events](https://developers.printify.com/#shop-events)
- [Product events](https://developers.printify.com/#product-events)
- [Order events](https://developers.printify.com/#order-events)
- [Personalization events](https://developers.printify.com/#personalization-events)
- [Event properties](https://developers.printify.com/#event-properties)
- [Resource properties](https://developers.printify.com/#resource-properties)
- [Resource data examples](https://developers.printify.com/#resource-data-examples)
  - [Shop resource data examples](https://developers.printify.com/#shop-resource-data-examples)
  - [Product resource data examples](https://developers.printify.com/#product-resource-data-examples)
  - [Order resource data examples](https://developers.printify.com/#order-resource-data-examples)
- [Payload examples](https://developers.printify.com/#payload-examples)

### Shop events

|     |     |
| --- | --- |
| Event | Description |
| `shop:disconnected` | The shop was disconnected. |

### Product events

|     |     |
| --- | --- |
| Event | Description |
| `product:deleted` | The product was deleted. |
| `product:created` | The product was created. |
| `product:updated` | The product was updated. |
| `product:publish:started` | The product publishing was started. |

### Order events

|     |     |
| --- | --- |
| Event | Description |
| `order:created` | The order was created. |
| `order:updated` | The order's status was updated. |
| `order:sent-to-production` | The order was sent to production. |
| `order:shipment:created` | Some/all items have been fulfilled. |
| `order:shipment:delivered` | Some/all items have been delivered. |

### Personalization events

|     |     |
| --- | --- |
| Event | Description |
| `personalization-preview-task:processed` | A personalization preview task reached a terminal state (completed, corrupt, or failed). |

### Event properties

|     |     |
| --- | --- |
| id | `"id": "653b6be8-2ff7-4ab5-a7a6-6889a8b3bbf5"`<br> A unique string identifier for the event. Each id is unique across the Printify system. |
| type | `"type": "order:created"`<br> The type of event that occurred. Different resources generate different types of event. |
| created\_at | `"created_at": "2017-04-18 13:24:28+00:00"`<br> The date and time when the event was triggered. |
| resource | `"resource": {<br>     "id": "653b6be8-2ff7-4ab5-a7a6-6889a8b3bbf5",<br>     "type": "product",<br>     "data":  {<br>        "shop_id": 1234567,<br>        "reason": "Request timed out"<br>    }<br>}`<br> Information about the resource that triggered the event. Check [Resource properties](https://developers.printify.com/#resource-properties) for reference. |

### Resource properties

|     |     |
| --- | --- |
| id | `"id": "5cb87a8cd490a2ccb256cec4"`<br> A unique string identifier for the resource. Each id is unique across the Printify system. |
| type | `"type": "product"`<br> Resource type, currently valid types are `shop`, `product`, `order` and `personalization-preview-task`. |
| data | `"data": {<br>    "shop_id": 1234567,<br>    "reason": "Request timed out"<br>}`<br> For more information see [Resource data examples](https://developers.printify.com/#resource-data-examples). |

### Resource data examples

### Shop events

|     |     |
| --- | --- |
| `shop:disconnected` | No resource data is sent. |

### Product events

|     |     |
| --- | --- |
| `product:deleted` | `"data": {<br>    "shop_id": 815256<br>}` |
| `product:created` | `"data": {<br>    "shop_id": 815256<br>}` |
| `product:updated` | `"data": {<br>    "shop_id": 815256<br>}` |
| `product:publish:started` | The values for the action property determine the resource data payload, the values can be "create", "update", or "delete". For "create" and "update" actions, the payload is as follows:<br> `"data": {<br>    "shop_id": 1234567,<br>    "publish_details": {<br>        "title": true,<br>        "description": true,<br>        "images": true,<br>        "variants": true,<br>        "tags": true,<br>        "key_features": true,<br>        "shipping_template": true<br>    },<br>    "action": "create",<br>}`<br> For the "delete" action, the payload is as follows:<br> `"data": {<br>    "action": "delete"<br>}`<br> For reference on what other properties mean, check [Publishing properties](https://developers.printify.com/#publishing-properties). |

### Order events

|     |     |
| --- | --- |
| `order:created` | No resource data is sent with this event. |
| `order:updated` | `"data": {<br>    "shop_id": 815256,<br>    "status": "in-production"<br>}`<br> For information on what production statuses can be expected, check [Order properties](https://developers.printify.com/#order-properties) for reference. |
| `order:shipment:created` | `"data": {<br>    "shop_id": 815256,<br>    "shipped_at": "2017-04-18 13:24:28+00:00",<br>    "carrier": {<br>      "code": "USPS",<br>      "tracking_number": "9400110200828911663274"<br>    },<br>    "skus": [<br>      "6220"<br>  ]<br>}` |
| `order:shipment:delivered` | `"data": {<br>    "shop_id": 815256,<br>    "delivered_at": "2017-04-18 13:24:28+00:00",<br>    "carrier": {<br>      "code": "USPS",<br>      "tracking_number": "9400110200828911663274"<br>    },<br>    "skus": [<br>      "6220"<br>  ]<br>}` |
| `order:sent-to-production` | No resource data is sent with this event. |

### Personalization events

|     |     |
| --- | --- |
| `personalization-preview-task:processed` | `"data": {<br>    "task_id": "e12eb4c7-c3bd-4ce5-8dad-d782e9450708",<br>    "status": "completed",<br>    "shop_id": 815256,<br>    "preview_count": 1,<br>    "mockups": [<br>        {<br>            "variant_id": 38191,<br>            "mockup_id": "Front",<br>            "src": "https://dsaujk5puqrkx.cloudfront.net/buyer-preview/145/buyer-preview/38191/97992/4715046825664400772_2048.jpeg"<br>        }<br>    ]<br>}`<br> This event only fires on terminal states, so `status` is always one of `completed`,<br> `corrupt`, or `failed`. When `status` is `corrupt` or<br> `failed`, `mockups` and `preview_count` are omitted and an `error`<br> object is present instead. For `"failed"`, `message` is a generic, non-sensitive<br> description of the stage that failed — safe to retry:<br> `"data": {<br>    "task_id": "e12eb4c7-c3bd-4ce5-8dad-d782e9450708",<br>    "status": "failed",<br>    "shop_id": 815256,<br>    "error": { "message": "Designer API request failed", "code": 500 }<br>}`<br> For `"corrupt"`, `message` describes the actual problem with the input — retrying with<br> the same input will not help:<br> `"data": {<br>    "task_id": "e12eb4c7-c3bd-4ce5-8dad-d782e9450708",<br>    "status": "corrupt",<br>    "shop_id": 815256,<br>    "error": { "message": "Requested variant_id \"99999999\" does not exist on this product.", "code": 422 }<br>}` |

### Payload examples

|     |     |
| --- | --- |
| `shop:disconnected` | `<br>{<br>  "id": "653b6be8-2ff7-4ab5-a7a6-6889a8b3bbf5",<br>  "type": "shop:disconnected",<br>  "created_at": "2022-05-17 15:00:00+00:00",<br>  "resource": {<br>    "id": 815256,<br>    "type": "shop",<br>    "data": null<br>  }<br>}<br>` |
| `product:deleted` | `<br>{<br>  "id": "653b6be8-2ff7-4ab5-a7a6-6889a8b3bbf5",<br>  "type": "product:deleted",<br>  "created_at": "2022-05-17 15:00:00+00:00",<br>  "resource": {<br>    "id": "5cb87a8cd490a2ccb256cec4",<br>    "type": "product",<br>    "data": {<br>      "shop_id": 815256<br>    }<br>  }<br>}<br>` |
| `product:publish:started` | `<br>{<br>  "id": "653b6be8-2ff7-4ab5-a7a6-6889a8b3bbf5",<br>  "type": "product:publish:started",<br>  "created_at": "2022-05-17 15:00:00+00:00",<br>  "resource": {<br>    "id": "5cb87a8cd490a2ccb256cec4",<br>    "type": "product",<br>    "data": {<br>      "shop_id": 815256,<br>      "publish_details": {<br>        "title": true,<br>        "variants": false,<br>        "description": true,<br>        "tags": true,<br>        "images": false,<br>        "key_features": false,<br>        "shipping_template": true<br>      },<br>      "action": "create",<br>      "out_of_stock_publishing": 0<br>    }<br>  }<br>}<br>` |
| `order:created` | `<br>{<br>  "id": "653b6be8-2ff7-4ab5-a7a6-6889a8b3bbf5",<br>  "type": "order:created",<br>  "created_at": "2022-05-17 15:00:00+00:00",<br>  "resource": {<br>    "id": "5a96f649b2439217d070f507",<br>    "type": "order",<br>    "data": {<br>      "shop_id": 815256<br>    }<br>  }<br>}<br>` |
| `order:updated` | `<br>{<br>  "id": "653b6be8-2ff7-4ab5-a7a6-6889a8b3bbf5",<br>  "type": "order:updated",<br>  "created_at": "2022-05-17 15:00:00+00:00",<br>  "resource": {<br>    "id": "5a96f649b2439217d070f507",<br>    "type": "order",<br>    "data": {<br>      "shop_id": 815256,<br>      "status": "in-production"<br>    }<br>  }<br>}<br>` |
| `order:shipment:created` | `<br>{<br>  "id": "653b6be8-2ff7-4ab5-a7a6-6889a8b3bbf5",<br>  "type": "order:shipment:created",<br>  "created_at": "2022-05-17 15:00:00+00:00",<br>  "resource": {<br>    "id": "5a96f649b2439217d070f507",<br>    "type": "order",<br>    "data": {<br>      "shop_id": 815256,<br>      "shipped_at": "2022-05-17 15:00:00+00:00",<br>      "carrier": {<br>        "code": "USPS",<br>        "tracking_number": "9400110200828911663274",<br>        "tracking_url": "https://example.com/track/9400110200828911663274"<br>      },<br>      "skus": [<br>        "6202"<br>      ]<br>    }<br>  }<br>}<br>` |
| `order:shipment:delivered` | `<br>{<br>  "id": "653b6be8-2ff7-4ab5-a7a6-6889a8b3bbf5",<br>  "type": "order:shipment:delivered",<br>  "created_at": "2022-05-17 15:00:00+00:00",<br>  "resource": {<br>    "id": "5a96f649b2439217d070f507",<br>    "type": "order",<br>    "data": {<br>      "shop_id": 815256,<br>      "delivered_at": "2022-05-17 15:00:00+00:00",<br>      "carrier": {<br>        "code": "USPS",<br>        "tracking_number": "9400110200828911663274",<br>        "tracking_url": "https://example.com/track/9400110200828911663274"<br>      },<br>      "skus": [<br>        "6202"<br>      ]<br>    }<br>  }<br>}<br>` |
| `order:sent-to-production` | `<br>{<br>  "id": "653b6be8-2ff7-4ab5-a7a6-6889a8b3bbf5",<br>  "type": "order:sent-to-production",<br>  "created_at": "2022-05-17 15:00:00+00:00",<br>  "resource": {<br>    "id": "5a96f649b2439217d070f507",<br>    "type": "order",<br>    "data": {<br>      "shop_id": 815256<br>    }<br>  }<br>}<br>` |
| `personalization-preview-task:processed` | `<br>{<br>  "id": "653b6be8-2ff7-4ab5-a7a6-6889a8b3bbf5",<br>  "type": "personalization-preview-task:processed",<br>  "created_at": "2022-05-17 15:00:00+00:00",<br>  "resource": {<br>    "id": "e12eb4c7-c3bd-4ce5-8dad-d782e9450708",<br>    "type": "personalization-preview-task",<br>    "data": {<br>      "task_id": "e12eb4c7-c3bd-4ce5-8dad-d782e9450708",<br>      "status": "completed",<br>      "shop_id": 815256,<br>      "preview_count": 1,<br>      "mockups": [<br>        {<br>          "variant_id": 38191,<br>          "mockup_id": "Front",<br>          "src": "https://dsaujk5puqrkx.cloudfront.net/buyer-preview/145/buyer-preview/38191/97992/4715046825664400772_2048.jpeg"<br>        }<br>      ]<br>    }<br>  }<br>}<br>` |

## Webhooks

You can use webhook subscriptions to receive notifications about particular events in a shop. After you've subscribed to a webhook, you can let your app execute code immediately after specific events occur in shops that have your app connected, instead of having to make API calls periodically to check their status. For example, you can rely on webhooks to trigger an action in your app when a merchant creates a new product in a store. By using webhooks subscriptions you can make fewer API calls overall, which makes sure that your apps are more efficient and update quickly. For more information what actually gets sent by a webhook check [Event properties](https://developers.printify.com/#event-properties) and [Resource data examples](https://developers.printify.com/#resource-data-examples).

|     |     |
| --- | --- |
| ⚠ | All webhook endpoints require a `{shop_id}` parameter. See [Retrieving Shop ID](https://developers.printify.com/#retrieving-shop-id) for instructions on how to obtain your shop ID. |

On this page:

- [Webhook rules to follow](https://developers.printify.com/#webhook-rules-to-follow)
- [What you can do with the webhooks resource](https://developers.printify.com/#what-you-can-do-with-the-webhooks-resource)
- [Webhook properties](https://developers.printify.com/#webhook-properties)
- [Webhook endpoints](https://developers.printify.com/#webhook-endpoints)
- [Securing your Webhooks](https://developers.printify.com/#securing-your-webhooks)

### Webhook rules to follow

To ensure that your webhook works correctly, follow these good practices:

- Printify will send a POST request to the URL you specify when the event occurs.
- This POST request will contain a JSON payload with information about the event.
- The expected response is a **200 OK**.
- In case of a 4xx or 5xx response, Printify will retry the request up to 3 times, after which the webhook will be **blocked** for 1 hour.
- If the webhook is blocked, no new requests will be sent to the URL until the block is lifted.

### What you can do with the Webhooks resource

The Printify Public API lets you do the following with the Webhook resource:

- [GET /v1/shops/{shop\_id}/webhooks.json](https://developers.printify.com/#retrieve-a-list-of-webhooks)

Retrieve a list of webhooks
- [POST /v1/shops/{shop\_id}/webhooks.json](https://developers.printify.com/#create-a-new-webhook)

Create a new webhook
- [PUT /v1/shops/{shop\_id}/webhooks/{webhook\_id}.json](https://developers.printify.com/#modify-a-webhook)

Modify a webhook
- [DELETE /v1/shops/{shop\_id}/webhooks/{webhook\_id}.json](https://developers.printify.com/#delete-a-webhook)

Delete a webhook

### Webhook properties

|     |     |
| --- | --- |
| id<br> READ-ONLY | `"id": "5cb87a8cd490a2ccb256cec4"`<br> A unique string identifier for the webhook. Each id is unique across the Printify system. |
| topic<br> REQUIREDREAD-ONLY | `"topic": "product:publish:started"`<br> Event that triggers the webhook. See [Events](https://developers.printify.com/#events) for reference. Can't be changed. |
| url<br> REQUIRED | `"url": "https://example.com/webhooks"`<br> URI where the webhook subscription should send the POST request when the event occurs. |
| shop\_id<br> READ-ONLY | `"shop_id": 1`<br> Id of merchant's store. |
| secret<br> OPTIONAL | `"secret": "optional-secret-value"`<br> Secret that will be used to sign requests for webhook. See [Securing your webhooks](https://developers.printify.com/#securing-your-webhooks) for more information. |

### Webhook endpoints

### Retrieve a list of webhooks

|     |     |
| --- | --- |
| GET | /v1/shops/{shop\_id}/webhooks.json |
| **Retrieve a list of webhooks**<br>`GET /v1/shops/{shop_id}/webhooks.json`<br>[View Response](https://developers.printify.com/#)`[<br>    {<br>        "topic": "order:created",<br>        "url": "https://example.com/webhooks/order/created",<br>        "shop_id": "1",<br>        "id": "5cb87a8cd490a2ccb256cec4"<br>    },<br>    {<br>        "topic": "order:updated",<br>        "url": "https://example.com/webhooks/order/updated",<br>        "shop_id": "1",<br>        "id": "5cb87a8cd490a2ccb256cec5"<br>    }<br>]<br>` |

### Create a new webhook

|     |     |
| --- | --- |
| POST | /v1/shops/{shop\_id}/webhooks.json |
| **Create a new webhook**<br>`POST /v1/shops/{shop_id}/webhooks.json`<br>`{<br>    "topic": "order:created",<br>    "url": "https://example.com/webhooks/order/created"<br>}` [View Response](https://developers.printify.com/#)`<br>{<br>    "topic": "order:created",<br>    "url": "https://example.com/webhooks/order/created",<br>    "shop_id": "1",<br>    "id": "5cb87a8cd490a2ccb256cec4"<br>}<br>` |

### Modify a webhook

|     |     |
| --- | --- |
| PUT | /v1/shops/{shop\_id}/webhooks/{webhook\_id}.json |
| **Modify a webhook**<br>`PUT /v1/shops/{shop_id}/webhooks/{webhook_id}.json`<br>`{<br>    "url": "https://example.com/callback/order/created"<br>}` [View Response](https://developers.printify.com/#)`<br>{<br>    "topic": "order:created",<br>    "url": "https://example.com/callback/order/created",<br>    "shop_id": "1",<br>    "id": "5cb87a8cd490a2ccb256cec4"<br>}<br>` |

### Delete a webhook

|     |     |
| --- | --- |
| DELETE | /v1/shops/{shop\_id}/webhooks/{webhook\_id}.json |
| host<br> REQUIRED | `host=example.com`<br>The expected host of the webhook’s URL. This parameter acts as a safeguard: the deletion will only succeed if the webhook’s URL host matches the value provided. This prevents accidental deletion of webhooks belonging to a different host. |
| **Delete a webhook**<br>`DELETE /v1/shops/{shop_id}/webhooks/{webhook_id}.json?host={webhook_host}`<br>[View Response](https://developers.printify.com/#)`{<br>    "id": "5cb87a8cd490a2ccb256cec4"<br>}<br>` |

### Simulating a webhook

Use this endpoint to simulate a webhook event. Any data in the request body will be returned
in the webhook `resource` property.

|     |     |
| --- | --- |
| POST | /v1/shops/{shop\_id}/webhooks/{webhook\_id}/simulate |
| **Simulate a webhook**<br>`POST /v1/shops/{shop_id}/webhooks/{webhook_id}/simulate`<br>`{<br>    "anything": "test"<br>}` |

### Securing your Webhooks

Once your server is configured to receive payloads, it'll listen for any payload sent to the endpoint you configured.
For security reasons, you probably want to limit requests to those coming from Printify.

There are a few ways to go about this
\- for example, you could opt to whitelist requests from Printify's IP address
\- but a far easier method is to set up a secret token and validate the information.

Summary:

- [Setting your shared secret with Printify](https://developers.printify.com/#setting-your-shared-secret-with-printify)
- [Accessing the Secret from your backend](https://developers.printify.com/#accessing-the-secret-from-your-backend)
- [Validating payloads from Printify](https://developers.printify.com/#validating-payloads-from-printify)

#### Setting your shared secret with Printify

You can generate the secret by running '`openssl rand -hex 20`'.

When your secret token is set, Printify will use it to create a hash signature with each payload body. Printify uses an HMAC
hexdigest to compute the hash `sha256` signature with your provided secret.

|     |
| --- |
| Secret example`<br>    7afa37fd47d7a52ea644382e04962a83c16aef62<br>` |

This payload body signature is passed along with each request in the headers as `X-Pfy-Signature`. The signature format is: `sha256={digest}`.

|     |
| --- |
| Signature example`<br>    x-pfy-signature: sha256=4260d30ec4ee2a17181ae5072c846d8dfcb5ceb195e24de055fd9a21d8c6648f<br>` |

#### Accessing the Secret from your backend

Next, set up a `SECRET_TOKEN` environment variable on your server that stores this token. **Never hardcode the**
**secret into your app!**

|     |
| --- |
| Setting the SECRET\_TOKEN environment variable example`<br>    $ export SECRET_TOKEN=your_token<br>` |

#### Validating payloads from Printify

Next, compute a request body hash using your `SECRET_TOKEN`, and ensure that the hash from Printify matches. Printify
uses an HMAC hexdigest to compute the hash. **Always use "constant time" string comparisons, which renders it safe from**
**certain timing attacks against regular equality operators.**

|     |
| --- |
| Validation sample (python)`<br>    import os<br>    import hmac<br>    def sha256hash(request):<br>        hash = hmac.new(os.environ['SECRET_TOKEN'].encode('utf-8'),<br>                        request.data.encode('utf-8'),<br>                        'sha256')<br>        return 'sha256=' + hash.hexdigest()<br>    def secure_compare(a, b):<br>        return hmac.compare_digest(a, b)<br>    print('%r' % secure_compare(request.headers['x-pfy-signature'],<br>                                sha256hash(request)))<br>` |

# V2 API Reference

The second version of the API is organized around the [{json:api}](https://jsonapi.org/) specification.
This version of the API is designed to be more consistent and predictable and to provide a better foundation
for future improvements. It follows JSON API standard on pagination, linking and can support the filtering
if it is mentioned in the endpoint documentation.

New features and improvements are being added to the V2 API, and we encourage you to use it for new integrations.
The V1 API will continue to be supported, but new features will only be added to the V2 API.

Use the following V2 API base URL for your brand:

- **Printify**: `https://api.printify.com/v2/`
- **Printful Enterprise**: `https://enterprise.printful.com/api/pfy/public/v2/`

The [Economy Shipping](https://help.printify.com/hc/en-us/sections/22109518886161-Economy-Shipping) costs listing is available only in the V2 API.

## Catalog V2

Through the Catalog resource you can see all of the products, product variants, variant options and print providers
available in the Printify catalog.

Products in the Printify catalog are referred to as blueprints (only after user artwork has been added, they are referred to as products).

Every blueprint in the Printify catalog has multiple Print Providers that offer that blueprint. In addition to general
differences between Print Providers including location and print technology employed, each Print Provider also offers
different colors, sizes, print areas and prices.

Each Print Provider's blueprint has specific option (e.g. color, size) combinations known as variants. Variants also contain
information on a products' available print areas and sizes.

On this page:

- [What you can do with the catalog resource](https://developers.printify.com/#v2-what-you-can-do-with-the-catalog-resource)
- [Shipping properties](https://developers.printify.com/#v2-catalog-shipping-attributes)
- [Endpoints](https://developers.printify.com/#v2-catalog-endpoints)

### What you can do with the catalog resource

The Printify Public API lets you do the following with the Catalog resource:

- [GET /v2/catalog/blueprints/{blueprint\_id}/print\_providers/{print\_provider\_id}/shipping.json](https://developers.printify.com/#v2-catalog-endpoints)

Retrieve the list of available shipping for all variants of a blueprint from a specific print provider
- [GET /v2/catalog/blueprints/{blueprint\_id}/print\_providers/{print\_provider\_id}/shipping/standard.json](https://developers.printify.com/#v2-catalog-endpoints)

Retrieve the standard shipping handling time and shipping costs for all variants of a blueprint from a specific print provider.
- [GET /v2/catalog/blueprints/{blueprint\_id}/print\_providers/{print\_provider\_id}/shipping/priority.json](https://developers.printify.com/#v2-catalog-endpoints)

Retrieve the priority shipping handling time and shipping costs for all variants of a blueprint from a specific print provider.
- [GET /v2/catalog/blueprints/{blueprint\_id}/print\_providers/{print\_provider\_id}/shipping/express.json](https://developers.printify.com/#v2-catalog-endpoints) Retrieve the express shipping handling time and shipping costs for all variants of a blueprint from a specific print provider.
- [GET /v2/catalog/blueprints/{blueprint\_id}/print\_providers/{print\_provider\_id}/shipping/economy.json](https://developers.printify.com/#v2-catalog-endpoints)

Retrieve the economy shipping handling time and shipping costs for all variants of a blueprint from a specific print provider.

### Shipping list attributes

| Attribute | Description |
| --- | --- |
| name<br> READ-ONLY | `"name": "standard"`<br> The shipping type (method) name |

#### Specific Shipping attributes

| Attribute | Description |
| --- | --- |
| shippingType<br> READ-ONLY | `"shippingType": "economy"`<br> The shipping type (method) name |
| country<br> READ-ONLY | `"country": {<br>  "code": "US"<br>}`<br> The code of the country the shipping costs apply to. Can be also `REST_OF_THE_WORLD` which means it applies to all the countries that don't have the costs specified. |
| variantId<br> READ-ONLY | `"variantId": 1`<br> Variant ID for which this shipping is available |
| shippingPlanId<br> READ-ONLY | `"shippingPlanId": "65a7c0825b50fcd56a018e02"`<br> Internal Shipping Plan ID that is used to calculate shipping costs |
| handlingTime<br> READ-ONLY | `"handlingTime": {<br>  "from": 4,<br>  "to": 8<br>}`<br> Delivery time in days |
| shippingCost<br> READ-ONLY | `"shippingCost": {<br>  "firstItem": {<br>      "amount": 399,<br>      "currency": "USD"<br>  },<br>  "additionalItems": {<br>      "amount": 219,<br>      "currency": "USD"<br>  }`<br> Shipping cost for first, and potentially additional items. Returned in cents (1/100), for example: 399 = $3.99. |

### Endpoints

#### Retrieve available shipping list information

|     |     |
| --- | --- |
| GET | /v2/catalog/blueprints/{blueprint\_id}/print\_providers/{print\_provider\_id}/shipping.json |
| **Retrieve available shipping list information**<br>`GET /v2/catalog/blueprints/{blueprint_id}/print_providers/{print_provider_id}/shipping.json`<br>[View Response](https://developers.printify.com/#)`{<br>    "data": [<br>        {<br>            "type": "shipping_method",<br>            "id": "1",<br>            "attributes": {<br>                "name": "standard"<br>            }<br>        },<br>        {<br>            "type": "shipping_method",<br>            "id": "2",<br>            "attributes": {<br>                "name": "priority"<br>            }<br>        },<br>        {<br>            "type": "shipping_method",<br>            "id": "3",<br>            "attributes": {<br>                "name": "express"<br>            }<br>        },<br>        {<br>            "type": "shipping_method",<br>            "id": "4",<br>            "attributes": {<br>                "name": "economy"<br>            }<br>        }<br>    ],<br>    "links": {<br>        "standard": "https://api.printify.com/v2/catalog/blueprints/{blueprint_id}/print_providers/{print_provider_id}/shipping/standard.json",<br>        "priority": "https://api.printify.com/v2/catalog/blueprints/{blueprint_id}/print_providers/{print_provider_id}/shipping/priority.json",<br>        "priority": "https://api.printify.com/v2/catalog/blueprints/{blueprint_id}/print_providers/{print_provider_id}/shipping/express.json",<br>        "economy": "https://api.printify.com/v2/catalog/blueprints/{blueprint_id}/print_providers/{print_provider_id}/shipping/economy.json"<br>    }<br>}` |

#### Retrieve specific shipping method information

|     |     |
| --- | --- |
| GET | /v2/catalog/blueprints/{blueprint\_id}/print\_providers/{print\_provider\_id}/shipping/standard.json |
| **Retrieve standard shipping method information**<br>`GET /v2/catalog/blueprints/{blueprint_id}/print_providers/{print_provider_id}/shipping/standard.json`<br>[View Response](https://developers.printify.com/#)`{<br>    "data": [<br>        {<br>            "type": "variant_shipping_standard_us",<br>            "id": "23494",<br>            "attributes": {<br>                "shippingType": "standard",<br>                "country": {<br>                    "code": "US"<br>                },<br>                "variantId": 23494,<br>                "shippingPlanId": "65a7c0825b50fcd56a018e02",<br>                "handlingTime": {<br>                    "from": 4,<br>                    "to": 8<br>                },<br>                "shippingCost": {<br>                    "firstItem": {<br>                        "amount": 399,<br>                        "currency": "USD"<br>                    },<br>                    "additionalItems": {<br>                        "amount": 219,<br>                        "currency": "USD"<br>                    }<br>                }<br>            }<br>        }<br>    ]<br>}` |
| GET | /v2/catalog/blueprints/{blueprint\_id}/print\_providers/{print\_provider\_id}/shipping/priority.json |
| **Retrieve priority shipping method information**<br>`GET /v2/catalog/blueprints/{blueprint_id}/print_providers/{print_provider_id}/shipping/priority.json`<br>[View Response](https://developers.printify.com/#)`{<br>    "data": [<br>        {<br>            "type": "variant_shipping_priority_us",<br>            "id": "23494",<br>            "attributes": {<br>                "shippingType": "priority",<br>                "country": {<br>                  "code": "US"<br>                },<br>                "variantId": 23494,<br>                "shippingPlanId": "65a7c0825b50fcd56a018e02",<br>                "handlingTime": {<br>                    "from": 4,<br>                    "to": 8<br>                },<br>                "shippingCost": {<br>                    "firstItem": {<br>                        "amount": 399,<br>                        "currency": "USD"<br>                    },<br>                    "additionalItems": {<br>                        "amount": 219,<br>                        "currency": "USD"<br>                    }<br>                }<br>            }<br>        }<br>    ]<br>}` |
| GET | /v2/catalog/blueprints/{blueprint\_id}/print\_providers/{print\_provider\_id}/shipping/express.json |
| **Retrieve express shipping method information**<br>`GET /v2/catalog/blueprints/{blueprint_id}/print_providers/{print_provider_id}/shipping/express.json`<br>[View Response](https://developers.printify.com/#)`{<br>    "data": [<br>        {<br>            "type": "variant_shipping_express_us",<br>            "id": "23494",<br>            "attributes": {<br>                "shippingType": "express",<br>                "country": {<br>                    "code": "US"<br>                },<br>                "variantId": 23494,<br>                "shippingPlanId": "65a7c0825b50fcd56a018e02",<br>                "handlingTime": {<br>                    "from": 4,<br>                    "to": 8<br>                },<br>                "shippingCost": {<br>                    "firstItem": {<br>                        "amount": 399,<br>                        "currency": "USD"<br>                    },<br>                    "additionalItems": {<br>                        "amount": 219,<br>                        "currency": "USD"<br>                    }<br>                }<br>            }<br>        }<br>    ]<br>}` |
| GET | /v2/catalog/blueprints/{blueprint\_id}/print\_providers/{print\_provider\_id}/shipping/economy.json |
| **Retrieve economy shipping method information**<br>`GET /v2/catalog/blueprints/{blueprint_id}/print_providers/{print_provider_id}/shipping/economy.json`<br>[View Response](https://developers.printify.com/#)`{<br>    "data": [<br>        {<br>            "type": "variant_shipping_economy_us",<br>            "id": "23494",<br>            "attributes": {<br>                "shippingType": "economy",<br>                "country": {<br>                    "code": "US"<br>                },<br>                "variantId": 23494,<br>                "shippingPlanId": "65a7c0825b50fcd56a018e02",<br>                "handlingTime": {<br>                    "from": 4,<br>                    "to": 8<br>                },<br>                "shippingCost": {<br>                    "firstItem": {<br>                        "amount": 399,<br>                        "currency": "USD"<br>                    },<br>                    "additionalItems": {<br>                        "amount": 219,<br>                        "currency": "USD"<br>                    }<br>                }<br>            }<br>        }<br>    ]<br>}` |

# HTTP Status Codes

Printify API relies heavily on standard [HTTP response codes](https://tools.ietf.org/html/rfc7231#section-6.1) codes.
Please find the brief summary of status codes used below.

### Success

| Code | Name | Description |
| --- | --- | --- |
| 200 | OK | Request completed successfully. |
| 201 | Created | The request has been fulfilled and has resulted in one or more new resources being created. |
| 202 | Accepted | The request has been accepted for processing, but the processing has not been completed. |
| 204 | No Content | Indicates that the server has successfully fulfilled the request and that there is no content to send in the response payload body. |

### User error codes

These errors generally indicate a problem on the client side. If you are getting one of these, check your code and the
request details.

| Code | Name | Description |
| --- | --- | --- |
| 400 | Bad Request | The request encoding is invalid; the request can't be parsed as a valid JSON. |
| 401 | Unauthorized | Accessing a protected resource without authorization or with invalid credentials. |
| 402 | Payment Required | The account associated with the API key making requests hits a quota that can be increased by upgrading the Printify API account plan. |
| 403 | Forbidden | Accessing a protected resource with API credentials that don't have access to that resource. |
| 404 | Not Found | Route or resource is not found. This error is returned when the request hits an undefined route, or if the resource doesn't exist (e.g. has been deleted). |
| 413 | Request Entity Too Large | The request exceeded the maximum allowed payload size. You shouldn't encounter this under normal use. |
| 422 | Invalid Request | The request data is invalid. This includes most of the base-specific validations. You will receive a detailed error message and code pointing to the exact issue. |
| 429 | Too Many Requests | Too Many Requests response status code indicates you have sent too many requests in a given amount of time ("rate limiting"). |

### Server error codes

These errors generally represent an error on our side. In the event of a 5xx error code, detailed information about the
error will be automatically recorded, and Printify's developers will be notified.

| Code | Name | Description |
| --- | --- | --- |
| 500 | Internal Server Error | The server encountered an unexpected condition. |
| 502 | Bad Gateway | Printify's servers are restarting or an unexpected outage is in progress. You should generally not receive this error, and requests are safe to retry. |
| 503 | Service Unavailable | The server could not process your request in time. The server could be temporarily unavailable, or it could have timed out processing your request. You should retry the request with backoffs. |

# History

- Last update Oct 3 2024 - lowered products max pagination from 100 to 50.

[![](https://developers.printify.com/images/privacy-choices-a74d2eee.svg)\\
Your privacy choices](https://developers.printify.com/#)
