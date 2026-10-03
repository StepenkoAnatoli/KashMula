---
url: https://apify.com/conversational_kermis/apify-market-pricing-intelligence/api
retrieved: 2026-10-03
command: firecrawl scrape https://apify.com/conversational_kermis/apify-market-pricing-intelligence/api --only-main-content --json
statusCode: 200
transport: firecrawl-cli
completeness: full
title: Apify Store Market Intelligence & Competitor Pricing Scraper API · Apify
---
![Apify Market Pricing Intelligence avatar](https://images.apifyusercontent.com/1uR60n3UnzzBoeYfGwbmDWC6uBirlC8hSI6foomeIAc/rs:fill:250:250/cb:1/aHR0cHM6Ly9hcGlmeS1pbWFnZS11cGxvYWRzLXByb2QuczMudXMtZWFzdC0xLmFtYXpvbmF3cy5jb20vajFLN1JTSUxENHpKQlg0ZEstYWN0b3ItdG9qbUFMVFBEWDdMTDBBTlMtODF5RWJVYWtHTS1pY29uLnBuZw.webp)
Apify Market Pricing Intelligence

Pricing

Pricing

from $10.00 / 1,000 results

[Try for free](https://console.apify.com/actors/tojmALTPDX7LL0ANS?addFromActorId=tojmALTPDX7LL0ANS)

[Go to Apify Store](https://apify.com/store)

![Apify Market Pricing Intelligence](https://images.apifyusercontent.com/1uR60n3UnzzBoeYfGwbmDWC6uBirlC8hSI6foomeIAc/rs:fill:250:250/cb:1/aHR0cHM6Ly9hcGlmeS1pbWFnZS11cGxvYWRzLXByb2QuczMudXMtZWFzdC0xLmFtYXpvbmF3cy5jb20vajFLN1JTSUxENHpKQlg0ZEstYWN0b3ItdG9qbUFMVFBEWDdMTDBBTlMtODF5RWJVYWtHTS1pY29uLnBuZw.webp)

# Apify Market Pricing Intelligence

conversational\_kermis/apify-market-pricing-intelligence

[Try for free](https://console.apify.com/actors/tojmALTPDX7LL0ANS?addFromActorId=tojmALTPDX7LL0ANS)

Ask questions about this Actor

The ultimate competitor analysis tool for Apify Developers. Scrape pricing models, market trends, and actor metadata across all categories. Stop guessing and optimize your monetization strategy with real-time data. Includes automated strategic advice and market gap analysis.

Pricing

from $10.00 / 1,000 results

Rating

0.0

(0)

Developer

[![the anh nguyen](https://apify.com/img/store/user_picture.svg)\\
the anh nguyen](https://apify.com/conversational_kermis) Maintained by Community

Actor stats

Bookmarks

0

Bookmarked

Total users

2

Total users

Monthly active users

0

Monthly active users

Last modified

a month ago

Last modified

Categories

[Developer tools](https://apify.com/store/categories/developer-tools) [Business](https://apify.com/store/categories/business) [Marketing](https://apify.com/store/categories/marketing)

Share

[README](https://apify.com/conversational_kermis/apify-market-pricing-intelligence) [Input](https://apify.com/conversational_kermis/apify-market-pricing-intelligence/input-schema) [Pricing](https://apify.com/conversational_kermis/apify-market-pricing-intelligence/pricing) [API](https://apify.com/conversational_kermis/apify-market-pricing-intelligence/api/python) [Issues](https://apify.com/conversational_kermis/apify-market-pricing-intelligence/issues/open) [Changelog](https://apify.com/conversational_kermis/apify-market-pricing-intelligence/changelog)

You can access the Apify Market Pricing Intelligence programmatically from your own applications by using the Apify API. You can also choose the language preference from below. To use the Apify API, you’ll need an Apify account and your API token, found in [API & Integrations](https://console.apify.com/settings/integrations) in Apify Console.

[![Python](https://apify.com/img/template-icons/python.svg)\\
Python](https://apify.com/conversational_kermis/apify-market-pricing-intelligence/api/python) [![JavaScript](https://apify.com/img/template-icons/javascript.svg)\\
JavaScript](https://apify.com/conversational_kermis/apify-market-pricing-intelligence/api/javascript) [CLI](https://apify.com/conversational_kermis/apify-market-pricing-intelligence/api/cli) [![OpenAPI](https://apify.com/img/icons/openapi.svg)\\
OpenAPI](https://apify.com/conversational_kermis/apify-market-pricing-intelligence/api/openapi) [HTTP](https://apify.com/conversational_kermis/apify-market-pricing-intelligence/api) [MCP](https://apify.com/conversational_kermis/apify-market-pricing-intelligence/api/mcp)

```bash
# Set API token
$API_TOKEN=<YOUR_API_TOKEN>

# Prepare Actor input
$cat > input.json << 'EOF'
<{
<  "mode": "quick",
<  "categories": [\
<    "AI",\
<    "ECOMMERCE",\
<    "SOCIAL_MEDIA"\
<  ],
<  "maxResults": 0
<}
<EOF

# Run the Actor using an HTTP API
# See the full API reference at https://docs.apify.com/api/v2
$curl "https://api.apify.com/v2/actors/conversational_kermis~apify-market-pricing-intelligence/runs?token=$API_TOKEN" \
<  -X POST \
<  -d @input.json \
<  -H 'Content-Type: application/json'
```

## Apify Store Market Intelligence & Competitor Pricing Scraper API

Below, you can find a list of relevant HTTP API endpoints for calling the Apify Market Pricing Intelligence Actor. For this, you’ll need an Apify account. Replace<YOUR\_API\_TOKEN> in the URLs with your Apify API token, which you can find under [API & Integrations](https://console.apify.com/settings/integrations) in Apify Console. For details, see the [API reference](https://docs.apify.com/api/v2#/reference/actors).

### Run Actor

POST

```http

```

Note: By adding the `method=POST` query parameter, this API endpoint can be called using a GET request and thus used in third-party webhooks. Please refer to our [Run Actor API documentation](https://docs.apify.com/api/v2#tag/ActorsRun-collection/operation/act_runs_post).

### Run Actor synchronously and get dataset items

POST

```http

```

Note: This endpoint supports both POST and GET request methods. However, only the POST method allows you to pass input data. For more information, please refer to our [Run Actor synchronously and get dataset items API documentation](https://docs.apify.com/api/v2#tag/ActorsRun-Actor-synchronously-and-get-dataset-items).

### Get Actor

GET

```http

```

For more information, please refer to our [Get Actor API documentation](https://docs.apify.com/api/v2#tag/ActorsActor-object/operation/act_get).

Actors can be used to scrape web pages, extract data, or automate browser tasks. Use the Apify Market Pricing Intelligence API programmatically via the Apify API.

You can choose from:

[![Python](https://apify.com/img/template-icons/python.svg)\\
\\
Apify Market Pricing Intelligence API in Python](https://apify.com/conversational_kermis/apify-market-pricing-intelligence/api/python) [![JavaScript](https://apify.com/img/template-icons/javascript.svg)\\
\\
Apify Market Pricing Intelligence API in JavaScript](https://apify.com/conversational_kermis/apify-market-pricing-intelligence/api/javascript) [Apify Market Pricing Intelligence API through CLI](https://apify.com/conversational_kermis/apify-market-pricing-intelligence/api/cli) [![OpenAPI](https://apify.com/img/icons/openapi.svg)\\
\\
Apify Market Pricing Intelligence OpenAPI definition](https://apify.com/conversational_kermis/apify-market-pricing-intelligence/api/openapi)

You can start Apify Market Pricing Intelligence with the Apify API by sending an HTTP POST request to the [Run Actor](https://docs.apify.com/api/v2#/reference/actors/run-collection/run-actor) endpoint. An Actor’s input and its content type can be passed as a payload of the POST request, and additional options can be specified using URL query parameters. The Apify Market Pricing Intelligence is identified within the API by its ID, which is the creator’s username and the name of the Actor.

When the Apify Market Pricing Intelligence run finishes you can list the data from its default [dataset](https://docs.apify.com/platform/storage/usage)(storage) via the API or you can preview the data directly on [Apify Console](https://console.apify.com/).

## You might also like

[![App Store Reviews Scraper - Search by Keyword avatar](https://images.apifyusercontent.com/b_s-T6PHGud7pp0Tsm_kQrdHfRhp953CY8ZFHMvHuSg/rs:fill:76:76/cb:1/aHR0cHM6Ly9hcGlmeS1pbWFnZS11cGxvYWRzLXByb2QuczMudXMtZWFzdC0xLmFtYXpvbmF3cy5jb20vajFLN1JTSUxENHpKQlg0ZEstYWN0b3ItVmdXVlgxRGNia0NZOU1QSFUtanBvbzJUZ01lTy1pY29uLnBuZw.webp)\\
\\
**App Store Reviews Scraper - Search by Keyword**\\
\\
conversational\_kermis/pulse-appstore\\
\\
Search the Apple App Store by keyword and export the reviews of matching apps: rating, title, body, author, app name and ID. Apple offers no public export and shows reviews a few at a time; this does the searching and paging for you.\\
\\
![User avatar](https://images.apifyusercontent.com/jQEnhQdd-BMPhbZYouT-7EJazp_6dsAr97thN8XwjCY/rs:fill:32:32/cb:1/aHR0cHM6Ly9pbWFnZXMuYXBpZnl1c2VyY29udGVudC5jb20vUk5LYU4taDZOa21ZdFhOQmtFb0d2NmtyVEVyZmRhc1IxMTJiLW9IRjNZOC9yczpmaWxsOjMyOjMyL2NiOjEvYUhSMGNITTZMeTkzZDNjdVozSmhkbUYwWVhJdVkyOXRMMkYyWVhSaGNpODRaRFEyTlROaE5qVXdOVFk0WVRjME9XRTFaVFF6WWpReU1tVmtaamszTVQ5a1BXaDBkSEJ6SlROQkpUSkdKVEpHWTJSdUxtRndhV1o1TG1OdmJTVXlSbWx0WnlVeVJtbGpiMjV6SlRKR1lXNXZibmx0YjNWelgzVnpaWEpmY0dsamRIVnlaUzV3Ym1j.webp)\\
\\
the anh nguyen\\
\\
2](https://apify.com/conversational_kermis/pulse-appstore)

[![Google Play App & Review Scraper avatar](https://images.apifyusercontent.com/5IjAP9xh5rmVjVtKU9Gf-8snCJYfx1iwVft6rWRYt6Y/rs:fill:76:76/cb:1/aHR0cHM6Ly9hcGlmeS1pbWFnZS11cGxvYWRzLXByb2QuczMudXMtZWFzdC0xLmFtYXpvbmF3cy5jb20vajFLN1JTSUxENHpKQlg0ZEstYWN0b3Itd2dVV3VEUjJaUnFZMlpIeDgtNWk1c0x0ZThNdS1pY29uLnBuZw.webp)\\
\\
**Google Play App & Review Scraper**\\
\\
conversational\_kermis/pulse-google-play\\
\\
Search Google Play by keyword, then collect the 1-3 star reviews of the matching apps: reviewer, rating, full review text and app id. Works without a proxy. Verified on the Apify platform on 2026-08-21.\\
\\
![User avatar](https://images.apifyusercontent.com/jQEnhQdd-BMPhbZYouT-7EJazp_6dsAr97thN8XwjCY/rs:fill:32:32/cb:1/aHR0cHM6Ly9pbWFnZXMuYXBpZnl1c2VyY29udGVudC5jb20vUk5LYU4taDZOa21ZdFhOQmtFb0d2NmtyVEVyZmRhc1IxMTJiLW9IRjNZOC9yczpmaWxsOjMyOjMyL2NiOjEvYUhSMGNITTZMeTkzZDNjdVozSmhkbUYwWVhJdVkyOXRMMkYyWVhSaGNpODRaRFEyTlROaE5qVXdOVFk0WVRjME9XRTFaVFF6WWpReU1tVmtaamszTVQ5a1BXaDBkSEJ6SlROQkpUSkdKVEpHWTJSdUxtRndhV1o1TG1OdmJTVXlSbWx0WnlVeVJtbGpiMjV6SlRKR1lXNXZibmx0YjNWelgzVnpaWEpmY0dsamRIVnlaUzV3Ym1j.webp)\\
\\
the anh nguyen\\
\\
2](https://apify.com/conversational_kermis/pulse-google-play)

[TP\\
\\
**Temu Product Intelligence API**\\
\\
soilair/temu-product-intelligence-api\\
\\
Search Temu products by keyword and extract current prices, original prices, product IDs, images, and product URLs with strict relevance filtering.\\
\\
![User avatar](https://images.apifyusercontent.com/v0m2zo2MCobQ7gujzCmKRG9CKThqVHmMjGZUjFgcDjI/rs:fill:32:32/cb:1/aHR0cHM6Ly9pbWFnZXMuYXBpZnl1c2VyY29udGVudC5jb20vbm45X3RZdi14dzc0WXVyWlZDZHhGVlZoZmkwaEhhLWJTTmZVZGVIR2NBRS9yczpmaWxsOjMyOjMyL2NiOjEvYUhSMGNITTZMeTlzYURNdVoyOXZaMnhsZFhObGNtTnZiblJsYm5RdVkyOXRMMkV2UVVObk9HOWpURWxCWm1wR2FXeFNObmRZYVRNeGFsYzVTRGx1YVc1RU5qSndka05pT1dwQk1taGxZV3MyWm5kNlEzSkljV1ExUlVGMVFUMXpPVFl0WXc.webp)\\
\\
Salih Can Kurnaz\\
\\
3](https://apify.com/soilair/temu-product-intelligence-api)

[AS\\
\\
**Apify Store Scraper**\\
\\
julia\_k/apify-store-scraper\\
\\
Scrape the Apify Store listing - ranking, review rating and count, user counts, run statistics, pricing and categories for every public Actor.\\
\\
![User avatar](https://images.apifyusercontent.com/prkwpBo2X05A3DKr_G_0er9kx2iqrJyIJcjcCKAhmos/rs:fill:32:32/cb:1/aHR0cHM6Ly9pbWFnZXMuYXBpZnl1c2VyY29udGVudC5jb20vVVFlQ3RmWGN5eFc5SlE4dEdEX3RsRUVqNlpjNmlXcDhYX19FVDN0T1l3RS9yczpmaWxsOjMyOjMyL2NiOjEvYUhSMGNITTZMeTlzYURNdVoyOXZaMnhsZFhObGNtTnZiblJsYm5RdVkyOXRMMkV2UVVObk9HOWpUSFF3UmtOYWFTMDVjM05sYzFNMGJraHFhRUp3T1VWNFMzWlNSbDh6U0hrMlZubFZTSEZHTURndE9GRkpRMEkxY0RWSGR6MXpPVFl0WXc.webp)\\
\\
Julia K\\
\\
2](https://apify.com/julia_k/apify-store-scraper)

[![Local Market Opportunity Intelligence avatar](https://images.apifyusercontent.com/AH6ENAlt4Nx89pVkxJD-CG8aZdq4MmOD6tVXt9MlMjc/rs:fill:76:76/cb:1/aHR0cHM6Ly9hcGlmeS1pbWFnZS11cGxvYWRzLXByb2QuczMudXMtZWFzdC0xLmFtYXpvbmF3cy5jb20vUG54VzlSbm15cmEzWWYyOFgtYWN0b3ItWk9obm1NVHhGOEdJRW5kTnctY1h1Q1RaZGhVMi1DaGF0R1BUX0ltYWdlX1NlcF8yMl9fMjAyNl9fMTFfMDFfMThfQU0ucG5n.webp)\\
\\
**Local Market Opportunity Intelligence**\\
\\
northpeak\_data/local-market-opportunity-intelligence\\
\\
Stop guessing where the next local-market opportunity is. Turn local business data into evidence-backed insights on market saturation, underserved areas, service gaps, competitor strength, and where to investigate next.\\
\\
![User avatar](https://images.apifyusercontent.com/vwKv1KkWtirqCoqeGeQPfPG5V4fcBwqaOlRl4hKp2Q4/rs:fill:32:32/cb:1/aHR0cHM6Ly9pbWFnZXMuYXBpZnl1c2VyY29udGVudC5jb20vbFJnRjFWbFd4WXJRbUw3Umk1ekVDS1lZbnd2RElvZ3NHLXhvTmV4eHpaVS9yczpmaWxsOjMyOjMyL2NiOjEvYUhSMGNITTZMeTloY0dsbWVTMXBiV0ZuWlMxMWNHeHZZV1J6TFhCeWIyUXVjek11ZFhNdFpXRnpkQzB4TG1GdFlYcHZibUYzY3k1amIyMHZVRzU0VnpsU2JtMTVjbUV6V1dZeU9GZ3RjSEp2Wm1sc1pTMUZRa2hhT0dkaVdFdFZMVU5vWVhSSFVGUmZTVzFoWjJWZlFYVm5YekU1WDE4eU1ESTJYMTh4TUY4ME1WOHlPRjlCVFM1d2JtYy5wbmc.webp)\\
\\
Northpeak Data\\
\\
2](https://apify.com/northpeak_data/local-market-opportunity-intelligence)

[![GitHub Trending Scraper - Daily Repos, Stars & Momentum avatar](https://images.apifyusercontent.com/znkqlIP5VL-VYKEZUdozVkTSQuI4Ky1RTH5ZmHe9fGg/rs:fill:76:76/cb:1/aHR0cHM6Ly9hcGlmeS1pbWFnZS11cGxvYWRzLXByb2QuczMudXMtZWFzdC0xLmFtYXpvbmF3cy5jb20vajFLN1JTSUxENHpKQlg0ZEstYWN0b3ItMWZCeHZvRU85RmxzbENFdGQtQ3BLTXV1bEYzUS1pY29uLnBuZw.webp)\\
\\
**GitHub Trending Scraper - Daily Repos, Stars & Momentum**\\
\\
conversational\_kermis/pulse-github-trending\\
\\
Get today's trending GitHub repositories as structured rows: owner, stars, forks, stars gained in the period, and language. GitHub publishes no API for its trending page and keeps no history, so run this daily and diff the results to track momentum.\\
\\
![User avatar](https://images.apifyusercontent.com/jQEnhQdd-BMPhbZYouT-7EJazp_6dsAr97thN8XwjCY/rs:fill:32:32/cb:1/aHR0cHM6Ly9pbWFnZXMuYXBpZnl1c2VyY29udGVudC5jb20vUk5LYU4taDZOa21ZdFhOQmtFb0d2NmtyVEVyZmRhc1IxMTJiLW9IRjNZOC9yczpmaWxsOjMyOjMyL2NiOjEvYUhSMGNITTZMeTkzZDNjdVozSmhkbUYwWVhJdVkyOXRMMkYyWVhSaGNpODRaRFEyTlROaE5qVXdOVFk0WVRjME9XRTFaVFF6WWpReU1tVmtaamszTVQ5a1BXaDBkSEJ6SlROQkpUSkdKVEpHWTJSdUxtRndhV1o1TG1OdmJTVXlSbWx0WnlVeVJtbGpiMjV6SlRKR1lXNXZibmx0YjNWelgzVnpaWEpmY0dsamRIVnlaUzV3Ym1j.webp)\\
\\
the anh nguyen\\
\\
2](https://apify.com/conversational_kermis/pulse-github-trending)

[![Apify Actor Details Scraper avatar](https://images.apifyusercontent.com/1PVb66jEQUl5BDiKOFEnu-_JfG59R54CIefS8rtX-KA/rs:fill:76:76/cb:1/aHR0cHM6Ly9hcGlmeS1pbWFnZS11cGxvYWRzLXByb2QuczMudXMtZWFzdC0xLmFtYXpvbmF3cy5jb20vY1ZNRVRxQUhSTmJuT0N6QXEtYWN0b3ItYldFa3NMVzRyU2ZpSXZXTWQtWWE2MjNWYlF6eC1sb2dvLnBuZw.webp)\\
\\
**Apify Actor Details Scraper**\\
\\
parseforge/apify-actor-details-scraper\\
\\
Pull detailed metadata from any Apify actor page. Extract title, description, author, categories, run counts, and social media tags. Ideal for market research, competitor analysis, or building an actor directory. Get structured data from actor URLs with pagination support.\\
\\
![User avatar](https://images.apifyusercontent.com/7v_fw1tYOZK4ZaPIPpFJPq4bd1wmXxpvscQbD-yADiU/rs:fill:32:32/cb:1/aHR0cHM6Ly9pbWFnZXMuYXBpZnl1c2VyY29udGVudC5jb20vWkphSmZPeFdyX3NPNFdCNU0wNEpfRWYyc1BlaWxmN0JyWUJGTkt5TmNFdy9yczpmaWxsOjMyOjMyL2NiOjEvYUhSMGNITTZMeTloY0dsbWVTMXBiV0ZuWlMxMWNHeHZZV1J6TFhCeWIyUXVjek11ZFhNdFpXRnpkQzB4TG1GdFlYcHZibUYzY3k1amIyMHZZMVpOUlZSeFFVaFNUbUp1VDBONlFYRXRjSEp2Wm1sc1pTMW5VbmxJWTBGSlFXNWtMWEJoY25ObFptOXlaMlZmYkc5bmJ5NXdibWMucG5n.webp)\\
\\
ParseForge\\
\\
2](https://apify.com/parseforge/apify-actor-details-scraper)

[LM\\
\\
**LLM Model Pricing, Deprecation & Migration Intelligence**\\
\\
quanmatrix/llm-model-pricing-deprecation-migration-intelligence\\
\\
Use this Actor to analyze llm model pricing, deprecation and migration and return decision-ready structured signals. Track model pricing, deprecations, context and availability changes across AI providers, then rank migration risk, cost impact and replacement priorities.\\
\\
![User avatar](https://images.apifyusercontent.com/AS-yXAGRROgODutgcKeonFC-zJZVQ5eJ3kXjsavW-Wg/rs:fill:32:32/cb:1/aHR0cHM6Ly9pbWFnZXMuYXBpZnl1c2VyY29udGVudC5jb20vcW1kaHdPZ3F3WlZZUzcySVpkdjJlN0xIeUxTMWxrRFQxMll5MkNIOW9Lay9yczpmaWxsOjMyOjMyL2NiOjEvYUhSMGNITTZMeTloY0dsbWVTMXBiV0ZuWlMxMWNHeHZZV1J6TFhCeWIyUXVjek11ZFhNdFpXRnpkQzB4TG1GdFlYcHZibUYzY3k1amIyMHZla05vTW1oa1IwaHBZa3hwYVVSQlFVVXRjSEp2Wm1sc1pTMUhia1pDUmxGemFIRkRMVmRvWVhSelFYQndYMGx0WVdkbFh6SXdNalV0TVRJdE1qbGZZWFJmTURFdU1EWXVOVFl1YW5CbFp3LmpwZWc.webp)\\
\\
Rafael Barreto Haddad\\
\\
2](https://apify.com/quanmatrix/llm-model-pricing-deprecation-migration-intelligence)

[![Stack Overflow Question Scraper - Search by Keyword & Tag avatar](https://images.apifyusercontent.com/_oUg232buJAX6WM_RYdhNn6yLw-AXOkhURIDu2QcUlA/rs:fill:76:76/cb:1/aHR0cHM6Ly9hcGlmeS1pbWFnZS11cGxvYWRzLXByb2QuczMudXMtZWFzdC0xLmFtYXpvbmF3cy5jb20vajFLN1JTSUxENHpKQlg0ZEstYWN0b3ItOUJqRURxdVdFQURhOXBGMkgtQUdkdDNlZDNvUy1pY29uLnBuZw.webp)\\
\\
**Stack Overflow Question Scraper - Search by Keyword & Tag**\\
\\
conversational\_kermis/pulse-stackoverflow\\
\\
Search Stack Overflow by keyword and get structured questions back: score, view count, answer count, tags, and whether it is answered. A question with high views and no accepted answer is a problem many people have and nobody has solved.\\
\\
![User avatar](https://images.apifyusercontent.com/jQEnhQdd-BMPhbZYouT-7EJazp_6dsAr97thN8XwjCY/rs:fill:32:32/cb:1/aHR0cHM6Ly9pbWFnZXMuYXBpZnl1c2VyY29udGVudC5jb20vUk5LYU4taDZOa21ZdFhOQmtFb0d2NmtyVEVyZmRhc1IxMTJiLW9IRjNZOC9yczpmaWxsOjMyOjMyL2NiOjEvYUhSMGNITTZMeTkzZDNjdVozSmhkbUYwWVhJdVkyOXRMMkYyWVhSaGNpODRaRFEyTlROaE5qVXdOVFk0WVRjME9XRTFaVFF6WWpReU1tVmtaamszTVQ5a1BXaDBkSEJ6SlROQkpUSkdKVEpHWTJSdUxtRndhV1o1TG1OdmJTVXlSbWx0WnlVeVJtbGpiMjV6SlRKR1lXNXZibmx0YjNWelgzVnpaWEpmY0dsamRIVnlaUzV3Ym1j.webp)\\
\\
the anh nguyen\\
\\
2](https://apify.com/conversational_kermis/pulse-stackoverflow)

[![Polymarket Price History Scraper avatar](https://images.apifyusercontent.com/7CXVNVwKKVZPfR9pnFG10qtxfEcyWEaFII8qFCyBk2Q/rs:fill:76:76/cb:1/aHR0cHM6Ly9hcGlmeS1pbWFnZS11cGxvYWRzLXByb2QuczMudXMtZWFzdC0xLmFtYXpvbmF3cy5jb20vcE9IY1J1Zk5OQWtic0FoN08tYWN0b3ItWHR4V2FIaUNobkxGQkhjaDQtYk5VbmdYUmVwSi1wb2x5bWFya2V0LnBuZw.webp)\\
\\
**Polymarket Price History Scraper**\\
\\
piotrv1001/polymarket-price-history-scraper\\
\\
The Polymarket Price History Scraper exports the full price history of Polymarket markets at 1-minute, hourly or daily intervals, with every point labelled by market, outcome, token ID and resolution (winner, close time) — ideal for prediction-market research and backtesting.\\
\\
![User avatar](https://images.apifyusercontent.com/hwpcE_mmsxc5tdo93bC-pAbO1W_iD3j4d9HUAWxt_u0/rs:fill:32:32/cb:1/aHR0cHM6Ly9pbWFnZXMuYXBpZnl1c2VyY29udGVudC5jb20vQXZwNS1MdmdVLUdFU0d6Z3NIdm5pZENtOFR4dmRsUnpkZUFFMlZpS0FUNC9yczpmaWxsOjMyOjMyL2NiOjEvYUhSMGNITTZMeTloY0dsbWVTMXBiV0ZuWlMxMWNHeHZZV1J6TFhCeWIyUXVjek11ZFhNdFpXRnpkQzB4TG1GdFlYcHZibUYzY3k1amIyMHZjRTlJWTFKMVprNU9RV3RpYzBGb04wOHRjSEp2Wm1sc1pTMDNRMk5SY1hsNVNXWkNMV0Z3YVdaNVgyeHZaMjh1Y0c1bi5wbmc.webp)\\
\\
FalconScrape\\
\\
2](https://apify.com/piotrv1001/polymarket-price-history-scraper)

### Related articles

[![Blog article image](https://images.apifyusercontent.com/0pRdflClAGPk0XaTq4LyAWsh2kFxkpdHwxk6knYyQDk/rs:fill:630:354/cb:1/aHR0cHM6Ly9zdG9yYWdlLmdob3N0LmlvL2MvZjIvNmUvZjI2ZWM5OTktOWE5MC00YWVlLWEwZDQtOWIzY2EyYmI2NjhmL2NvbnRlbnQvaW1hZ2VzL3NpemUvdzEyMDAvMjAyNi8wNi9BdXRvbWF0ZWRNYXJrZXQtcmVzZWFyY2gucG5n.webp)\\
\\
Automated market research: Build end-to-end workflows from one platform\\
\\
Read more](https://blog.apify.com/market-research-automation/)
