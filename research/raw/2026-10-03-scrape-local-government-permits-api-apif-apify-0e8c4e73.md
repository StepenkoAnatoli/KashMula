---
url: https://apify.com/spec-lab/scrape-local-government-permits/api
retrieved: 2026-10-03
command: firecrawl scrape https://apify.com/spec-lab/scrape-local-government-permits/api --only-main-content --json
statusCode: 200
transport: firecrawl-cli
completeness: full
title: Scrape Local Government Permits API · Apify
---
![Scrape Local Government Permits avatar](https://apify.com/img/store/actor_picture.svg)
Scrape Local Government Permits

Pricing

Pricing

from $0.00001 / result

[Try for free](https://console.apify.com/actors/HftrOB3zK2i9YOrdN?addFromActorId=HftrOB3zK2i9YOrdN)

[Go to Apify Store](https://apify.com/store)

![Scrape Local Government Permits](https://apify.com/img/store/actor_picture.svg)

# Scrape Local Government Permits

spec-lab/scrape-local-government-permits

[Try for free](https://console.apify.com/actors/HftrOB3zK2i9YOrdN?addFromActorId=HftrOB3zK2i9YOrdN)

Ask questions about this Actor

Scrapes local government permit and license application pages. Extracts structured data including permit types, requirements, fees, and application procedures from municipal websites. Outputs clean JSON format ready for analysis.

Pricing

from $0.00001 / result

Rating

0.0

(0)

Developer

[![HAYATO YOKOSHIMA](https://apify.com/img/store/user_picture.svg)\\
HAYATO YOKOSHIMA](https://apify.com/spec-lab) Maintained by Community

Actor stats

Bookmarks

0

Bookmarked

Total users

5

Total users

Monthly active users

1

Monthly active users

Last modified

6 months ago

Last modified

Categories

[AI](https://apify.com/store/categories/ai) [Automation](https://apify.com/store/categories/automation) [Jobs](https://apify.com/store/categories/jobs)

Share

[README](https://apify.com/spec-lab/scrape-local-government-permits) [Input](https://apify.com/spec-lab/scrape-local-government-permits/input-schema) [Pricing](https://apify.com/spec-lab/scrape-local-government-permits/pricing) [API](https://apify.com/spec-lab/scrape-local-government-permits/api/python) [Issues](https://apify.com/spec-lab/scrape-local-government-permits/issues/open)

You can access the Scrape Local Government Permits programmatically from your own applications by using the Apify API. You can also choose the language preference from below. To use the Apify API, you’ll need an Apify account and your API token, found in [API & Integrations](https://console.apify.com/settings/integrations) in Apify Console.

[![Python](https://apify.com/img/template-icons/python.svg)\\
Python](https://apify.com/spec-lab/scrape-local-government-permits/api/python) [![JavaScript](https://apify.com/img/template-icons/javascript.svg)\\
JavaScript](https://apify.com/spec-lab/scrape-local-government-permits/api/javascript) [CLI](https://apify.com/spec-lab/scrape-local-government-permits/api/cli) [![OpenAPI](https://apify.com/img/icons/openapi.svg)\\
OpenAPI](https://apify.com/spec-lab/scrape-local-government-permits/api/openapi) [HTTP](https://apify.com/spec-lab/scrape-local-government-permits/api) [MCP](https://apify.com/spec-lab/scrape-local-government-permits/api/mcp)

```bash
# Set API token
$API_TOKEN=<YOUR_API_TOKEN>

# Prepare Actor input
$cat > input.json << 'EOF'
<{
<  "startUrls": [\
<    {\
<      "url": "https://www.buildingpermit.com/reports/monthly.html"\
<    }\
<  ],
<  "proxyConfiguration": {
<    "useApifyProxy": false
<  }
<}
<EOF

# Run the Actor using an HTTP API
# See the full API reference at https://docs.apify.com/api/v2
$curl "https://api.apify.com/v2/actors/spec-lab~scrape-local-government-permits/runs?token=$API_TOKEN" \
<  -X POST \
<  -d @input.json \
<  -H 'Content-Type: application/json'
```

## Scrape Local Government Permits API

Below, you can find a list of relevant HTTP API endpoints for calling the Scrape Local Government Permits Actor. For this, you’ll need an Apify account. Replace<YOUR\_API\_TOKEN> in the URLs with your Apify API token, which you can find under [API & Integrations](https://console.apify.com/settings/integrations) in Apify Console. For details, see the [API reference](https://docs.apify.com/api/v2#/reference/actors).

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

Actors can be used to scrape web pages, extract data, or automate browser tasks. Use the Scrape Local Government Permits API programmatically via the Apify API.

You can choose from:

[![Python](https://apify.com/img/template-icons/python.svg)\\
\\
Scrape Local Government Permits API in Python](https://apify.com/spec-lab/scrape-local-government-permits/api/python) [![JavaScript](https://apify.com/img/template-icons/javascript.svg)\\
\\
Scrape Local Government Permits API in JavaScript](https://apify.com/spec-lab/scrape-local-government-permits/api/javascript) [Scrape Local Government Permits API through CLI](https://apify.com/spec-lab/scrape-local-government-permits/api/cli) [![OpenAPI](https://apify.com/img/icons/openapi.svg)\\
\\
Scrape Local Government Permits OpenAPI definition](https://apify.com/spec-lab/scrape-local-government-permits/api/openapi)

You can start Scrape Local Government Permits with the Apify API by sending an HTTP POST request to the [Run Actor](https://docs.apify.com/api/v2#/reference/actors/run-collection/run-actor) endpoint. An Actor’s input and its content type can be passed as a payload of the POST request, and additional options can be specified using URL query parameters. The Scrape Local Government Permits is identified within the API by its ID, which is the creator’s username and the name of the Actor.

When the Scrape Local Government Permits run finishes you can list the data from its default [dataset](https://docs.apify.com/platform/storage/usage)(storage) via the API or you can preview the data directly on [Apify Console](https://console.apify.com/).

## You might also like

[![🏗️ US Building Permits Scraper — Construction Leads avatar](https://images.apifyusercontent.com/KUMgLDZ238bFiQM0-O0xAWUXcdNGSFwoj3Q-lWRUHE4/rs:fill:76:76/cb:1/aHR0cHM6Ly9hcGlmeS1pbWFnZS11cGxvYWRzLXByb2QuczMudXMtZWFzdC0xLmFtYXpvbmF3cy5jb20vaDA3Y3ZyWVhDNmdHYnkzT2EtYWN0b3ItNFdqaXpYdkl0VmxncTU3UGotWHZReHdCdUxuMi1hSFIwY0hNNkx5OWhjR2xtZVMxcGJXRm5aUzExY0d4dllXUnpMWEJ5YjJRdWN6TXVkWE10WldGemRDMHhMbUZ0.webp)\\
\\
**🏗️ US Building Permits Scraper — Construction Leads**\\
\\
inexhaustible\_glass/us-building-permits-scraper\\
\\
Scrape US building permits from official city open-data APIs. Construction lead-gen for solar, roofing, HVAC & contractors: fresh permits, trade filter, contractor name + phone, owner, project value, lead score. No proxy, no blocks — public records.\\
\\
![User avatar](https://images.apifyusercontent.com/-dGl0H4SMe4cEFtN8UXxE58LOeVSdgZw0FkVyr_0kGY/rs:fill:32:32/cb:1/aHR0cHM6Ly9pbWFnZXMuYXBpZnl1c2VyY29udGVudC5jb20vOXlPcDNDdExSX25iUHB6WVF0aVBYOEFZa1NJbW8yc25BaVBLTVp5akY1RS9yczpmaWxsOjMyOjMyL2NiOjEvYUhSMGNITTZMeTlzYURNdVoyOXZaMnhsZFhObGNtTnZiblJsYm5RdVkyOXRMMkV2UVVObk9HOWpTbnBRTFcxSVozaEJVRmxwTFV0RE9HRnhUR3RtV0RSMVQwNVVRemRyTTFaUlpXZFdTbFkyY1V0WVZrbDBUblpCUFhNNU5pMWo.webp)\\
\\
Hitman studio\\
\\
34\\
\\
5.0\\
\\
(2)](https://apify.com/inexhaustible_glass/us-building-permits-scraper)

[![US Building Permit Scraper — Construction Lead Gen avatar](https://images.apifyusercontent.com/PJsbqy-cuKnlKtVyW-TrGlryG6r5xELMO6pNoWcCaSo/rs:fill:76:76/cb:1/aHR0cHM6Ly9hcGlmeS1pbWFnZS11cGxvYWRzLXByb2QuczMudXMtZWFzdC0xLmFtYXpvbmF3cy5jb20vRlQ1cjdqQkNFd3ZvTHBXbTAtYWN0b3ItZEFXVkFXM1hZUlBjSjlzODMtMW9sZDlMQjhQSS1hcGlmeS1pY29uLWJ1aWxkaW5nLXBlcm1pdC5wbmc.webp)\\
\\
**US Building Permit Scraper — Construction Lead Gen**\\
\\
handstands.io/us-building-permit-scraper\\
\\
Pull building permits from 13 US cities: Chicago, NYC, LA, SF, Seattle, Austin, Cincinnati, Orlando, Baton Rouge, New Orleans, Minneapolis, Baltimore, Tempe. Supports Socrata + ArcGIS portals.\\
\\
![User avatar](https://images.apifyusercontent.com/yy5PY4CZ3b0Xnj8gc_7jhoDSs89ZRNfrZudbEQhuRlk/rs:fill:32:32/cb:1/aHR0cHM6Ly9pbWFnZXMuYXBpZnl1c2VyY29udGVudC5jb20vMWRXMms5eXY3YjZETThGZnc1T2ptbl9jdk0wOXA2T1FXbEpZaTFYSUxlVS9yczpmaWxsOjMyOjMyL2NiOjEvYUhSMGNITTZMeTloY0dsbWVTMXBiV0ZuWlMxMWNHeHZZV1J6TFhCeWIyUXVjek11ZFhNdFpXRnpkQzB4TG1GdFlYcHZibUYzY3k1amIyMHZSbFExY2pkcVFrTkZkM1p2VEhCWGJUQXRjSEp2Wm1sc1pTMTBiR2hGYUdoVGQzaFFMV3h2WjI4dWNHNW4ucG5n.webp)\\
\\
handstands io\\
\\
35](https://apify.com/handstands.io/us-building-permit-scraper)

[![Building Permits Scraper - Contractor & Construction Leads avatar](https://images.apifyusercontent.com/wMABgFd4V2QD0ugqNw_ahmezhaux7FGf39cgELV27C8/rs:fill:76:76/cb:1/aHR0cHM6Ly9hcGlmeS1pbWFnZS11cGxvYWRzLXByb2QuczMudXMtZWFzdC0xLmFtYXpvbmF3cy5jb20vcUhCNFdCdVdsUmtraUdIWXctYWN0b3ItdUlWS0RNa0xVM1ZFZDNOUnEtS0hhVDZKSXVWUy1jbGluaWNhbHRyaWFscy1nb3YucG5n.webp)\\
\\
**Building Permits Scraper - Contractor & Construction Leads**\\
\\
pink\_comic/building-permits-construction-leads\\
\\
Search official building permit records from 47 optimized US city/county sources, with Socrata auto-discovery for others. Find contractor and construction leads with addresses, dates, project descriptions, and available permit values for roofing, HVAC, solar, property research, and sales.\\
\\
![User avatar](https://images.apifyusercontent.com/xHIQ8NPgSWhC7jbdKz1bniz5JDgrODfO99BuuEXmJbQ/rs:fill:32:32/cb:1/aHR0cHM6Ly9pbWFnZXMuYXBpZnl1c2VyY29udGVudC5jb20vV19KMWN2OFBpYlc5enZjT2ZWUVcxTnNyQVk1eU9Sd0F3QkMwWWYzWGpRSS9yczpmaWxsOjMyOjMyL2NiOjEvYUhSMGNITTZMeTloY0dsbWVTMXBiV0ZuWlMxMWNHeHZZV1J6TFhCeWIyUXVjek11ZFhNdFpXRnpkQzB4TG1GdFlYcHZibUYzY3k1amIyMHZjVWhDTkZkQ2RWZHNVbXRyYVVkSVdYY3RjSEp2Wm1sc1pTMW1NakYwYkdwVFFraDNMWE5qY21WbGJuTm9iM1JmTWpBeU5pMHdNeTB5TkY5aGRGODRMalExTGpFMVgwRk5MbkJ1WncucG5n.webp)\\
\\
Ava Torres\\
\\
124](https://apify.com/pink_comic/building-permits-construction-leads)

[GC\\
\\
**Government Compliance Data - EPA, OSHA, Permits — $3.75/1k**\\
\\
fortuitous\_pirate/compliance-data-scraper\\
\\
Scrape EPA ECHO environmental compliance, OSHA workplace inspections, EPA emissions data & building permits. Search by company, location, compliance status. Perfect for due diligence & research. No login or cookies. MCP-ready for AI agents. $3.75 per 1,000 records.\\
\\
![User avatar](https://images.apifyusercontent.com/8JeKpijqTl7G8i50eCe0PpBnie_-hPRhosraMzNT46o/rs:fill:32:32/cb:1/aHR0cHM6Ly9pbWFnZXMuYXBpZnl1c2VyY29udGVudC5jb20vNXNtNUpBWHdTbWxZbVV3VUxQT3AyblFTN1hSZ3JRS3Qtdk1CRmVlMlBfVS9yczpmaWxsOjMyOjMyL2NiOjEvYUhSMGNITTZMeTloZG1GMFlYSnpMbWRwZEdoMVluVnpaWEpqYjI1MFpXNTBMbU52YlM5MUx6RXlNelEwTWpNMU1B.webp)\\
\\
Fortuitous Pirate\\
\\
19](https://apify.com/fortuitous_pirate/compliance-data-scraper)

[![Building Permits Scraper — Contractor & Construction Leads avatar](https://images.apifyusercontent.com/hMORpNAKup7iDcGwMlNZiCIheWRbn8y8vbP831eyp4I/rs:fill:76:76/cb:1/aHR0cHM6Ly9hcGlmeS1pbWFnZS11cGxvYWRzLXByb2QuczMudXMtZWFzdC0xLmFtYXpvbmF3cy5jb20vTWoyS3VleW5sY2NNR1BWdFEtYWN0b3ItQ1dMQ3R1TmIzeWFoNVBUbm8tSHQ4VnNsWTB1RC1pY29uX2J1aWxkaW5nX3Blcm1pdF8xNzczMzc4MTM1MTA4LnBuZw.webp)\\
\\
**Building Permits Scraper — Contractor & Construction Leads**\\
\\
intelscrape/building-permit-scraper\\
\\
Multi-city building permits from city/county open-data APIs. cities\[\] + keyword. Contractor names, addresses, work type. Soft CTA → Skip Trace / UCC / Code Violations.\\
\\
![User avatar](https://images.apifyusercontent.com/tS0qMa1TVozt_YrFKQVQ86NfXv4T3xwyS2sRVxbcIv4/rs:fill:32:32/cb:1/aHR0cHM6Ly9pbWFnZXMuYXBpZnl1c2VyY29udGVudC5jb20vNTdrU1lrdG5acEtpMUwyY2IzOFhLNXdsWXBBUnhxNjVodENtMF9sSGcyby9yczpmaWxsOjMyOjMyL2NiOjEvYUhSMGNITTZMeTloY0dsbWVTMXBiV0ZuWlMxMWNHeHZZV1J6TFhCeWIyUXVjek11ZFhNdFpXRnpkQzB4TG1GdFlYcHZibUYzY3k1amIyMHZUV295UzNWbGVXNXNZMk5OUjFCV2RGRXRjSEp2Wm1sc1pTMUVNRGRvWTFKVlJUY3dMV2x0WVdkbExuQnVady5wbmc.webp)\\
\\
IntelScrape\\
\\
106\\
\\
1.0\\
\\
(1)](https://apify.com/intelscrape/building-permit-scraper)

[![Local Business Email Finder – Owner Emails, Phones & Socials avatar](https://images.apifyusercontent.com/F9MaK12briF3yiwfMRtR-GVOZwoUsnlw9NZjEjp1Nd8/rs:fill:76:76/cb:1/aHR0cHM6Ly9hcGlmeS1pbWFnZS11cGxvYWRzLXByb2QuczMudXMtZWFzdC0xLmFtYXpvbmF3cy5jb20vMHk0cVAyeGJmY2xKT01hR2gtYWN0b3ItSkZIN2NRTGU2Y2QzWGNkUGQtVzl4WXRRdjFCWi1DaGF0R1BUX0ltYWdlX1NlcF8xMF9fMjAyNl9fMDhfNTZfNTVfUE0ucG5n.webp)\\
\\
**Local Business Email Finder – Owner Emails, Phones & Socials**\\
\\
inovaflow/local-business-email-finder\\
\\
Find the owner's or business e-mail of any local business — from a list of names or websites, or a search by category and city. Deep website crawl + long-tail web search, owner name and title, phones and socials; every e-mail verified and tagged with source and confidence. Dataset-only, MCP-ready.\\
\\
![User avatar](https://images.apifyusercontent.com/0TgSgo7L5KerAPPhpoXMHKCQIseMG1DvedUnKn0tZ6w/rs:fill:32:32/cb:1/aHR0cHM6Ly9pbWFnZXMuYXBpZnl1c2VyY29udGVudC5jb20vUlRTakFkMUJVc0hyRE1rdzI1aE9kLWo3Wk1SVFR5bUlLdlN2WWhPd09say9yczpmaWxsOjMyOjMyL2NiOjEvYUhSMGNITTZMeTloY0dsbWVTMXBiV0ZuWlMxMWNHeHZZV1J6TFhCeWIyUXVjek11ZFhNdFpXRnpkQzB4TG1GdFlYcHZibUYzY3k1amIyMHZNSGswY1ZBeWVHSm1ZMnhLVDAxaFIyZ3RjSEp2Wm1sc1pTMXZTRUV4UlRkS2NIcDBMVVoxYkd4TWIyZHZYMVJ5WVc1emNHRnlaVzUwWDA1dlFuVm1abVZ5WHlVeU9ESTJKVEk1TG5CdVp3LnBuZw.webp)\\
\\
inovaflow\\
\\
21](https://apify.com/inovaflow/local-business-email-finder)

[![Local Business  Contact Finder avatar](https://images.apifyusercontent.com/oZatXspT1IbOY45ExJQOgfGJFXfRJpjq4EjivLwp5n4/rs:fill:76:76/cb:1/aHR0cHM6Ly9hcGlmeS1pbWFnZS11cGxvYWRzLXByb2QuczMudXMtZWFzdC0xLmFtYXpvbmF3cy5jb20vZ0xyWlVPSlduOWtmRVppZWUtYWN0b3ItQnNpR29QbTRqOWJYTm1YWTQtZ0t4RnhZMXBPYy1pbWFnZXMuamZpZg.webp)\\
\\
**Local Business Contact Finder**\\
\\
adept-training-center/local-business-contact-finder\\
\\
Local Business Contact Finder: Scrape business directories (like Google Maps or Yelp) to collect contact details, opening hours, and addresses for lead generation or building a local business database.\\
\\
![User avatar](https://images.apifyusercontent.com/zLn0lnh7dO2qZDooRA0yAQXoXClpbRuZMaXrC2j1OHQ/rs:fill:32:32/cb:1/aHR0cHM6Ly9pbWFnZXMuYXBpZnl1c2VyY29udGVudC5jb20vM3FNVzYxSnBQNlB0QVRURGlHWTdqclI5cFJIZXF5YkI5SmxrNTU0dzBpQS9yczpmaWxsOjMyOjMyL2NiOjEvYUhSMGNITTZMeTloY0dsbWVTMXBiV0ZuWlMxMWNHeHZZV1J6TFhCeWIyUXVjek11ZFhNdFpXRnpkQzB4TG1GdFlYcHZibUYzY3k1amIyMHZaMHh5V2xWUFNsZHVPV3RtUlZwcFpXVXRjSEp2Wm1sc1pTMXpjVmxZZFdObFRXOU1MV0Z5Y0hJNExsQk9SeTV3Ym1jLnBuZw.webp)\\
\\
Adept Training Center\\
\\
6](https://apify.com/adept-training-center/local-business-contact-finder)

[![Local Permit & Business License Lead Finder avatar](https://images.apifyusercontent.com/-v9SAztamqEdAgNDpKnHBabXamCCi2R0N5I-jxSyS28/rs:fill:76:76/cb:1/aHR0cHM6Ly9hcGlmeS1pbWFnZS11cGxvYWRzLXByb2QuczMudXMtZWFzdC0xLmFtYXpvbmF3cy5jb20vSFNPS0lUcldBT1B0emZBaUItYWN0b3ItRXZaOXJwZTNjMFpJcUg4Z2wtZjZ4ZTVLaWprNi1HZW5lcmF0ZWRfaW1hZ2VfMV8lMjgxNiUyOS5wbmc.webp)\\
\\
**Local Permit & Business License Lead Finder**\\
\\
glowing\_glove/local-permit-business-license-lead-finder\\
\\
Find local permit, license, and public-government lead signals for contractors, suppliers, agencies, and B2B sales teams.\\
\\
![User avatar](https://images.apifyusercontent.com/blEZDwCYJeC_3OR4Scwz-GsGUkfu1_Hz_LyNDLBbJM0/rs:fill:32:32/cb:1/aHR0cHM6Ly9pbWFnZXMuYXBpZnl1c2VyY29udGVudC5jb20vWWVPVUN3ZXhGcGxSYzlHNmRndU5ROG5YTWQxbFhVRHF6VTNlajl1REw5RS9yczpmaWxsOjMyOjMyL2NiOjEvYUhSMGNITTZMeTlzYURNdVoyOXZaMnhsZFhObGNtTnZiblJsYm5RdVkyOXRMMkV2UVVObk9HOWpTaTB4UjBsSGQyNURPR3BXYWxCM1QzSktWMjU0VUZaMWVHRnNlRmhIUjBodmRIVXRhVmMwYUZac1VFUlpiVE5pTW1rOWN6azJMV00.webp)\\
\\
Ushba Khan\\
\\
2](https://apify.com/glowing_glove/local-permit-business-license-lead-finder)

[![Building Permits Scraper — Construction Leads avatar](https://images.apifyusercontent.com/7ng8RygEM94FtGVqcuGutN2Hlr1m5vUC7jVVjqehaBo/rs:fill:76:76/cb:1/aHR0cHM6Ly9hcGlmeS1pbWFnZS11cGxvYWRzLXByb2QuczMudXMtZWFzdC0xLmFtYXpvbmF3cy5jb20vYWhOZlV1R0toSUh1NlNsTkEtYWN0b3ItMHB2d1dnQUhVTmwxNVJWRmgtZHlWQkZSQ0lvWS1idWlsZGluZy1wZXJtaXRzLnBuZw.webp)\\
\\
**Building Permits Scraper — Construction Leads**\\
\\
4l3c/building-permits-scraper\\
\\
Fresh building permit data from 11 verified city & county open-data APIs: Chicago, NYC, LA, Austin, SF, Seattle, Miami, Miami-Dade, Maricopa, New Orleans, Philadelphia. Roofing, solar, HVAC & remodeling leads with contractor and valuation data. Reliable government sources, no proxies, no breakage.\\
\\
![User avatar](https://images.apifyusercontent.com/MX-TkqV4I1mMwIOD5eC1ve_NiNoKQBawURS2FmONylw/rs:fill:32:32/cb:1/aHR0cHM6Ly9pbWFnZXMuYXBpZnl1c2VyY29udGVudC5jb20vbkpudzlpMTJfb3VwVTVNaC1VZzVUY3BYelBheVp5Y0g3LWtBVGpnazd1dy9yczpmaWxsOjMyOjMyL2NiOjEvYUhSMGNITTZMeTloY0dsbWVTMXBiV0ZuWlMxMWNHeHZZV1J6TFhCeWIyUXVjek11ZFhNdFpXRnpkQzB4TG1GdFlYcHZibUYzY3k1amIyMHZZV2hPWmxWMVIwdG9TVWgxTmxOc1RrRXRjSEp2Wm1sc1pTMTFiR1JZU2s5bmEzTTVMV1V6WVRrMllXVmpMVE0yTURZdE5ETTNZUzA1WXprMUxUQXlPVGxtTkRVelptVTNNQzVxY0djLmpwZw.webp)\\
\\
Alec\\
\\
18](https://apify.com/4l3c/building-permits-scraper)

[![Chicago Building Permits Scraper avatar](https://images.apifyusercontent.com/IZxdkLuZ16zPuUyyFgKx9ELTF7nAqNnkLZrg5e8LAQo/rs:fill:76:76/cb:1/aHR0cHM6Ly9hcGlmeS1pbWFnZS11cGxvYWRzLXByb2QuczMudXMtZWFzdC0xLmFtYXpvbmF3cy5jb20vZ2VMWE9ZV3FqY0FjWng0TDAtYWN0b3ItY2hHWVNENXhwakNFYVpLdnctUmJrUFhWakhSNC1pY29uLXVwbG9hZC1hNTVhODU3MC0wNDMyLTQxNDktYjkxMS03ZTE2NjgzOWQyOTIucG5n.webp)\\
\\
**Chicago Building Permits Scraper**\\
\\
maximedupre/chicago-building-permits\\
\\
Search the official City of Chicago building-permit dataset by date, status, work type, location, contact, cost, or exact permit ID. Save structured permit details, project scope, fees, contacts, and source links for construction and property research.\\
\\
![User avatar](https://images.apifyusercontent.com/rphAVS3cnUgZlUxGcpMm57KYTFWYekrE_5yAgDTZm-E/rs:fill:32:32/cb:1/aHR0cHM6Ly9pbWFnZXMuYXBpZnl1c2VyY29udGVudC5jb20vdHROY21HdkhUcmFXQ0F3WktNdlFROTAxZHdlZTU0eWVlMmhad0pLVXNGQS9yczpmaWxsOjMyOjMyL2NiOjEvYUhSMGNITTZMeTloY0dsbWVTMXBiV0ZuWlMxMWNHeHZZV1J6TFhCeWIyUXVjek11ZFhNdFpXRnpkQzB4TG1GdFlYcHZibUYzY3k1amIyMHZaMlZNV0U5WlYzRnFZMEZqV25nMFREQXRjSEp2Wm1sc1pTMHpRbXRRVFVkeVVGWkVMVU5vWVhSSFVGUmZTVzFoWjJWZlFYQnlYekl4WDE4eU1ESTJYMTh4TUY4MU0xODFORjlCVFM1d2JtYy5wbmc.webp)\\
\\
Maxime Dupré\\
\\
2](https://apify.com/maximedupre/chicago-building-permits)
