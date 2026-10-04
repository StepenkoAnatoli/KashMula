---
url: https://pypi.org/project/apify/
retrieved: 2026-10-04
command: firecrawl scrape https://pypi.org/project/apify/ --only-main-content --json
statusCode: 200
transport: firecrawl-cli
completeness: full
title: apify · PyPI
---
[Skip to main content](https://pypi.org/project/apify/#content) Switch to mobile version

Search PyPISearch

# apify 4.0.2

Apify SDK for Python

pip install apifyCopy PIP instructions

# Apify SDK for Python

**The official Python SDK for building [Apify Actors](https://docs.apify.com/platform/actors).**

[![PyPI version](https://pypi-camo.freetls.fastly.net/3bca98f09272add3eebd0b370c47302951fd4ab8/68747470733a2f2f62616467652e667572792e696f2f70792f61706966792e737667)](https://pypi.org/project/apify/)[![PyPI downloads](https://pypi-camo.freetls.fastly.net/fb4ce77262bfa6575abedcf0100198b0852a7ca3/68747470733a2f2f696d672e736869656c64732e696f2f707970692f646d2f6170696679)](https://pypi.org/project/apify/)[![Python versions](https://pypi-camo.freetls.fastly.net/d1b8432486e8eaa505d6dfecced0e9bf7d2c7892/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f707974686f6e2d332e31312532422d626c7565)](https://pypi.org/project/apify/)[![Build status](https://pypi-camo.freetls.fastly.net/3700596454a73f4d9bc0532aaa07beafd5a6a00c/68747470733a2f2f6769746875622e636f6d2f61706966792f61706966792d73646b2d707974686f6e2f616374696f6e732f776f726b666c6f77732f6f6e5f6d61737465722e79616d6c2f62616467652e7376673f6272616e63683d6d6173746572)](https://github.com/apify/apify-sdk-python/actions/workflows/on_master.yaml)[![Coverage](https://pypi-camo.freetls.fastly.net/44275d745c6e48371a4066ba91fa5592fba84f84/68747470733a2f2f636f6465636f762e696f2f67682f61706966792f61706966792d73646b2d707974686f6e2f67726170682f62616467652e7376673f746f6b656e3d59364a42495a51465436)](https://codecov.io/gh/apify/apify-sdk-python)[![License](https://pypi-camo.freetls.fastly.net/5c19631838d7b5e154e83e54f4daece508052f4a/68747470733a2f2f696d672e736869656c64732e696f2f707970692f6c2f6170696679)](https://github.com/apify/apify-sdk-python/blob/master/LICENSE)[![Chat on Discord](https://pypi-camo.freetls.fastly.net/74af4511b5626135094374616646c33307c4d715/68747470733a2f2f696d672e736869656c64732e696f2f646973636f72642f3830313136333731373931353537343332333f6c6162656c3d646973636f7264)](https://discord.gg/jyEM2PRvMU)

`apify` is the official SDK for building [Apify Actors](https://docs.apify.com/platform/actors) in Python. It handles the Actor lifecycle, [storage](https://docs.apify.com/platform/storage) access, platform events, [Apify Proxy](https://docs.apify.com/platform/proxy), pay-per-event charging, and more.

> If you only need to **consume** the [Apify API](https://docs.apify.com/api/v2) from Python (running Actors, reading datasets, managing storages) rather than building Actors, use the [Apify API client for Python](https://docs.apify.com/api/client/python) instead. It comes bundled with this SDK.

## Table of contents

- [Installation](https://pypi.org/project/apify/#user-content-installation)
- [Quick start](https://pypi.org/project/apify/#user-content-quick-start)
- [What are Actors?](https://pypi.org/project/apify/#user-content-what-are-actors)
- [Features](https://pypi.org/project/apify/#user-content-features)
- [What you can build](https://pypi.org/project/apify/#user-content-what-you-can-build)
- [Usage examples](https://pypi.org/project/apify/#user-content-usage-examples)
- [Documentation](https://pypi.org/project/apify/#user-content-documentation)
- [Related projects](https://pypi.org/project/apify/#user-content-related-projects)
- [Support and community](https://pypi.org/project/apify/#user-content-support-and-community)
- [Contributing](https://pypi.org/project/apify/#user-content-contributing)
- [License](https://pypi.org/project/apify/#user-content-license)

## Installation

The Apify SDK for Python requires **Python 3.11 or higher**. It is published on [PyPI](https://pypi.org/project/apify/) as the `apify` package and can be installed with [pip](https://pip.pypa.io/):

```
pip install apify
```

or with [uv](https://docs.astral.sh/uv/):

```
uv add apify
```

To use the Scrapy integration, install the `scrapy` extra:

```
pip install 'apify[scrapy]'
```

## Quick start

An Actor is a Python program that runs inside the `async with Actor:` context. The context initializes the Actor when it starts and tears it down when it finishes. Here's a minimal Actor that reads its input and stores a result:

```
from apify import Actor

async def main() -> None:
    async with Actor:
        actor_input = await Actor.get_input()
        Actor.log.info('Actor input: %s', actor_input)
        await Actor.set_value('OUTPUT', 'Hello, world!')
```

The quickest way to scaffold a full Actor project, with the `.actor` configuration, input schema, and Dockerfile already in place, is the [Apify CLI](https://docs.apify.com/cli):

1. Install the CLI:


```
npm install -g apify-cli
```

2. Create a new Actor from the Python "getting started" template:


```
apify create my-actor --template python-start
```

3. Run it locally:


```
cd my-actor
apify run
```


To create, run, and deploy your first Actor step by step, see the [Quick start guide](https://docs.apify.com/sdk/python/docs/quick-start).

## What are Actors?

Actors are serverless programs that can do almost anything. From simple scripts and web scrapers to complex automation workflows, AI agents, or even always-on services that expose HTTP endpoints.

They can run either locally or on the Apify platform, where you can scale their execution, monitor runs, schedule tasks, integrate them with other services, or even publish and monetize them. If you're new to Apify, learn more about the platform in the [Apify documentation](https://docs.apify.com/platform/about).

For more context, read the [Actor whitepaper](https://whitepaper.actor/).

## Features

- Run the full Actor lifecycle inside `async with Actor:`, covering init, exit, failures, status messages, and reboots ( [Actor lifecycle](https://docs.apify.com/sdk/python/docs/concepts/actor-lifecycle)).
- Read Actor input validated against your input schema with `Actor.get_input()` ( [Actor input](https://docs.apify.com/sdk/python/docs/concepts/actor-input)).
- Read and write datasets, key-value stores, and request queues, locally or on the platform ( [Working with storages](https://docs.apify.com/sdk/python/docs/concepts/storages)).
- React to platform events such as system info, migration, and abort ( [Actor events](https://docs.apify.com/sdk/python/docs/concepts/actor-events)).
- Route requests through Apify Proxy with group selection, country targeting, and rotation ( [Proxy management](https://docs.apify.com/sdk/python/docs/concepts/proxy-management)).
- Start, call, abort, and metamorph other Actors and tasks, and attach webhooks to run events ( [Interacting with other Actors](https://docs.apify.com/sdk/python/docs/concepts/interacting-with-other-actors), [Webhooks](https://docs.apify.com/sdk/python/docs/concepts/webhooks)).
- Monetize your Actor with pay-per-event charging ( [Pay-per-event](https://docs.apify.com/sdk/python/docs/concepts/pay-per-event)).
- Reach the full [Apify API](https://docs.apify.com/api/v2) through a preconfigured `ApifyClient` ( [Accessing the Apify API](https://docs.apify.com/sdk/python/docs/concepts/access-apify-api)).

## What you can build

Almost any Python project can become an Actor, including projects for:

- **Web scraping and crawling** — The SDK is fully compatible with [Crawlee](https://crawlee.dev/python), which makes Apify a natural place to deploy and scale your crawlers (see the [Crawlee guide](https://docs.apify.com/sdk/python/docs/guides/crawlee)). It also works with other popular scraping libraries, such as [Scrapy](https://docs.apify.com/sdk/python/docs/guides/scrapy), [Scrapling](https://docs.apify.com/sdk/python/docs/guides/scrapling), or [Crawl4AI](https://docs.apify.com/sdk/python/docs/guides/crawl4ai).
- **Browser automation** — Drive a real browser with [Playwright](https://docs.apify.com/sdk/python/docs/guides/playwright) or [Selenium](https://docs.apify.com/sdk/python/docs/guides/selenium), or with higher-level tools such as [Browser Use](https://docs.apify.com/sdk/python/docs/guides/browser-use).
- **Web servers and APIs** — Run a [web server](https://docs.apify.com/sdk/python/docs/guides/running-webserver) inside an Actor to serve HTTP requests, for example to expose your scraper as a live API.
- **AI agents** — Host agents built with your framework of choice (see the [AI agents guide](https://docs.apify.com/sdk/python/docs/guides/ai-agents)). Ready-made Actor templates cover [LangGraph](https://apify.com/templates/python-langgraph), [CrewAI](https://apify.com/templates/python-crewai), [PydanticAI](https://apify.com/templates/python-pydanticai), [LlamaIndex](https://apify.com/templates/python-llamaindex-agent), and [Smolagents](https://apify.com/templates/python-smolagents).
- **MCP servers** — Deploy a Python MCP server as an Actor and make its tools available to any MCP client (see the [MCP servers guide](https://docs.apify.com/sdk/python/docs/guides/mcp-servers)). Ready-made Actor templates cover the [MCP server](https://apify.com/templates/python-mcp-empty) and [MCP proxy](https://apify.com/templates/python-mcp-proxy).

Whatever you build, the Apify SDK doesn't lock you into a particular framework. Bring the libraries you already use, and let Apify run your project in the cloud.

## Usage examples

The examples below show two common setups, but the same `async with Actor:` pattern works with any stack. For more, see the [guides](https://docs.apify.com/sdk/python/docs/guides/beautifulsoup-httpx).

### HTTPX with BeautifulSoup

Scrape pages with [HTTPX](https://www.python-httpx.org/) and [BeautifulSoup](https://pypi.org/project/beautifulsoup4/), using the Actor's request queue to track URLs:

```
from bs4 import BeautifulSoup
from httpx import AsyncClient

from apify import Actor

async def main() -> None:
    async with Actor:
        actor_input = await Actor.get_input() or {}
        start_urls = actor_input.get('start_urls', [{'url': 'https://apify.com'}])

        # Enqueue the start URLs into the default request queue.
        request_queue = await Actor.open_request_queue()
        for start_url in start_urls:
            await request_queue.add_request(start_url['url'])

        # Process the queue until it's empty.
        while request := await request_queue.fetch_next_request():
            Actor.log.info(f'Scraping {request.url} ...')
            async with AsyncClient() as client:
                response = await client.get(request.url)
            soup = BeautifulSoup(response.content, 'html.parser')

            # Push the extracted data to the default dataset.
            await Actor.push_data(
                {
                    'url': request.url,
                    'title': soup.title.string if soup.title else None,
                }
            )

            # Mark the request as handled so it is not processed again.
            await request_queue.mark_request_as_handled(request)
```

### Crawlee with Playwright

Scrape pages with [Crawlee](https://crawlee.dev/python)'s `PlaywrightCrawler`, which handles queueing, concurrency, and the browser for you:

```
from crawlee.crawlers import PlaywrightCrawler, PlaywrightCrawlingContext

from apify import Actor

async def main() -> None:
    async with Actor:
        actor_input = await Actor.get_input() or {}
        start_urls = [url['url'] for url in actor_input.get('start_urls', [{'url': 'https://apify.com'}])]

        crawler = PlaywrightCrawler(max_requests_per_crawl=50, headless=True)

        @crawler.router.default_handler
        async def handler(context: PlaywrightCrawlingContext) -> None:
            Actor.log.info(f'Scraping {context.request.url} ...')
            await context.push_data(
                {
                    'url': context.request.url,
                    'title': await context.page.title(),
                }
            )
            # Follow links found on the page.
            await context.enqueue_links()

        await crawler.run(start_urls)
```

## Documentation

The full SDK documentation lives at **[docs.apify.com/sdk/python](https://docs.apify.com/sdk/python)**. For the Apify platform itself, see the [Apify documentation](https://docs.apify.com/).

| Section | What you'll find |
| --- | --- |
| [Overview](https://docs.apify.com/sdk/python/docs/overview) | What the SDK is, what Actors are, and how the pieces fit together. |
| [Quick start](https://docs.apify.com/sdk/python/docs/quick-start) | Create, run, and deploy your first Python Actor. |
| [Concepts](https://docs.apify.com/sdk/python/docs/concepts/actor-lifecycle) | Actor lifecycle, input, storages, events, proxy management, interacting with other Actors, webhooks, accessing the Apify API, logging, configuration, and pay-per-event. |
| [Guides](https://docs.apify.com/sdk/python/docs/guides/beautifulsoup-httpx) | Integrations with BeautifulSoup, Parsel, Playwright, Selenium, Crawlee, Scrapy, Scrapling, Crawl4AI, and Browser Use, plus using uv, validating input with Pydantic, running a web server, building MCP servers, and hosting AI agents. |
| [Upgrading](https://docs.apify.com/sdk/python/docs/upgrading/upgrading-to-v4) | Migrating between major versions. |
| [API reference](https://docs.apify.com/sdk/python/reference) | Generated reference for every class and method. |
| [Changelog](https://docs.apify.com/sdk/python/docs/changelog) | Release history and breaking changes. |

## Related projects

- **[Apify API client for Python](https://docs.apify.com/api/client/python)** — talk to the Apify API directly from Python (bundled with this SDK).
- **[Crawlee for Python](https://crawlee.dev/python)** — web scraping and browser automation framework; fully compatible with this SDK.
- **[Apify SDK for JavaScript / TypeScript](https://docs.apify.com/sdk/js)** — the equivalent SDK for Node.js.
- **[Apify API client for JavaScript / TypeScript](https://docs.apify.com/api/client/js)** — the equivalent API client for Node.js.
- **[Crawlee for JavaScript / TypeScript](https://crawlee.dev/)** — the original Node.js implementation of Crawlee.
- **[Apify CLI](https://docs.apify.com/cli)** — command-line tool for creating, running, and deploying Actors locally and on the platform.

## Support and community

- **Discord** — chat with the team and other users on the [Apify Discord server](https://discord.gg/jyEM2PRvMU).
- **GitHub issues** — report a bug or request a feature in the [issue tracker](https://github.com/apify/apify-sdk-python/issues).

## Contributing

Bug reports, fixes, and improvements are welcome! See [CONTRIBUTING.md](https://pypi.org/project/apify/CONTRIBUTING.md) for the development setup, coding standards, testing, and release process. The project uses [uv](https://docs.astral.sh/uv/) for project management and [Poe the Poet](https://poethepoet.natn.io/) as a task runner; the typical loop is:

```
uv run poe install-dev   # install dev dependencies and git hooks
uv run poe check-code    # lint, type-check, and unit tests
```

## License

Released under the [Apache License 2.0](https://pypi.org/project/apify/LICENSE).

## Project links

Data verified by PyPI on Sep 3, 2026

Data provided by the project maintainers, verified at the time the release was uploaded to PyPI.

- [Issue Tracker](https://github.com/apify/apify-sdk-python/issues)
- [Source Code](https://github.com/apify/apify-sdk-python)

- [Apify Homepage](https://apify.com/)
- [Changelog](https://docs.apify.com/sdk/python/docs/changelog)
- [Discord](https://discord.com/invite/jyEM2PRvMU)
- [Documentation](https://docs.apify.com/sdk/python/docs/overview)
- [Homepage](https://docs.apify.com/sdk/python/)
- [Release Notes](https://docs.apify.com/sdk/python/docs/upgrading/upgrading-to-v4)

## Key dates

PyPI data

Data sourced directly from PyPI's database.

- **Released:** Sep 3, 2026

Latest release

## Owner

PyPI data

Data sourced directly from PyPI's database.

- [Apify](https://pypi.org/org/apify/)

## 2 maintainers

PyPI data

Data sourced directly from PyPI's database.

[![Avatar for frantisek.nesveda from gravatar.com](https://pypi-camo.freetls.fastly.net/23392f675ef88d49f1cced89dd35b9c125ff84ab/68747470733a2f2f7365637572652e67726176617461722e636f6d2f6176617461722f37613162376432306361396435653365343263316536343663316130333939623f73697a653d3335)frantisek.nesveda](https://pypi.org/user/frantisek.nesveda/) [![Avatar for jancurn from gravatar.com](https://pypi-camo.freetls.fastly.net/4d4e811c61e746d148c8489288b8a692d3d5ef6f/68747470733a2f2f7365637572652e67726176617461722e636f6d2f6176617461722f34363364393166626264646435643237313963623066383161396264383134383f73697a653d3335)jancurn](https://pypi.org/user/jancurn/)

## Credits

**Author:** [Apify Technologies s.r.o.](mailto:support@apify.com)

## GitHub Statistics

Data verified by PyPI on Sep 3, 2026

The GitHub source repository was provided by the project maintainers and verified by PyPI at the time of upload. Stars, forks, and open issues/PRs are derived from that repository and have not been independently verified.

- [Repository](https://github.com/apify/apify-sdk-python)
- Stars:

- Forks:

- Open issues:

- Open PRs:


## License expression [About license expressions](https://spdx.github.io/spdx-spec/v3.0.1/annexes/spdx-license-expressions/)

Apache-2.0


[View SPDX License List](https://spdx.org/licenses/)

## Requires

**Python** >=3.11

## Provides Extra

`scrapy`

## Tags

`apify``sdk``automation``chrome``crawlee``crawler``headless``scraper``scraping`

## Classifiers

- Development Status
  - [5 - Production/Stable](https://pypi.org/search/?c=Development+Status+%3A%3A+5+-+Production%2FStable)
- Environment
  - [Console](https://pypi.org/search/?c=Environment+%3A%3A+Console)
- Intended Audience
  - [Developers](https://pypi.org/search/?c=Intended+Audience+%3A%3A+Developers)
- Operating System
  - [OS Independent](https://pypi.org/search/?c=Operating+System+%3A%3A+OS+Independent)
- Programming Language
  - [Python :: 3.11](https://pypi.org/search/?c=Programming+Language+%3A%3A+Python+%3A%3A+3.11)
  - [Python :: 3.12](https://pypi.org/search/?c=Programming+Language+%3A%3A+Python+%3A%3A+3.12)
  - [Python :: 3.13](https://pypi.org/search/?c=Programming+Language+%3A%3A+Python+%3A%3A+3.13)
  - [Python :: 3.14](https://pypi.org/search/?c=Programming+Language+%3A%3A+Python+%3A%3A+3.14)
- Topic
  - [Software Development :: Libraries](https://pypi.org/search/?c=Topic+%3A%3A+Software+Development+%3A%3A+Libraries)
- Typing
  - [Typed](https://pypi.org/search/?c=Typing+%3A%3A+Typed)

[Report project as malware](https://pypi.org/project/apify/submit-malware-report/)

## Metadata

## Project links

Data verified by PyPI on Sep 3, 2026

Data provided by the project maintainers, verified at the time the release was uploaded to PyPI.

- [Issue Tracker](https://github.com/apify/apify-sdk-python/issues)
- [Source Code](https://github.com/apify/apify-sdk-python)

- [Apify Homepage](https://apify.com/)
- [Changelog](https://docs.apify.com/sdk/python/docs/changelog)
- [Discord](https://discord.com/invite/jyEM2PRvMU)
- [Documentation](https://docs.apify.com/sdk/python/docs/overview)
- [Homepage](https://docs.apify.com/sdk/python/)
- [Release Notes](https://docs.apify.com/sdk/python/docs/upgrading/upgrading-to-v4)

## Key dates

PyPI data

Data sourced directly from PyPI's database.

- **Released:** Sep 3, 2026

Latest release

## Owner

PyPI data

Data sourced directly from PyPI's database.

- [Apify](https://pypi.org/org/apify/)

## 2 maintainers

PyPI data

Data sourced directly from PyPI's database.

[![Avatar for frantisek.nesveda from gravatar.com](https://pypi-camo.freetls.fastly.net/23392f675ef88d49f1cced89dd35b9c125ff84ab/68747470733a2f2f7365637572652e67726176617461722e636f6d2f6176617461722f37613162376432306361396435653365343263316536343663316130333939623f73697a653d3335)frantisek.nesveda](https://pypi.org/user/frantisek.nesveda/) [![Avatar for jancurn from gravatar.com](https://pypi-camo.freetls.fastly.net/4d4e811c61e746d148c8489288b8a692d3d5ef6f/68747470733a2f2f7365637572652e67726176617461722e636f6d2f6176617461722f34363364393166626264646435643237313963623066383161396264383134383f73697a653d3335)jancurn](https://pypi.org/user/jancurn/)

## Credits

**Author:** [Apify Technologies s.r.o.](mailto:support@apify.com)

## GitHub Statistics

Data verified by PyPI on Sep 3, 2026

The GitHub source repository was provided by the project maintainers and verified by PyPI at the time of upload. Stars, forks, and open issues/PRs are derived from that repository and have not been independently verified.

- [Repository](https://github.com/apify/apify-sdk-python)
- Stars:

- Forks:

- Open issues:

- Open PRs:


## License expression [About license expressions](https://spdx.github.io/spdx-spec/v3.0.1/annexes/spdx-license-expressions/)

Apache-2.0


[View SPDX License List](https://spdx.org/licenses/)

## Requires

**Python** >=3.11

## Provides Extra

`scrapy`

## Tags

`apify``sdk``automation``chrome``crawlee``crawler``headless``scraper``scraping`

## Classifiers

- Development Status
  - [5 - Production/Stable](https://pypi.org/search/?c=Development+Status+%3A%3A+5+-+Production%2FStable)
- Environment
  - [Console](https://pypi.org/search/?c=Environment+%3A%3A+Console)
- Intended Audience
  - [Developers](https://pypi.org/search/?c=Intended+Audience+%3A%3A+Developers)
- Operating System
  - [OS Independent](https://pypi.org/search/?c=Operating+System+%3A%3A+OS+Independent)
- Programming Language
  - [Python :: 3.11](https://pypi.org/search/?c=Programming+Language+%3A%3A+Python+%3A%3A+3.11)
  - [Python :: 3.12](https://pypi.org/search/?c=Programming+Language+%3A%3A+Python+%3A%3A+3.12)
  - [Python :: 3.13](https://pypi.org/search/?c=Programming+Language+%3A%3A+Python+%3A%3A+3.13)
  - [Python :: 3.14](https://pypi.org/search/?c=Programming+Language+%3A%3A+Python+%3A%3A+3.14)
- Topic
  - [Software Development :: Libraries](https://pypi.org/search/?c=Topic+%3A%3A+Software+Development+%3A%3A+Libraries)
- Typing
  - [Typed](https://pypi.org/search/?c=Typing+%3A%3A+Typed)

[Report project as malware](https://pypi.org/project/apify/submit-malware-report/)

## Release files for apify 4.0.2

For a detailed explanation of source distributions (sdists) and built distributions (wheels), please see the [package formats documentation](https://packaging.python.org/en/latest/discussions/package-formats/#package-formats "External link").

### Source distribution (sdist)

| File | Size | Uploaded |  |
| --- | --- | --- | --- |
| [apify-4.0.2.tar.gz](https://files.pythonhosted.org/packages/87/11/7ce58b8739924bfde2fbcffc8315bfe3ec65f8234f7002ff872cb8ea2ab7/apify-4.0.2.tar.gz) | 127.5 kB | Sep 3, 2026 | [Details](https://pypi.org/project/apify/#apify-4.0.2.tar.gz) |

Source distribution for apify 4.0.2

* * *

### Built distribution (wheel)

| File | Interpreter | ABI | Platform | [Reset](https://pypi.org/project/apify/#files) |
| --- | --- | --- | --- | --- |
| [apify-4.0.2-py3-none-any.whl](https://files.pythonhosted.org/packages/52/b5/ba013e6b4082a2e5f198e02f1883d6130d4d70346e09e21a237e5b7cfafb/apify-4.0.2-py3-none-any.whl)132.2 kBSep 3, 2026 | Python 3 | none | any | [Details](https://pypi.org/project/apify/#apify-4.0.2-py3-none-any.whl) |

Table of built distributions (wheels) for apify 4.0.2

* * *

**Total release size:** 259.7 kB


## [Release files](https://pypi.org/project/apify/\#files)  / apify-4.0.2.tar.gz

| Download URL | [apify-4.0.2.tar.gz](https://files.pythonhosted.org/packages/87/11/7ce58b8739924bfde2fbcffc8315bfe3ec65f8234f7002ff872cb8ea2ab7/apify-4.0.2.tar.gz) |
| Size | 127.5 kB |
| Tags | Source |
| SHA-256 checksum <br>[How to use checksums](https://pip.pypa.io/en/stable/topics/secure-installs/#hash-checking-mode "External link") | `<br>            bb9d2d8453be552625fe79949b4a86db79c93e3322b66f4572c7f7d3412043c5<br>` |
| BLAKE2b-256 checksum <br>[How to use checksums](https://pip.pypa.io/en/stable/topics/secure-installs/#hash-checking-mode "External link") | `<br>            87117ce58b8739924bfde2fbcffc8315bfe3ec65f8234f7002ff872cb8ea2ab7<br>` |
| Upload date | Sep 3, 2026 |
| Uploaded using Trusted Publishing? <br>[What is trusted publishing?](https://docs.pypi.org/trusted-publishers/) | Yes |
| Uploaded via | `twine/7.0.0 CPython/3.13.14` |

### Provenance

**Provenance** describes where a file came from. On PyPI, provenance is shared via **attestations**, which provide a verifiable record of the build or publishing details. [View details, limitations and caveats.](https://docs.pypi.org/attestations/)

![](https://pypi.org/static/images/github.683a0246.svg)![](https://pypi.org/static/images/pypi-attestation-cube.1cfdb012.svg)

#### [PyPI Publish](https://docs.pypi.org/attestations/publish/v1) Attestation

PyPI verified that this artifact, at this checksum, originated from the publisher listed below.

**Signed by GitHub Actions, verified by PyPI on Sep 3, 2026.**

[Transparency log](https://search.sigstore.dev/?logIndex=2698504561 "Sigstore transparency entry")

##### Identity

Publishing platform
GitHub Actions

Publishing repository [github.com/apify/apify-sdk-python](https://github.com/apify/apify-sdk-python)
Publishing commit [github.com/apify/apify-sdk-python/tree/d778ba39a97fce6281140a854abba338c089fb6f](https://github.com/apify/apify-sdk-python/tree/d778ba39a97fce6281140a854abba338c089fb6f)

##### Workflow

Publishing configuration [github.com/apify/apify-sdk-python/blob/d778ba39a97fce6281140a854abba338c089fb6f/.github/workflows/manual\_release\_stable.yaml](https://github.com/apify/apify-sdk-python/blob/d778ba39a97fce6281140a854abba338c089fb6f/.github/workflows/manual_release_stable.yaml)
Publishing logs [github.com/apify/apify-sdk-python/actions/runs/33748427629/attempts/1](https://github.com/apify/apify-sdk-python/actions/runs/33748427629/attempts/1)

##### Artifact

Subject`apify-4.0.2.tar.gz`SHA-256 checksum`
              bb9d2d8453be552625fe79949b4a86db79c93e3322b66f4572c7f7d3412043c5

` [Verifying attestations](https://docs.pypi.org/attestations/consuming-attestations/)

## [Release files](https://pypi.org/project/apify/\#files)  / apify-4.0.2-py3-none-any.whl

| Download URL | [apify-4.0.2-py3-none-any.whl](https://files.pythonhosted.org/packages/52/b5/ba013e6b4082a2e5f198e02f1883d6130d4d70346e09e21a237e5b7cfafb/apify-4.0.2-py3-none-any.whl) |
| Size | 132.2 kB |
| Tags | Python 3 |
| SHA-256 checksum <br>[How to use checksums](https://pip.pypa.io/en/stable/topics/secure-installs/#hash-checking-mode "External link") | `<br>            f2c951e310c3a8420480255bdabc132442000b63f7a4a21706bb27ce8b3e1b54<br>` |
| BLAKE2b-256 checksum <br>[How to use checksums](https://pip.pypa.io/en/stable/topics/secure-installs/#hash-checking-mode "External link") | `<br>            52b5ba013e6b4082a2e5f198e02f1883d6130d4d70346e09e21a237e5b7cfafb<br>` |
| Upload date | Sep 3, 2026 |
| Uploaded using Trusted Publishing? <br>[What is trusted publishing?](https://docs.pypi.org/trusted-publishers/) | Yes |
| Uploaded via | `twine/7.0.0 CPython/3.13.14` |

### Provenance

**Provenance** describes where a file came from. On PyPI, provenance is shared via **attestations**, which provide a verifiable record of the build or publishing details. [View details, limitations and caveats.](https://docs.pypi.org/attestations/)

![](https://pypi.org/static/images/github.683a0246.svg)![](https://pypi.org/static/images/pypi-attestation-cube.1cfdb012.svg)

#### [PyPI Publish](https://docs.pypi.org/attestations/publish/v1) Attestation

PyPI verified that this artifact, at this checksum, originated from the publisher listed below.

**Signed by GitHub Actions, verified by PyPI on Sep 3, 2026.**

[Transparency log](https://search.sigstore.dev/?logIndex=2698504611 "Sigstore transparency entry")

##### Identity

Publishing platform
GitHub Actions

Publishing repository [github.com/apify/apify-sdk-python](https://github.com/apify/apify-sdk-python)
Publishing commit [github.com/apify/apify-sdk-python/tree/d778ba39a97fce6281140a854abba338c089fb6f](https://github.com/apify/apify-sdk-python/tree/d778ba39a97fce6281140a854abba338c089fb6f)

##### Workflow

Publishing configuration [github.com/apify/apify-sdk-python/blob/d778ba39a97fce6281140a854abba338c089fb6f/.github/workflows/manual\_release\_stable.yaml](https://github.com/apify/apify-sdk-python/blob/d778ba39a97fce6281140a854abba338c089fb6f/.github/workflows/manual_release_stable.yaml)
Publishing logs [github.com/apify/apify-sdk-python/actions/runs/33748427629/attempts/1](https://github.com/apify/apify-sdk-python/actions/runs/33748427629/attempts/1)

##### Artifact

Subject`apify-4.0.2-py3-none-any.whl`SHA-256 checksum`
              f2c951e310c3a8420480255bdabc132442000b63f7a4a21706bb27ce8b3e1b54

` [Verifying attestations](https://docs.pypi.org/attestations/consuming-attestations/)

## Release history[Release notifications](https://pypi.org/help/\#project-release-notifications) \|  [RSS feed](https://pypi.org/rss/project/apify/releases.xml)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[4.0.3b3](https://pypi.org/project/apify/4.0.3b3/)

Sep 29, 2026 [2 release files](https://pypi.org/project/apify/4.0.3b3/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[4.0.3b2](https://pypi.org/project/apify/4.0.3b2/)

Sep 25, 2026 [2 release files](https://pypi.org/project/apify/4.0.3b2/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[4.0.3b1](https://pypi.org/project/apify/4.0.3b1/)

Sep 22, 2026 [2 release files](https://pypi.org/project/apify/4.0.3b1/#files)

This release

![](https://pypi.org/static/images/blue-cube.572a5bfb.svg)

[4.0.2](https://pypi.org/project/apify/4.0.2/) This release

Sep 3, 2026 [2 release files](https://pypi.org/project/apify/4.0.2/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[4.0.2b5](https://pypi.org/project/apify/4.0.2b5/)

Aug 31, 2026 [2 release files](https://pypi.org/project/apify/4.0.2b5/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[4.0.2b4](https://pypi.org/project/apify/4.0.2b4/)

Aug 25, 2026 [2 release files](https://pypi.org/project/apify/4.0.2b4/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[4.0.2b3](https://pypi.org/project/apify/4.0.2b3/)

Aug 25, 2026 [2 release files](https://pypi.org/project/apify/4.0.2b3/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[4.0.2b2](https://pypi.org/project/apify/4.0.2b2/)

Aug 20, 2026 [2 release files](https://pypi.org/project/apify/4.0.2b2/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[4.0.2b1](https://pypi.org/project/apify/4.0.2b1/)

Aug 19, 2026 [2 release files](https://pypi.org/project/apify/4.0.2b1/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[4.0.1](https://pypi.org/project/apify/4.0.1/)

Aug 7, 2026 [2 release files](https://pypi.org/project/apify/4.0.1/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[4.0.1b5](https://pypi.org/project/apify/4.0.1b5/)

Aug 7, 2026 [2 release files](https://pypi.org/project/apify/4.0.1b5/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[4.0.1b4](https://pypi.org/project/apify/4.0.1b4/)

Aug 6, 2026 [2 release files](https://pypi.org/project/apify/4.0.1b4/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[4.0.1b3](https://pypi.org/project/apify/4.0.1b3/)

Aug 5, 2026 [2 release files](https://pypi.org/project/apify/4.0.1b3/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[4.0.1b2](https://pypi.org/project/apify/4.0.1b2/)

Aug 5, 2026 [2 release files](https://pypi.org/project/apify/4.0.1b2/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[4.0.1b1](https://pypi.org/project/apify/4.0.1b1/)

Aug 4, 2026 [2 release files](https://pypi.org/project/apify/4.0.1b1/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[4.0.0](https://pypi.org/project/apify/4.0.0/)

Jul 20, 2026 [2 release files](https://pypi.org/project/apify/4.0.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.4.2b36](https://pypi.org/project/apify/3.4.2b36/)

Jul 20, 2026 [2 release files](https://pypi.org/project/apify/3.4.2b36/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.4.2b35](https://pypi.org/project/apify/3.4.2b35/)

Jul 17, 2026 [2 release files](https://pypi.org/project/apify/3.4.2b35/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.4.2b34](https://pypi.org/project/apify/3.4.2b34/)

Jul 16, 2026 [2 release files](https://pypi.org/project/apify/3.4.2b34/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.4.2b33](https://pypi.org/project/apify/3.4.2b33/)

Jul 16, 2026 [2 release files](https://pypi.org/project/apify/3.4.2b33/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.4.2b32](https://pypi.org/project/apify/3.4.2b32/)

Jul 15, 2026 [2 release files](https://pypi.org/project/apify/3.4.2b32/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.4.2b31](https://pypi.org/project/apify/3.4.2b31/)

Jul 3, 2026 [2 release files](https://pypi.org/project/apify/3.4.2b31/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.4.2b30](https://pypi.org/project/apify/3.4.2b30/)

Jul 3, 2026 [2 release files](https://pypi.org/project/apify/3.4.2b30/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.4.2b29](https://pypi.org/project/apify/3.4.2b29/)

Jun 25, 2026 [2 release files](https://pypi.org/project/apify/3.4.2b29/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.4.2b28](https://pypi.org/project/apify/3.4.2b28/)

Jun 22, 2026 [2 release files](https://pypi.org/project/apify/3.4.2b28/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.4.2b27](https://pypi.org/project/apify/3.4.2b27/)

Jun 22, 2026 [2 release files](https://pypi.org/project/apify/3.4.2b27/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.4.2b26](https://pypi.org/project/apify/3.4.2b26/)

Jun 18, 2026 [2 release files](https://pypi.org/project/apify/3.4.2b26/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.4.2b25](https://pypi.org/project/apify/3.4.2b25/)

Jun 18, 2026 [2 release files](https://pypi.org/project/apify/3.4.2b25/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.4.2b24](https://pypi.org/project/apify/3.4.2b24/)

Jun 17, 2026 [2 release files](https://pypi.org/project/apify/3.4.2b24/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.4.2b23](https://pypi.org/project/apify/3.4.2b23/)

Jun 16, 2026 [2 release files](https://pypi.org/project/apify/3.4.2b23/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.4.2b22](https://pypi.org/project/apify/3.4.2b22/)

Jun 16, 2026 [2 release files](https://pypi.org/project/apify/3.4.2b22/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.4.2b21](https://pypi.org/project/apify/3.4.2b21/)

Jun 15, 2026 [2 release files](https://pypi.org/project/apify/3.4.2b21/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.4.2b20](https://pypi.org/project/apify/3.4.2b20/)

Jun 15, 2026 [2 release files](https://pypi.org/project/apify/3.4.2b20/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.4.2b19](https://pypi.org/project/apify/3.4.2b19/)

Jun 15, 2026 [2 release files](https://pypi.org/project/apify/3.4.2b19/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.4.2b18](https://pypi.org/project/apify/3.4.2b18/)

Jun 15, 2026 [2 release files](https://pypi.org/project/apify/3.4.2b18/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.4.2b17](https://pypi.org/project/apify/3.4.2b17/)

Jun 15, 2026 [2 release files](https://pypi.org/project/apify/3.4.2b17/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.4.2b16](https://pypi.org/project/apify/3.4.2b16/)

Jun 15, 2026 [2 release files](https://pypi.org/project/apify/3.4.2b16/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.4.2b15](https://pypi.org/project/apify/3.4.2b15/)

Jun 15, 2026 [2 release files](https://pypi.org/project/apify/3.4.2b15/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.4.2b14](https://pypi.org/project/apify/3.4.2b14/)

Jun 12, 2026 [2 release files](https://pypi.org/project/apify/3.4.2b14/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.4.2b13](https://pypi.org/project/apify/3.4.2b13/)

Jun 12, 2026 [2 release files](https://pypi.org/project/apify/3.4.2b13/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.4.2b12](https://pypi.org/project/apify/3.4.2b12/)

Jun 12, 2026 [2 release files](https://pypi.org/project/apify/3.4.2b12/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.4.2b11](https://pypi.org/project/apify/3.4.2b11/)

Jun 12, 2026 [2 release files](https://pypi.org/project/apify/3.4.2b11/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.4.2b10](https://pypi.org/project/apify/3.4.2b10/)

Jun 12, 2026 [2 release files](https://pypi.org/project/apify/3.4.2b10/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.4.2b9](https://pypi.org/project/apify/3.4.2b9/)

Jun 12, 2026 [2 release files](https://pypi.org/project/apify/3.4.2b9/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.4.2b8](https://pypi.org/project/apify/3.4.2b8/)

Jun 12, 2026 [2 release files](https://pypi.org/project/apify/3.4.2b8/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.4.2b7](https://pypi.org/project/apify/3.4.2b7/)

Jun 11, 2026 [2 release files](https://pypi.org/project/apify/3.4.2b7/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.4.2b6](https://pypi.org/project/apify/3.4.2b6/)

Jun 10, 2026 [2 release files](https://pypi.org/project/apify/3.4.2b6/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.4.2b5](https://pypi.org/project/apify/3.4.2b5/)

Jun 9, 2026 [2 release files](https://pypi.org/project/apify/3.4.2b5/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.4.2b4](https://pypi.org/project/apify/3.4.2b4/)

Jun 9, 2026 [2 release files](https://pypi.org/project/apify/3.4.2b4/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.4.2b3](https://pypi.org/project/apify/3.4.2b3/)

Jun 5, 2026 [2 release files](https://pypi.org/project/apify/3.4.2b3/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.4.2b2](https://pypi.org/project/apify/3.4.2b2/)

Jun 2, 2026 [2 release files](https://pypi.org/project/apify/3.4.2b2/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.4.2b1](https://pypi.org/project/apify/3.4.2b1/)

May 29, 2026 [2 release files](https://pypi.org/project/apify/3.4.2b1/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[3.4.1](https://pypi.org/project/apify/3.4.1/)

May 29, 2026 [2 release files](https://pypi.org/project/apify/3.4.1/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.4.1b2](https://pypi.org/project/apify/3.4.1b2/)

May 26, 2026 [2 release files](https://pypi.org/project/apify/3.4.1b2/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.4.1b1](https://pypi.org/project/apify/3.4.1b1/)

May 25, 2026 [2 release files](https://pypi.org/project/apify/3.4.1b1/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[3.4.0](https://pypi.org/project/apify/3.4.0/)

May 5, 2026 [2 release files](https://pypi.org/project/apify/3.4.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.3.4b1](https://pypi.org/project/apify/3.3.4b1/)

May 4, 2026 [2 release files](https://pypi.org/project/apify/3.3.4b1/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[3.3.3](https://pypi.org/project/apify/3.3.3/)

Apr 21, 2026 [2 release files](https://pypi.org/project/apify/3.3.3/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.3.3b6](https://pypi.org/project/apify/3.3.3b6/)

Apr 21, 2026 [2 release files](https://pypi.org/project/apify/3.3.3b6/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.3.3b5](https://pypi.org/project/apify/3.3.3b5/)

Apr 21, 2026 [2 release files](https://pypi.org/project/apify/3.3.3b5/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.3.3b4](https://pypi.org/project/apify/3.3.3b4/)

Apr 20, 2026 [2 release files](https://pypi.org/project/apify/3.3.3b4/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.3.3b3](https://pypi.org/project/apify/3.3.3b3/)

Apr 20, 2026 [2 release files](https://pypi.org/project/apify/3.3.3b3/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.3.3b2](https://pypi.org/project/apify/3.3.3b2/)

Apr 20, 2026 [2 release files](https://pypi.org/project/apify/3.3.3b2/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.3.3b1](https://pypi.org/project/apify/3.3.3b1/)

Apr 20, 2026 [2 release files](https://pypi.org/project/apify/3.3.3b1/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[3.3.2](https://pypi.org/project/apify/3.3.2/)

Mar 27, 2026 [2 release files](https://pypi.org/project/apify/3.3.2/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.3.2b5](https://pypi.org/project/apify/3.3.2b5/)

Mar 27, 2026 [2 release files](https://pypi.org/project/apify/3.3.2b5/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.3.2b4](https://pypi.org/project/apify/3.3.2b4/)

Mar 27, 2026 [2 release files](https://pypi.org/project/apify/3.3.2b4/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.3.2b3](https://pypi.org/project/apify/3.3.2b3/)

Mar 26, 2026 [2 release files](https://pypi.org/project/apify/3.3.2b3/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.3.2b2](https://pypi.org/project/apify/3.3.2b2/)

Mar 26, 2026 [2 release files](https://pypi.org/project/apify/3.3.2b2/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.3.2b1](https://pypi.org/project/apify/3.3.2b1/)

Mar 16, 2026 [2 release files](https://pypi.org/project/apify/3.3.2b1/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[3.3.1](https://pypi.org/project/apify/3.3.1/)

Mar 11, 2026 [2 release files](https://pypi.org/project/apify/3.3.1/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.3.1b6](https://pypi.org/project/apify/3.3.1b6/)

Mar 11, 2026 [2 release files](https://pypi.org/project/apify/3.3.1b6/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.3.1b5](https://pypi.org/project/apify/3.3.1b5/)

Mar 3, 2026 [2 release files](https://pypi.org/project/apify/3.3.1b5/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.3.1b4](https://pypi.org/project/apify/3.3.1b4/)

Mar 2, 2026 [2 release files](https://pypi.org/project/apify/3.3.1b4/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.3.1b3](https://pypi.org/project/apify/3.3.1b3/)

Mar 2, 2026 [2 release files](https://pypi.org/project/apify/3.3.1b3/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.3.1b2](https://pypi.org/project/apify/3.3.1b2/)

Mar 2, 2026 [2 release files](https://pypi.org/project/apify/3.3.1b2/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.3.1b1](https://pypi.org/project/apify/3.3.1b1/)

Mar 2, 2026 [2 release files](https://pypi.org/project/apify/3.3.1b1/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[3.3.0](https://pypi.org/project/apify/3.3.0/)

Feb 25, 2026 [2 release files](https://pypi.org/project/apify/3.3.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.2.2b6](https://pypi.org/project/apify/3.2.2b6/)

Feb 25, 2026 [2 release files](https://pypi.org/project/apify/3.2.2b6/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.2.2b5](https://pypi.org/project/apify/3.2.2b5/)

Feb 25, 2026 [2 release files](https://pypi.org/project/apify/3.2.2b5/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.2.2b4](https://pypi.org/project/apify/3.2.2b4/)

Feb 23, 2026 [2 release files](https://pypi.org/project/apify/3.2.2b4/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.2.2b3](https://pypi.org/project/apify/3.2.2b3/)

Feb 20, 2026 [2 release files](https://pypi.org/project/apify/3.2.2b3/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.2.2b2](https://pypi.org/project/apify/3.2.2b2/)

Feb 19, 2026 [2 release files](https://pypi.org/project/apify/3.2.2b2/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.2.2b1](https://pypi.org/project/apify/3.2.2b1/)

Feb 18, 2026 [2 release files](https://pypi.org/project/apify/3.2.2b1/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[3.2.1](https://pypi.org/project/apify/3.2.1/)

Feb 17, 2026 [2 release files](https://pypi.org/project/apify/3.2.1/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.2.1b5](https://pypi.org/project/apify/3.2.1b5/)

Feb 17, 2026 [2 release files](https://pypi.org/project/apify/3.2.1b5/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.2.1b4](https://pypi.org/project/apify/3.2.1b4/)

Feb 17, 2026 [2 release files](https://pypi.org/project/apify/3.2.1b4/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.2.1b3](https://pypi.org/project/apify/3.2.1b3/)

Feb 17, 2026 [2 release files](https://pypi.org/project/apify/3.2.1b3/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.2.1b2](https://pypi.org/project/apify/3.2.1b2/)

Feb 16, 2026 [2 release files](https://pypi.org/project/apify/3.2.1b2/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.2.1b1](https://pypi.org/project/apify/3.2.1b1/)

Feb 15, 2026 [2 release files](https://pypi.org/project/apify/3.2.1b1/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[3.2.0](https://pypi.org/project/apify/3.2.0/)

Feb 11, 2026 [2 release files](https://pypi.org/project/apify/3.2.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.1.1b31](https://pypi.org/project/apify/3.1.1b31/)

Feb 11, 2026 [2 release files](https://pypi.org/project/apify/3.1.1b31/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.1.1b30](https://pypi.org/project/apify/3.1.1b30/)

Feb 11, 2026 [2 release files](https://pypi.org/project/apify/3.1.1b30/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.1.1b29](https://pypi.org/project/apify/3.1.1b29/)

Feb 11, 2026 [2 release files](https://pypi.org/project/apify/3.1.1b29/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.1.1b28](https://pypi.org/project/apify/3.1.1b28/)

Feb 11, 2026 [2 release files](https://pypi.org/project/apify/3.1.1b28/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.1.1b27](https://pypi.org/project/apify/3.1.1b27/)

Feb 9, 2026 [2 release files](https://pypi.org/project/apify/3.1.1b27/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.1.1b26](https://pypi.org/project/apify/3.1.1b26/)

Feb 5, 2026 [2 release files](https://pypi.org/project/apify/3.1.1b26/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.1.1b25](https://pypi.org/project/apify/3.1.1b25/)

Feb 3, 2026 [2 release files](https://pypi.org/project/apify/3.1.1b25/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.1.1b24](https://pypi.org/project/apify/3.1.1b24/)

Jan 27, 2026 [2 release files](https://pypi.org/project/apify/3.1.1b24/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.1.1b23](https://pypi.org/project/apify/3.1.1b23/)

Jan 27, 2026 [2 release files](https://pypi.org/project/apify/3.1.1b23/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.1.1b22](https://pypi.org/project/apify/3.1.1b22/)

Jan 26, 2026 [2 release files](https://pypi.org/project/apify/3.1.1b22/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.1.1b21](https://pypi.org/project/apify/3.1.1b21/)

Jan 23, 2026 [2 release files](https://pypi.org/project/apify/3.1.1b21/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.1.1b20](https://pypi.org/project/apify/3.1.1b20/)

Jan 22, 2026 [2 release files](https://pypi.org/project/apify/3.1.1b20/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.1.1b19](https://pypi.org/project/apify/3.1.1b19/)

Jan 21, 2026 [2 release files](https://pypi.org/project/apify/3.1.1b19/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.1.1b18](https://pypi.org/project/apify/3.1.1b18/)

Jan 21, 2026 [2 release files](https://pypi.org/project/apify/3.1.1b18/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.1.1b17](https://pypi.org/project/apify/3.1.1b17/)

Jan 20, 2026 [2 release files](https://pypi.org/project/apify/3.1.1b17/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.1.1b16](https://pypi.org/project/apify/3.1.1b16/)

Jan 19, 2026 [2 release files](https://pypi.org/project/apify/3.1.1b16/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.1.1b15](https://pypi.org/project/apify/3.1.1b15/)

Jan 16, 2026 [2 release files](https://pypi.org/project/apify/3.1.1b15/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.1.1b14](https://pypi.org/project/apify/3.1.1b14/)

Jan 12, 2026 [2 release files](https://pypi.org/project/apify/3.1.1b14/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.1.1b13](https://pypi.org/project/apify/3.1.1b13/)

Jan 8, 2026 [2 release files](https://pypi.org/project/apify/3.1.1b13/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.1.1b12](https://pypi.org/project/apify/3.1.1b12/)

Jan 8, 2026 [2 release files](https://pypi.org/project/apify/3.1.1b12/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.1.1b11](https://pypi.org/project/apify/3.1.1b11/)

Jan 5, 2026 [2 release files](https://pypi.org/project/apify/3.1.1b11/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.1.1b10](https://pypi.org/project/apify/3.1.1b10/)

Jan 2, 2026 [2 release files](https://pypi.org/project/apify/3.1.1b10/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.1.1b9](https://pypi.org/project/apify/3.1.1b9/)

Jan 2, 2026 [2 release files](https://pypi.org/project/apify/3.1.1b9/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.1.1b8](https://pypi.org/project/apify/3.1.1b8/)

Dec 31, 2025 [2 release files](https://pypi.org/project/apify/3.1.1b8/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.1.1b7](https://pypi.org/project/apify/3.1.1b7/)

Dec 30, 2025 [2 release files](https://pypi.org/project/apify/3.1.1b7/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.1.1b6](https://pypi.org/project/apify/3.1.1b6/)

Dec 26, 2025 [2 release files](https://pypi.org/project/apify/3.1.1b6/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.1.1b5](https://pypi.org/project/apify/3.1.1b5/)

Dec 18, 2025 [2 release files](https://pypi.org/project/apify/3.1.1b5/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.1.1b4](https://pypi.org/project/apify/3.1.1b4/)

Dec 17, 2025 [2 release files](https://pypi.org/project/apify/3.1.1b4/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.1.1b3](https://pypi.org/project/apify/3.1.1b3/)

Dec 12, 2025 [2 release files](https://pypi.org/project/apify/3.1.1b3/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.1.1b2](https://pypi.org/project/apify/3.1.1b2/)

Dec 9, 2025 [2 release files](https://pypi.org/project/apify/3.1.1b2/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.1.1b1](https://pypi.org/project/apify/3.1.1b1/)

Dec 9, 2025 [2 release files](https://pypi.org/project/apify/3.1.1b1/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[3.1.0](https://pypi.org/project/apify/3.1.0/)

Dec 8, 2025 [2 release files](https://pypi.org/project/apify/3.1.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.0.6b9](https://pypi.org/project/apify/3.0.6b9/)

Dec 8, 2025 [2 release files](https://pypi.org/project/apify/3.0.6b9/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.0.6b8](https://pypi.org/project/apify/3.0.6b8/)

Dec 1, 2025 [2 release files](https://pypi.org/project/apify/3.0.6b8/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.0.6b7](https://pypi.org/project/apify/3.0.6b7/)

Nov 28, 2025 [2 release files](https://pypi.org/project/apify/3.0.6b7/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.0.6b6](https://pypi.org/project/apify/3.0.6b6/)

Nov 28, 2025 [2 release files](https://pypi.org/project/apify/3.0.6b6/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.0.6b5](https://pypi.org/project/apify/3.0.6b5/)

Nov 24, 2025 [2 release files](https://pypi.org/project/apify/3.0.6b5/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.0.6b4](https://pypi.org/project/apify/3.0.6b4/)

Nov 21, 2025 [2 release files](https://pypi.org/project/apify/3.0.6b4/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.0.6b3](https://pypi.org/project/apify/3.0.6b3/)

Nov 21, 2025 [2 release files](https://pypi.org/project/apify/3.0.6b3/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.0.6b2](https://pypi.org/project/apify/3.0.6b2/)

Nov 19, 2025 [2 release files](https://pypi.org/project/apify/3.0.6b2/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.0.6b1](https://pypi.org/project/apify/3.0.6b1/)

Nov 19, 2025 [2 release files](https://pypi.org/project/apify/3.0.6b1/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[3.0.5](https://pypi.org/project/apify/3.0.5/)

Nov 18, 2025 [2 release files](https://pypi.org/project/apify/3.0.5/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.0.5b11](https://pypi.org/project/apify/3.0.5b11/)

Nov 18, 2025 [2 release files](https://pypi.org/project/apify/3.0.5b11/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.0.5b10](https://pypi.org/project/apify/3.0.5b10/)

Nov 14, 2025 [2 release files](https://pypi.org/project/apify/3.0.5b10/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.0.5b9](https://pypi.org/project/apify/3.0.5b9/)

Nov 13, 2025 [2 release files](https://pypi.org/project/apify/3.0.5b9/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.0.5b8](https://pypi.org/project/apify/3.0.5b8/)

Nov 12, 2025 [2 release files](https://pypi.org/project/apify/3.0.5b8/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.0.5b7](https://pypi.org/project/apify/3.0.5b7/)

Nov 11, 2025 [2 release files](https://pypi.org/project/apify/3.0.5b7/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.0.5b6](https://pypi.org/project/apify/3.0.5b6/)

Nov 10, 2025 [2 release files](https://pypi.org/project/apify/3.0.5b6/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.0.5b5](https://pypi.org/project/apify/3.0.5b5/)

Nov 7, 2025 [2 release files](https://pypi.org/project/apify/3.0.5b5/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.0.5b4](https://pypi.org/project/apify/3.0.5b4/)

Nov 6, 2025 [2 release files](https://pypi.org/project/apify/3.0.5b4/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.0.5b3](https://pypi.org/project/apify/3.0.5b3/)

Nov 6, 2025 [2 release files](https://pypi.org/project/apify/3.0.5b3/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.0.5b2](https://pypi.org/project/apify/3.0.5b2/)

Nov 4, 2025 [2 release files](https://pypi.org/project/apify/3.0.5b2/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.0.5b1](https://pypi.org/project/apify/3.0.5b1/)

Nov 4, 2025 [2 release files](https://pypi.org/project/apify/3.0.5b1/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[3.0.4](https://pypi.org/project/apify/3.0.4/)

Nov 3, 2025 [2 release files](https://pypi.org/project/apify/3.0.4/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.0.4b4](https://pypi.org/project/apify/3.0.4b4/)

Oct 31, 2025 [2 release files](https://pypi.org/project/apify/3.0.4b4/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.0.4b3](https://pypi.org/project/apify/3.0.4b3/)

Oct 29, 2025 [2 release files](https://pypi.org/project/apify/3.0.4b3/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.0.4b2](https://pypi.org/project/apify/3.0.4b2/)

Oct 29, 2025 [2 release files](https://pypi.org/project/apify/3.0.4b2/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.0.4b1](https://pypi.org/project/apify/3.0.4b1/)

Oct 23, 2025 [2 release files](https://pypi.org/project/apify/3.0.4b1/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[3.0.3](https://pypi.org/project/apify/3.0.3/)

Oct 21, 2025 [2 release files](https://pypi.org/project/apify/3.0.3/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.0.3b1](https://pypi.org/project/apify/3.0.3b1/)

Oct 20, 2025 [2 release files](https://pypi.org/project/apify/3.0.3b1/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[3.0.2](https://pypi.org/project/apify/3.0.2/)

Oct 17, 2025 [2 release files](https://pypi.org/project/apify/3.0.2/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.0.2b7](https://pypi.org/project/apify/3.0.2b7/)

Oct 17, 2025 [2 release files](https://pypi.org/project/apify/3.0.2b7/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.0.2b6](https://pypi.org/project/apify/3.0.2b6/)

Oct 15, 2025 [2 release files](https://pypi.org/project/apify/3.0.2b6/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.0.2b5](https://pypi.org/project/apify/3.0.2b5/)

Oct 14, 2025 [2 release files](https://pypi.org/project/apify/3.0.2b5/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.0.2b4](https://pypi.org/project/apify/3.0.2b4/)

Oct 13, 2025 [2 release files](https://pypi.org/project/apify/3.0.2b4/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.0.2b3](https://pypi.org/project/apify/3.0.2b3/)

Oct 13, 2025 [2 release files](https://pypi.org/project/apify/3.0.2b3/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.0.2b2](https://pypi.org/project/apify/3.0.2b2/)

Oct 13, 2025 [2 release files](https://pypi.org/project/apify/3.0.2b2/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.0.2b1](https://pypi.org/project/apify/3.0.2b1/)

Oct 9, 2025 [2 release files](https://pypi.org/project/apify/3.0.2b1/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[3.0.1](https://pypi.org/project/apify/3.0.1/)

Oct 8, 2025 [2 release files](https://pypi.org/project/apify/3.0.1/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.0.1b2](https://pypi.org/project/apify/3.0.1b2/)

Oct 8, 2025 [2 release files](https://pypi.org/project/apify/3.0.1b2/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.0.1b1](https://pypi.org/project/apify/3.0.1b1/)

Oct 8, 2025 [2 release files](https://pypi.org/project/apify/3.0.1b1/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[3.0.0](https://pypi.org/project/apify/3.0.0/)

Sep 29, 2025 [2 release files](https://pypi.org/project/apify/3.0.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[Pre-release](https://pypi.org/help/#pre-release-versioning)

[3.0.0rc1](https://pypi.org/project/apify/3.0.0rc1/)

Aug 22, 2025 [2 release files](https://pypi.org/project/apify/3.0.0rc1/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[2.7.3](https://pypi.org/project/apify/2.7.3/)

Aug 11, 2025 [2 release files](https://pypi.org/project/apify/2.7.3/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[2.7.2](https://pypi.org/project/apify/2.7.2/)

Jul 30, 2025 [2 release files](https://pypi.org/project/apify/2.7.2/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[2.7.1](https://pypi.org/project/apify/2.7.1/)

Jul 24, 2025 [2 release files](https://pypi.org/project/apify/2.7.1/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[2.7.0](https://pypi.org/project/apify/2.7.0/)

Jul 14, 2025 [2 release files](https://pypi.org/project/apify/2.7.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[2.6.0](https://pypi.org/project/apify/2.6.0/)

Jun 9, 2025 [2 release files](https://pypi.org/project/apify/2.6.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[2.5.0](https://pypi.org/project/apify/2.5.0/)

Mar 27, 2025 [2 release files](https://pypi.org/project/apify/2.5.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[2.4.0](https://pypi.org/project/apify/2.4.0/)

Mar 7, 2025 [2 release files](https://pypi.org/project/apify/2.4.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[2.3.1](https://pypi.org/project/apify/2.3.1/)

Feb 25, 2025 [2 release files](https://pypi.org/project/apify/2.3.1/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[2.3.0](https://pypi.org/project/apify/2.3.0/)

Feb 19, 2025 [2 release files](https://pypi.org/project/apify/2.3.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[2.2.1](https://pypi.org/project/apify/2.2.1/)

Jan 17, 2025 [2 release files](https://pypi.org/project/apify/2.2.1/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[2.2.0](https://pypi.org/project/apify/2.2.0/)

Jan 10, 2025 [2 release files](https://pypi.org/project/apify/2.2.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[2.1.0](https://pypi.org/project/apify/2.1.0/)

Dec 3, 2024 [2 release files](https://pypi.org/project/apify/2.1.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[2.0.2](https://pypi.org/project/apify/2.0.2/)

Nov 12, 2024 [2 release files](https://pypi.org/project/apify/2.0.2/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[2.0.1](https://pypi.org/project/apify/2.0.1/)

Oct 25, 2024 [2 release files](https://pypi.org/project/apify/2.0.1/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[2.0.0](https://pypi.org/project/apify/2.0.0/)

Sep 10, 2024 [2 release files](https://pypi.org/project/apify/2.0.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.7.2](https://pypi.org/project/apify/1.7.2/)

Jul 8, 2024 [2 release files](https://pypi.org/project/apify/1.7.2/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.7.1](https://pypi.org/project/apify/1.7.1/)

May 23, 2024 [2 release files](https://pypi.org/project/apify/1.7.1/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.7.0](https://pypi.org/project/apify/1.7.0/)

Mar 12, 2024 [2 release files](https://pypi.org/project/apify/1.7.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.6.0](https://pypi.org/project/apify/1.6.0/)

Feb 23, 2024 [2 release files](https://pypi.org/project/apify/1.6.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.5.5](https://pypi.org/project/apify/1.5.5/)

Feb 1, 2024 [2 release files](https://pypi.org/project/apify/1.5.5/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.5.4](https://pypi.org/project/apify/1.5.4/)

Jan 24, 2024 [2 release files](https://pypi.org/project/apify/1.5.4/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.5.3](https://pypi.org/project/apify/1.5.3/)

Jan 23, 2024 [2 release files](https://pypi.org/project/apify/1.5.3/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.5.2](https://pypi.org/project/apify/1.5.2/)

Jan 19, 2024 [2 release files](https://pypi.org/project/apify/1.5.2/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.5.1](https://pypi.org/project/apify/1.5.1/)

Jan 10, 2024 [2 release files](https://pypi.org/project/apify/1.5.1/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.5.0](https://pypi.org/project/apify/1.5.0/)

Jan 3, 2024 [2 release files](https://pypi.org/project/apify/1.5.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.4.1](https://pypi.org/project/apify/1.4.1/)

Dec 21, 2023 [2 release files](https://pypi.org/project/apify/1.4.1/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.4.0](https://pypi.org/project/apify/1.4.0/)

Dec 5, 2023 [2 release files](https://pypi.org/project/apify/1.4.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.3.0](https://pypi.org/project/apify/1.3.0/)

Nov 15, 2023 [2 release files](https://pypi.org/project/apify/1.3.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.2.0](https://pypi.org/project/apify/1.2.0/)

Oct 23, 2023 [2 release files](https://pypi.org/project/apify/1.2.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.1.5](https://pypi.org/project/apify/1.1.5/)

Oct 3, 2023 [2 release files](https://pypi.org/project/apify/1.1.5/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.1.4](https://pypi.org/project/apify/1.1.4/)

Sep 6, 2023 [2 release files](https://pypi.org/project/apify/1.1.4/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.1.3](https://pypi.org/project/apify/1.1.3/)

Aug 25, 2023 [2 release files](https://pypi.org/project/apify/1.1.3/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.1.2](https://pypi.org/project/apify/1.1.2/)

Aug 2, 2023 [2 release files](https://pypi.org/project/apify/1.1.2/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.1.1](https://pypi.org/project/apify/1.1.1/)

May 23, 2023 [2 release files](https://pypi.org/project/apify/1.1.1/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.1.0](https://pypi.org/project/apify/1.1.0/)

May 23, 2023 [2 release files](https://pypi.org/project/apify/1.1.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[1.0.0](https://pypi.org/project/apify/1.0.0/)

Mar 13, 2023 [2 release files](https://pypi.org/project/apify/1.0.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.2.0](https://pypi.org/project/apify/0.2.0/)

Mar 6, 2023 [2 release files](https://pypi.org/project/apify/0.2.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.1.0](https://pypi.org/project/apify/0.1.0/)

Feb 9, 2023 [2 release files](https://pypi.org/project/apify/0.1.0/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.0.2](https://pypi.org/project/apify/0.0.2/)

Jan 8, 2019 [2 release files](https://pypi.org/project/apify/0.0.2/#files)

![](https://pypi.org/static/images/white-cube.2351a86c.svg)

[0.0.1](https://pypi.org/project/apify/0.0.1/)

Jan 8, 2019 [1 release file](https://pypi.org/project/apify/0.0.1/#files)

[![](https://pypi-camo.freetls.fastly.net/0e16ff2846ab7bc04f1e52d760b072c987232f52/68747470733a2f2f73332e6475616c737461636b2e75732d656173742d322e616d617a6f6e6177732e636f6d2f707974686f6e646f746f72672d6173736574732f6d656469612f73706f6e736f725f7765625f6c6f676f732f416e7468726f7069635f6c6f676f5f2d5f536c6174652e706e67)Anthropic, PBCVisionary sponsor](https://www.anthropic.com/) [![](https://pypi-camo.freetls.fastly.net/2056e7cc45e271b6b509980e9ff24b8b6346f2f4/68747470733a2f2f73332e6475616c737461636b2e75732d656173742d322e616d617a6f6e6177732e636f6d2f707974686f6e646f746f72672d6173736574732f6d656469612f73706f6e736f725f7765625f6c6f676f732f626c6f6f6d626572672e706e67)BloombergVisionary sponsor](https://www.techatbloomberg.com/) [![](https://pypi-camo.freetls.fastly.net/7e24ecafc35532bbd56c7c91521ea6701110c742/68747470733a2f2f73332e6475616c737461636b2e75732d656173742d322e616d617a6f6e6177732e636f6d2f707974686f6e646f746f72672d6173736574732f6d656469612f73706f6e736f725f7765625f6c6f676f732f6872742e706e67)Hudson River TradingVisionary sponsor](https://www.hudsonrivertrading.com/careers/) [![](https://pypi-camo.freetls.fastly.net/6f7cbf25b7d9ee146661528e012e8fa51d6f3337/68747470733a2f2f73332e6475616c737461636b2e75732d656173742d322e616d617a6f6e6177732e636f6d2f707974686f6e646f746f72672d6173736574732f6d656469612f73706f6e736f725f7765625f6c6f676f732f4d6574615f6c6f636b75705f706f7369746976655f7072696d6172795f5247425f636f70795f68546b493532472e706e67)MetaVisionary sponsor](https://about.facebook.com/meta/) [![](https://pypi-camo.freetls.fastly.net/22baa32a7b36b109ce052634015d878f5d029280/68747470733a2f2f73332e6475616c737461636b2e75732d656173742d322e616d617a6f6e6177732e636f6d2f707974686f6e646f746f72672d6173736574732f6d656469612f73706f6e736f725f7765625f6c6f676f732f6e76696469612e706e67)NVIDIAVisionary sponsor](https://developer.nvidia.com/) [![](https://pypi-camo.freetls.fastly.net/34ebcaca9a4316e862f2f7641b12534f0cb81bf1/68747470733a2f2f73332e6475616c737461636b2e75732d656173742d322e616d617a6f6e6177732e636f6d2f707974686f6e646f746f72672d6173736574732f6d656469612f73706f6e736f725f7765625f6c6f676f732f6d6963726f736f66742e706e67)MicrosoftSustainability sponsor](https://aka.ms/python) [![](https://pypi-camo.freetls.fastly.net/237c8773674b9f8beff9f894a07424e3b579cd6a/68747470733a2f2f73746f726167652e676f6f676c65617069732e636f6d2f707970692d6173736574732f73706f6e736f726c6f676f732f6465706f742d636f6c6f722d6c6f676f2d35567a75416e7a6b2e706e67)DepotContinuous Integration](https://depot.dev/) [![](https://pypi-camo.freetls.fastly.net/f0e9bd2edb2aa1c533d61b0d4fda0ee761bef88a/68747470733a2f2f73746f726167652e676f6f676c65617069732e636f6d2f707970692d6173736574732f73706f6e736f726c6f676f732f6177732d636f6c6f722d6c6f676f2d416c6f43525230612e706e67)AWSCloud computing and Security Sponsor](https://aws.amazon.com/) [![](https://pypi-camo.freetls.fastly.net/530379bec76c3440bd94a24092f49e27323ad0d7/68747470733a2f2f73746f726167652e676f6f676c65617069732e636f6d2f707970692d6173736574732f73706f6e736f726c6f676f732f64617461646f672d636f6c6f722d6c6f676f2d71616563774a67722e706e67)DatadogMonitoring](https://www.datadoghq.com/) [![](https://pypi-camo.freetls.fastly.net/9706778018adad6f5bf682f55d7bbc226abe551c/68747470733a2f2f73746f726167652e676f6f676c65617069732e636f6d2f707970692d6173736574732f73706f6e736f726c6f676f732f666173746c792d636f6c6f722d6c6f676f2d766c6d424c33654c2e706e67)FastlyCDN](https://www.fastly.com/) [![](https://pypi-camo.freetls.fastly.net/522342e78db3080c18697369dde99a0ed7925e86/68747470733a2f2f73746f726167652e676f6f676c65617069732e636f6d2f707970692d6173736574732f73706f6e736f726c6f676f732f676f6f676c652d636f6c6f722d6c6f676f2d32755437496c54702e706e67)GoogleDownload Analytics](https://careers.google.com/) [![](https://pypi-camo.freetls.fastly.net/f2a422796f8e4d51d60d7030b7973aa1651bd096/68747470733a2f2f73746f726167652e676f6f676c65617069732e636f6d2f707970692d6173736574732f73706f6e736f726c6f676f732f73656e7472792d636f6c6f722d6c6f676f2d346e306a654878502e706e67)SentryError logging](https://sentry.io/for/python/?utm_source=pypi&utm_medium=paid-community&utm_campaign=python-na-evergreen&utm_content=static-ad-pypi-sponsor-learnmore) [![](https://pypi-camo.freetls.fastly.net/b0ba0741ac65afcb01ebb4bbf0634c54b8a15827/68747470733a2f2f73746f726167652e676f6f676c65617069732e636f6d2f707970692d6173736574732f73706f6e736f726c6f676f732f737461747573706167652d636f6c6f722d6c6f676f2d423232436b746e6b2e706e67)StatusPageStatus page](https://statuspage.io/)

- "PyPI", "Python Package Index", and the blocks logos are registered [trademarks](https://pypi.org/trademarks/) of the [Python Software Foundation](https://www.python.org/psf-landing).
- © 2026 [Python Software Foundation](https://www.python.org/psf-landing/ "External link")
- [Site map](https://pypi.org/sitemap/)
- Deployed from [`8f38ce5`](https://github.com/pypi/warehouse/commit/8f38ce5c45aef4f0370509d6651551073a2a82fa "External link")
