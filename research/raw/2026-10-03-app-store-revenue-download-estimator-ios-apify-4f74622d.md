---
url: https://apify.com/seibs.co/app-store-revenue-estimator/api/mcp
retrieved: 2026-10-03
command: firecrawl scrape https://apify.com/seibs.co/app-store-revenue-estimator/api/mcp --only-main-content --json
statusCode: 200
transport: firecrawl-cli
completeness: full
title: App Store Revenue & Download Estimator - iOS and Google Play MCP server · Apify
---
![App Store Revenue & Download Estimator - iOS and Google Play avatar](https://apify.com/img/store/actor_picture.svg)
App Store Revenue & Download Estimator - iOS and Google Play

Pricing

Pricing

from $10.00 / 1,000 app records

[Try for free](https://console.apify.com/actors/QgXeAHeSV8FhvNbFD?addFromActorId=QgXeAHeSV8FhvNbFD)

[Go to Apify Store](https://apify.com/store)

![App Store Revenue & Download Estimator - iOS and Google Play](https://apify.com/img/store/actor_picture.svg)

# App Store Revenue & Download Estimator - iOS and Google Play

seibs.co/app-store-revenue-estimator

[Try for free](https://console.apify.com/actors/QgXeAHeSV8FhvNbFD?addFromActorId=QgXeAHeSV8FhvNbFD)

Ask questions about this Actor

Estimate App Store and Google Play downloads and revenue from public signals (rank, rank history, ratings velocity, review deltas). Per-app records, modeled estimate bands, and publisher rollups. For app devs, UA/growth teams, and investors - the gated Sensor Tower/data.ai layer, priced per call.

Pricing

from $10.00 / 1,000 app records

Rating

0.0

(0)

Developer

[![Seibs.co](https://apify.com/img/store/user_picture.svg)\\
Seibs.co](https://apify.com/seibs.co) Maintained by Community

Actor stats

Bookmarks

0

Bookmarked

Total users

58

Total users

Monthly active users

22

Monthly active users

Last modified

5 days ago

Last modified

Categories

[Business](https://apify.com/store/categories/business) [Marketing](https://apify.com/store/categories/marketing) [E-commerce](https://apify.com/store/categories/ecommerce)

Share

[README](https://apify.com/seibs.co/app-store-revenue-estimator) [Input](https://apify.com/seibs.co/app-store-revenue-estimator/input-schema) [Output](https://apify.com/seibs.co/app-store-revenue-estimator/output-schema) [Pricing](https://apify.com/seibs.co/app-store-revenue-estimator/pricing) [API](https://apify.com/seibs.co/app-store-revenue-estimator/api/python) [Issues](https://apify.com/seibs.co/app-store-revenue-estimator/issues/open) [Changelog](https://apify.com/seibs.co/app-store-revenue-estimator/changelog)

You can access the App Store Revenue & Download Estimator - iOS and Google Play programmatically from your own applications by using the Apify API. You can also choose the language preference from below. To use the Apify API, you’ll need an Apify account and your API token, found in [API & Integrations](https://console.apify.com/settings/integrations) in Apify Console.

[![Python](https://apify.com/img/template-icons/python.svg)\\
Python](https://apify.com/seibs.co/app-store-revenue-estimator/api/python) [![JavaScript](https://apify.com/img/template-icons/javascript.svg)\\
JavaScript](https://apify.com/seibs.co/app-store-revenue-estimator/api/javascript) [CLI](https://apify.com/seibs.co/app-store-revenue-estimator/api/cli) [![OpenAPI](https://apify.com/img/icons/openapi.svg)\\
OpenAPI](https://apify.com/seibs.co/app-store-revenue-estimator/api/openapi) [HTTP](https://apify.com/seibs.co/app-store-revenue-estimator/api) [MCP](https://apify.com/seibs.co/app-store-revenue-estimator/api/mcp)

```json
{
    "mcpServers": {
        "apify": {
            "type": "http",
            "url": "https://mcp.apify.com/?tools=fetch-actor-details,seibs.co/app-store-revenue-estimator"
        }
    }
}
```

## Configure MCP server with App Store Revenue & Download Estimator - iOS and Google Play

The configuration above connects to the hosted Apify MCP server with the App Store Revenue & Download Estimator - iOS and Google Play Actor already loaded. It uses OAuth, so your client opens a browser window to sign you in to Apify on first use. No API token is needed. Clients without OAuth support can authenticate with an`Authorization: Bearer` header carrying an API token from [API & Integrations](https://console.apify.com/settings/integrations) in Apify Console.

Get a ready-to-use configuration for your MCP client with the App Store Revenue & Download Estimator - iOS and Google Play Actor preconfigured at [https://mcp.apify.com/?tools=fetch-actor-details,seibs.co/app-store-revenue-estimator](https://mcp.apify.com/?tools=fetch-actor-details,seibs.co/app-store-revenue-estimator).

You can connect to [the Apify MCP Server](https://mcp.apify.com/) using clients like [Tester MCP Client](https://apify.com/jiri.spilka/tester-mcp-client), or any other [MCP client](https://modelcontextprotocol.io/clients) of your choice.

If you want to learn more about our Apify MCP implementation, check out our [MCP documentation](https://docs.apify.com/platform/integrations/mcp). To learn more about the Model Context Protocol in general, refer to the [official MCP documentation](https://modelcontextprotocol.io/introduction) or read [our blog post](https://blog.apify.com/what-is-model-context-protocol).

## You might also like

[![Top Ranking Mobile Apps avatar](https://images.apifyusercontent.com/Jl9HYjaF2HCiFq9T71iwgwsul-7q-1Dq23KrC8V3BoA/rs:fill:76:76/cb:1/aHR0cHM6Ly9hcGlmeS1pbWFnZS11cGxvYWRzLXByb2QuczMudXMtZWFzdC0xLmFtYXpvbmF3cy5jb20vSFZEbjBqeTRKQnJNOVNDanctYWN0b3ItbkdBaGFpc1RFeno3bG1rNFYtT2RJdXNIaFYzMy1tb2JpbGUtY2xvdWRfMTU5ODQ5ODQucG5n.webp)\\
\\
**Top Ranking Mobile Apps**\\
\\
codebyte/top-ranking-mobile-apps\\
\\
Scrape top trending apps for both Apple App Store and Google Play Store. Extract by category, country, device, and date including download estimates, revenue estimates, ratings, publisher info and pricing data. Monitor competitor rankings, track market trends, measure app performance across regions.\\
\\
![User avatar](https://images.apifyusercontent.com/g-XUnhlIIMtuWKu14jr_Ubb_W-iCvJRyoudSD5_j9EE/rs:fill:32:32/cb:1/aHR0cHM6Ly9pbWFnZXMuYXBpZnl1c2VyY29udGVudC5jb20vLXkwVThPaFZsTVBaLU5qdGFxX0s0d1FVRlZCN0g1SmN1aV9HbXNFTG56dy9yczpmaWxsOjMyOjMyL2NiOjEvYUhSMGNITTZMeTkzZDNjdVozSmhkbUYwWVhJdVkyOXRMMkYyWVhSaGNpOHhPVGN4TmpZNU1XVTRPVEkyTnpBM01ERXlPVEpoTVRrMU1EWmxPR05oWlQ5a1BXaDBkSEJ6SlROQkpUSkdKVEpHWTJSdUxtRndhV1o1TG1OdmJTVXlSbWx0WnlVeVJtbGpiMjV6SlRKR1lXNXZibmx0YjNWelgzVnpaWEpmY0dsamRIVnlaUzV3Ym1j.webp)\\
\\
Codebyte\\
\\
84](https://apify.com/codebyte/top-ranking-mobile-apps)

[![App Store Scraper (from $0.10/1,000 apps) - Apple iOS Data avatar](https://images.apifyusercontent.com/QfGCaFphje6dsNhvF2FgA8NZt6wBPjT5w14-zVp2MMw/rs:fill:76:76/cb:1/aHR0cHM6Ly9hcGlmeS1pbWFnZS11cGxvYWRzLXByb2QuczMuYW1hem9uYXdzLmNvbS8xanVCbDZRZWRXSjNid2JnWi9QY0U1N3VBYWZqZDRQOWlGZi1pY29uX2FwcHN0b3JlX19ldjB6Nzcwenl4b3lfbGFyZ2VfMngucG5n.webp)\\
\\
**App Store Scraper (from $0.10/1,000 apps) - Apple iOS Data**\\
\\
epctex/appstore-scraper\\
\\
Search the App Store by keyword, or look up apps by App Store ID, bundle ID, or developer ID. First 50 free, then $0.10/1,000 (search) or $0.40/1,000 for direct lookups, 45 fields per app. Reviews from $0.10/1,000, similar apps from $0.01/1,000, as add-ons. Fits ASO teams, publishers, researchers.\\
\\
![User avatar](https://images.apifyusercontent.com/8mPoO24sM5-ntL8gkoqmL7u3aUNKuBebtvTVMQstXxM/rs:fill:32:32/cb:1/aHR0cHM6Ly9pbWFnZXMuYXBpZnl1c2VyY29udGVudC5jb20vd3ZxTW02YUlwVDdvay00NFN6N1M2RElGVnhKbHZwTXhwQVhGdklmeENscy9yczpmaWxsOjMyOjMyL2NiOjEvYUhSMGNITTZMeTloY0dsbWVTMXBiV0ZuWlMxMWNHeHZZV1J6TFhCeWIyUXVjek11WVcxaGVtOXVZWGR6TG1OdmJTOHpjV2hCWTFNeldsSktTelJoTjNWT1J5OW9jelpyTlhvMmFrTk5Oa3BIWTNVMFFpMXpjWFZoY21VdFlteGhZMnN1Y0c1bi5wbmc.webp)\\
\\
epctex\\
\\
1.1K\\
\\
5.0\\
\\
(10)](https://apify.com/epctex/appstore-scraper)

[![App Store Reviews Scraper API | $0.10/1K Reviews avatar](https://images.apifyusercontent.com/Pa1UJJzZsKmUcArRo-Ncw8x1unQGydn4Ri5gyrUcf4k/rs:fill:76:76/cb:1/aHR0cHM6Ly9hcGlmeS1pbWFnZS11cGxvYWRzLXByb2QuczMudXMtZWFzdC0xLmFtYXpvbmF3cy5jb20vNHFSZ2g1dlhYc3YwYkthMWwvd1o0eFh5czNNejNmZ1VmMnUtYXBwc3RvcmUucG5n.webp)\\
\\
**App Store Reviews Scraper API \| $0.10/1K Reviews**\\
\\
thewolves/appstore-reviews-scraper\\
\\
App Store Reviews Scraper is your ultimate tool to retrieve the reviews directly from the Apple Store. With extremely capable information retrieval, the lowest price, and lightning speed, this actor is unbeatable. It's priced at just $0.10 per 1000 reviews!\\
\\
![User avatar](https://images.apifyusercontent.com/y2b3AkXB5OZwY_cXnyiQpIhVgbZySiaFb7aHKB7gUL0/rs:fill:32:32/cb:1/aHR0cHM6Ly9pbWFnZXMuYXBpZnl1c2VyY29udGVudC5jb20vTFRSTzJQYVNVNF92Y2NYMV9yYVBFNGwybmVsSE8weklnLV9vcHlfdTJ0NC9yczpmaWxsOjMyOjMyL2NiOjEvYUhSMGNITTZMeTloY0dsbWVTMXBiV0ZuWlMxMWNHeHZZV1J6TFhCeWIyUXVjek11ZFhNdFpXRnpkQzB4TG1GdFlYcHZibUYzY3k1amIyMHZaazFwTmxSRlREVkdZamhyTWt0QlZFWXZaMGhhTjJkeE5HMXZPRFpUZG5oNk1Ha3RiRzluYnk1cWNHVm4uanBlZw.webp)\\
\\
The Wolves\\
\\
2.3K\\
\\
5.0\\
\\
(10)](https://apify.com/thewolves/appstore-reviews-scraper)

[![Apple App Store Scraper avatar](https://images.apifyusercontent.com/0ZWfaOhi_bz6E1JSxSMa-96VDWRI6phFlyb1Qreb774/rs:fill:76:76/cb:1/aHR0cHM6Ly9hcGlmeS1pbWFnZS11cGxvYWRzLXByb2QuczMudXMtZWFzdC0xLmFtYXpvbmF3cy5jb20vbnRIQ25oTlVrelhSN25iVVotYWN0b3ItcUIzM0FtNkYyanVjNVhsYVYtZ0RvMHAzQWRhYS1hY3Rvci1pY29uLnBuZw.webp)\\
\\
**Apple App Store Scraper**\\
\\
automation-lab/apple-app-store-scraper\\
\\
Extract Apple App Store data: app details, ratings, reviews, and search results. Get app name, developer, price, rating, description, screenshots, and 30+ fields. Export to JSON, CSV, or Excel. No API key or login required.\\
\\
![User avatar](https://images.apifyusercontent.com/K_C4LOMfOgJZv5UcVqbze6xlfc6mS23zsoHRS5nDXvM/rs:fill:32:32/cb:1/aHR0cHM6Ly9pbWFnZXMuYXBpZnl1c2VyY29udGVudC5jb20vMDdsSFdveGptQlpJN0NMWkJqVi1wUlBjV0ZHRFQyRzIwVjdkVzBRSzBCay9yczpmaWxsOjMyOjMyL2NiOjEvYUhSMGNITTZMeTloY0dsbWVTMXBiV0ZuWlMxMWNHeHZZV1J6TFhCeWIyUXVjek11ZFhNdFpXRnpkQzB4TG1GdFlYcHZibUYzY3k1amIyMHZiblJJUTI1b1RsVnJlbGhTTjI1aVZWb3RjSEp2Wm1sc1pTMW9ORkJYYTNsWWVVSmxMV0YxZEc5dFlYUnBiMjR0YkdGaUxYQnliMlpwYkdVdGJHOW5ieTV3Ym1jLnBuZw.webp)\\
\\
Automation Lab\\
\\
580\\
\\
5.0\\
\\
(1)](https://apify.com/automation-lab/apple-app-store-scraper)

[![Google Play Store Scraper avatar](https://images.apifyusercontent.com/jfUoHSXP2dYRiJOdNBk7b9_If7FwLdp8868VAnT7mpg/rs:fill:76:76/cb:1/aHR0cHM6Ly9hcGlmeS1pbWFnZS11cGxvYWRzLXByb2QuczMudXMtZWFzdC0xLmFtYXpvbmF3cy5jb20vbnRIQ25oTlVrelhSN25iVVotYWN0b3ItWW03YkhYNnhhZnFOZ0ZaZ08ta3NXN1lCN09pby1hY3Rvci1pY29uLnBuZw.webp)\\
\\
**Google Play Store Scraper**\\
\\
automation-lab/google-play-scraper\\
\\
Scrape Google Play Store — app details, ratings, reviews, and search results. Extract app name, developer, installs, rating, price, screenshots, and 30+ fields. No API key needed.\\
\\
![User avatar](https://images.apifyusercontent.com/K_C4LOMfOgJZv5UcVqbze6xlfc6mS23zsoHRS5nDXvM/rs:fill:32:32/cb:1/aHR0cHM6Ly9pbWFnZXMuYXBpZnl1c2VyY29udGVudC5jb20vMDdsSFdveGptQlpJN0NMWkJqVi1wUlBjV0ZHRFQyRzIwVjdkVzBRSzBCay9yczpmaWxsOjMyOjMyL2NiOjEvYUhSMGNITTZMeTloY0dsbWVTMXBiV0ZuWlMxMWNHeHZZV1J6TFhCeWIyUXVjek11ZFhNdFpXRnpkQzB4TG1GdFlYcHZibUYzY3k1amIyMHZiblJJUTI1b1RsVnJlbGhTTjI1aVZWb3RjSEp2Wm1sc1pTMW9ORkJYYTNsWWVVSmxMV0YxZEc5dFlYUnBiMjR0YkdGaUxYQnliMlpwYkdVdGJHOW5ieTV3Ym1jLnBuZw.webp)\\
\\
Automation Lab\\
\\
787\\
\\
5.0\\
\\
(3)](https://apify.com/automation-lab/google-play-scraper)

[![Similarweb Scraper - Traffic, AI Traffic & WHOIS avatar](https://images.apifyusercontent.com/Vwonnr74D6o3VxIylzyhgRLWTEgvjBzDWsWK9xXbRtI/rs:fill:76:76/cb:1/aHR0cHM6Ly9hcGlmeS1pbWFnZS11cGxvYWRzLXByb2QuczMudXMtZWFzdC0xLmFtYXpvbmF3cy5jb20vTzM3VUI4dVdFbmo1OXJWZDQtYWN0b3ItSzF1TGJleVpnWUFvTWd2d0ktVXJrNzhKendBbC1zaW1pbGFyd2ViX2xvZ28ucG5n.webp)\\
\\
**Similarweb Scraper - Traffic, AI Traffic & WHOIS**\\
\\
vortex\_data/similarweb-scraper\\
\\
🔍 Spy on any website in seconds: traffic, rankings, top keywords, AI traffic share (ChatGPT/Claude/Gemini), competitors, similar sites & WHOIS — all from Similarweb. No login or API key. Bulk parallel scrape, captcha-resilient. Export to JSON/CSV/Excel. SEO, lead gen, research.\\
\\
![User avatar](https://images.apifyusercontent.com/K9Xj3VX98sJnIR3gO3LmzPSRobxjEkKP-kSminffR2U/rs:fill:32:32/cb:1/aHR0cHM6Ly9pbWFnZXMuYXBpZnl1c2VyY29udGVudC5jb20vd25SNVJKZXUtcDJFM3ByZ2Q2dzNzZVE3X1pJRGw0QzdtbjlQMWRfZ1c3NC9yczpmaWxsOjMyOjMyL2NiOjEvYUhSMGNITTZMeTloY0dsbWVTMXBiV0ZuWlMxMWNHeHZZV1J6TFhCeWIyUXVjek11ZFhNdFpXRnpkQzB4TG1GdFlYcHZibUYzY3k1amIyMHZUek0zVlVJNGRWZEZibW8xT1hKV1pEUXRjSEp2Wm1sc1pTMHhNa3RZVW5CR2NreG9MVU5vWVhSSFVGUmZTVzFoWjJWZk0xOWZYMTlmTWpBeU5sOWZMbDlmTURaZk16SmZOVE11Y0c1bi5wbmc.webp)\\
\\
VortexData\\
\\
511\\
\\
5.0\\
\\
(2)](https://apify.com/vortex_data/similarweb-scraper)

[![Mobile App Revenue & Competitor Analyzer | Downloads Estimate avatar](https://images.apifyusercontent.com/nrO2Bc99TE79CHRF_77xie_NqXSO9p1PEyjO25eJajk/rs:fill:76:76/cb:1/aHR0cHM6Ly9hcGlmeS1pbWFnZS11cGxvYWRzLXByb2QuczMudXMtZWFzdC0xLmFtYXpvbmF3cy5jb20veUQ1VWZUNmJhbmR2eW03NTYtYWN0b3Itb1VMdGFVSEtTNHlhNXVhU3EtUFJ0eEJteU8zZy1hcHAtcmV2ZW51ZS1hbmFseXplci5qcGc.webp)\\
\\
**Mobile App Revenue & Competitor Analyzer \| Downloads Estimate**\\
\\
apivault\_labs/app-revenue-analyzer\\
\\
Estimate any iOS app's revenue and downloads: bands with confidence, chart positions, update cadence, in-app purchases, developer portfolio and 8 direct competitors. Keyword search mode for ASO. Bulk, no login, no API key. \ per 1,000 reports. CSV/JSON/Excel/API.\\
\\
![User avatar](https://images.apifyusercontent.com/eP0jKApGrxNpVvW77QOMpwULclV41A4L2avtvLG4wmo/rs:fill:32:32/cb:1/aHR0cHM6Ly9pbWFnZXMuYXBpZnl1c2VyY29udGVudC5jb20vOHBNNFZ0Vm9EcDVhUWRzVFJ2QzREZGJEZWVKY0thelZDdy1jZzVndzBGcy9yczpmaWxsOjMyOjMyL2NiOjEvYUhSMGNITTZMeTloY0dsbWVTMXBiV0ZuWlMxMWNHeHZZV1J6TFhCeWIyUXVjek11ZFhNdFpXRnpkQzB4TG1GdFlYcHZibUYzY3k1amIyMHZlVVExVldaVU5tSmhibVIyZVcwM05UWXRjSEp2Wm1sc1pTMTFURkZ6UkU0elJIaDVMV1psTkRoaU5EVTFMV1E1TmprdE5ESTNOaTFoTjJZM0xUTTROVEJqTlRRMVpERXhZekUzTnpNMU16VXlNekV3TWpZdFozVTRhSHA2ZGpVd2FTNXdibWMucG5n.webp)\\
\\
Apivault Labs\\
\\
6](https://apify.com/apivault_labs/app-revenue-analyzer)

[AS\\
\\
**App Store Revenue & Download Estimator - MCP Server**\\
\\
seibs.co/mcp-app-store-revenue-estimator\\
\\
MCP server for app-store-revenue-estimator. AI-agent tools for App Store and Google Play download/revenue estimates, rank history, and publisher rollups. x402 (USDC on Base) and Skyfire agentic-payment ready. For app devs, UA teams, and app investors.\\
\\
![User avatar](https://images.apifyusercontent.com/29eXpPbTd32SJTXKk7DZBu2qvCw1Ik3IpgcctL20-Wk/rs:fill:32:32/cb:1/aHR0cHM6Ly9pbWFnZXMuYXBpZnl1c2VyY29udGVudC5jb20vZkhPQVpBcUt2RDRXaFlkVTJuUlkxamFJbF9sSjRfcmZpeVNWWDRLdEVhay9yczpmaWxsOjMyOjMyL2NiOjEvYUhSMGNITTZMeTloY0dsbWVTMXBiV0ZuWlMxMWNHeHZZV1J6TFhCeWIyUXVjek11ZFhNdFpXRnpkQzB4TG1GdFlYcHZibUYzY3k1amIyMHZNbVExZUVkeVUyTmhPSGhDUVZOeWNtd3RjSEp2Wm1sc1pTMXphMUUxWkV4eVJrYzFMWE5sYVdKemJHOW5ieTV3Ym1jLnBuZw.webp)\\
\\
Seibs.co\\
\\
3](https://apify.com/seibs.co/mcp-app-store-revenue-estimator)

[![TikTok Ads Library Scraper — EU Library & Creative Center avatar](https://images.apifyusercontent.com/YWcR6kU0yFcXugUdp7Lb7BcWXnGDngmtdL9yOZ7rhUw/rs:fill:76:76/cb:1/aHR0cHM6Ly9hcGlmeS1pbWFnZS11cGxvYWRzLXByb2QuczMudXMtZWFzdC0xLmFtYXpvbmF3cy5jb20veGxsMEJId0VjbUZaelNaMEgtYWN0b3Itc2FYRW1TS2hRZjRZU1VCclYtcXB0UzZDRXhwVy1HZW1pbmlfR2VuZXJhdGVkX0ltYWdlX3U2b2doNXU2b2doNXU2b2cucG5n.webp)\\
\\
**TikTok Ads Library Scraper — EU Library & Creative Center**\\
\\
brilliant\_gum/tiktok-ads-library-scraper\\
\\
Scrape TikTok Ads Library (EU/EEA/UK) and Creative Center (global). Extract ad creatives, targeting data, reach estimates, CTR, video URLs, and industry insights. Dual-source coverage — no login required. Residential proxies built-in.\\
\\
![User avatar](https://images.apifyusercontent.com/Wzp7UhDSjhaq-pnZTFbsBCn-RljHmVGhYzJ3EfGJOuA/rs:fill:32:32/cb:1/aHR0cHM6Ly9pbWFnZXMuYXBpZnl1c2VyY29udGVudC5jb20vZXUzd0dKbWxVQ2VYejdQNWI5TzJOQk1YVkt3WjNzemZwbHBzTHR2VHBLUS9yczpmaWxsOjMyOjMyL2NiOjEvYUhSMGNITTZMeTloY0dsbWVTMXBiV0ZuWlMxMWNHeHZZV1J6TFhCeWIyUXVjek11ZFhNdFpXRnpkQzB4TG1GdFlYcHZibUYzY3k1amIyMHZlR3hzTUVKSWQwVmpiVVphZWxOYU1FZ3RjSEp2Wm1sc1pTMXhjMmRJUWtGalEyaG9MVWRsYldsdWFWOUhaVzVsY21GMFpXUmZTVzFoWjJWZmFEZHVjR0p5YURkdWNHSnlhRGR1Y0M1d2JtYy5wbmc.webp)\\
\\
Yuliia Kulakova\\
\\
454](https://apify.com/brilliant_gum/tiktok-ads-library-scraper)

[MA\\
\\
**Mobile App Intelligence API - Downloads, Revenue, Ranks**\\
\\
nabeelbaghoor/mobile-app-intelligence-api\\
\\
App Store and Google Play data as rows: app metadata, modelled download and revenue estimates by country and day, top chart positions, store reviews and daily, weekly and monthly active users. Read one app, a publisher's whole catalogue or a whole chart. Bring your own key.\\
\\
![User avatar](https://images.apifyusercontent.com/N5BXXkDuLbfeQd4735e15yPK_0fc0r_frdtpeslpm3E/rs:fill:32:32/cb:1/aHR0cHM6Ly9pbWFnZXMuYXBpZnl1c2VyY29udGVudC5jb20vb3ZmR29HSVVnR29BT05RYWw4Tk4xdHNoTzNreTl4b2tzY0kwUm9EY0RqYy9yczpmaWxsOjMyOjMyL2NiOjEvYUhSMGNITTZMeTlzYURNdVoyOXZaMnhsZFhObGNtTnZiblJsYm5RdVkyOXRMMkV2UVVObk9HOWpTbll5ZDJWT04zZGhYMmRpWldJek1teHVPRWd5UVUxUlRGUnhOUzF2ZGpGRWMxWk1MVTR6VUdzMWVYUmtUakpSV21ROWN6azJMV00.webp)\\
\\
Nabeel Hassan\\
\\
3](https://apify.com/nabeelbaghoor/mobile-app-intelligence-api)
