---
url: https://docs.apify.com/sdk/python/docs/concepts/storage-clients.md
retrieved: 2026-10-04
command: firecrawl scrape https://docs.apify.com/sdk/python/docs/concepts/storage-clients.md --only-main-content --json
statusCode: 200
transport: firecrawl-cli
completeness: full
---
# Storage clients

Copy for LLM

Storage clients are the components that read and write your [storages](https://docs.apify.com/sdk/python/docs/concepts/storages.md): datasets, key-value stores, and request queues. The Apify SDK selects an appropriate client automatically based on where the Actor runs. For most Actors you never need to think about them. This page explains the available clients and how to customize them when you do.

For details on how storage clients work and how to write your own, see the [Crawlee storage clients guide](https://crawlee.dev/python/docs/guides/storage-clients).

## How the Actor selects a storage client[](#how-the-actor-selects-a-storage-client)

By default, the Actor uses a [`SmartApifyStorageClient`](https://docs.apify.com/sdk/python/reference/class/SmartApifyStorageClient.md), a hybrid client that delegates to one of two underlying clients depending on the environment:

* When running on the Apify platform (detected automatically), or when you pass `force_cloud=True`, it uses the cloud client, [`ApifyStorageClient`](https://docs.apify.com/sdk/python/reference/class/ApifyStorageClient.md), which persists data through the Apify API.
* When running locally, it uses the local client, [`FileSystemStorageClient`](https://docs.apify.com/sdk/python/reference/class/FileSystemStorageClient.md), which emulates platform storages on your filesystem under the `storage` folder.

As a result, the same Actor code can run unchanged both locally and on the platform.

## Available storage clients[](#available-storage-clients)

The `apify.storage_clients` module provides the following clients:

* [`SmartApifyStorageClient`](https://docs.apify.com/sdk/python/reference/class/SmartApifyStorageClient.md) - the default hybrid client. It wraps a `cloud_storage_client` and a `local_storage_client` and routes each call to the right one.
* [`ApifyStorageClient`](https://docs.apify.com/sdk/python/reference/class/ApifyStorageClient.md) - talks to the Apify API. Used as the cloud client.
* [`FileSystemStorageClient`](https://docs.apify.com/sdk/python/reference/class/FileSystemStorageClient.md) - persists data to the local filesystem. Used as the default local client.
* [`MemoryStorageClient`](https://docs.apify.com/sdk/python/reference/class/MemoryStorageClient.md) - keeps everything in memory and persists nothing. Useful for tests and short-lived runs.

All of these clients implement Crawlee's [`StorageClient`](https://docs.apify.com/sdk/python/reference/class/StorageClient.md) interface, so any of them can be used as a sub-client of `SmartApifyStorageClient`. For details, see [customizing the storage client](#customizing-the-storage-client).

Crawlee additionally ships storage clients backed by a self-hosted database: a [`RedisStorageClient`](https://crawlee.dev/python/api/class/RedisStorageClient) and a [`SqlStorageClient`](https://crawlee.dev/python/api/class/SqlStorageClient). The Apify SDK doesn't re-export these, because they each require an extra dependency that the SDK doesn't install. To use one of the storage clients:

1. Install the matching Crawlee extra (`crawlee[redis]`, `crawlee[sql-postgres]`, or `crawlee[sql-sqlite]`).
2. Import the client from `crawlee.storage_clients` and pass it as a sub-client of `SmartApifyStorageClient`.

For details, see the [Crawlee storage clients guide](https://crawlee.dev/python/docs/guides/storage-clients).

## Single vs. shared request queue[](#single-vs-shared-request-queue)

`ApifyStorageClient` supports two ways of accessing the Apify request queue, selected via its `request_queue_access` argument:

* **`'single'`** (default) - optimized for a single consumer. It makes fewer API calls, so it's cheaper and faster, but it doesn't support multiple clients consuming the same queue concurrently. This is the right choice for the majority of Actors.
* **`'shared'`** - supports multiple consumers working on the same queue at the same time, at the cost of more API calls. Use it when several Actor runs share one named request queue. For example, you can split a large crawl across parallel runs, or feed the queue from a producer run while worker runs consume it.

To opt into the shared client, set it as the cloud client of the `SmartApifyStorageClient` in the [service locator](https://crawlee.dev/python/docs/guides/service-locator) before entering the Actor context:

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuZnJvbSBjcmF3bGVlIGltcG9ydCBzZXJ2aWNlX2xvY2F0b3JcXG5cXG5mcm9tIGFwaWZ5IGltcG9ydCBBY3RvclxcbmZyb20gYXBpZnkuc3RvcmFnZV9jbGllbnRzIGltcG9ydCBBcGlmeVN0b3JhZ2VDbGllbnQsIFNtYXJ0QXBpZnlTdG9yYWdlQ2xpZW50XFxuXFxuXFxuYXN5bmMgZGVmIG1haW4oKSAtPiBOb25lOlxcbiAgICAjIFVzZSB0aGUgc2hhcmVkIEFwaWZ5IHJlcXVlc3QgcXVldWUgY2xpZW50LCB3aGljaCBzdXBwb3J0cyBtdWx0aXBsZVxcbiAgICAjIGNvbnN1bWVycyB3b3JraW5nIG9uIHRoZSBzYW1lIHF1ZXVlIGF0IHRoZSBjb3N0IG9mIG1vcmUgQVBJIGNhbGxzLlxcbiAgICBjbG91ZF9zdG9yYWdlX2NsaWVudCA9IEFwaWZ5U3RvcmFnZUNsaWVudChyZXF1ZXN0X3F1ZXVlX2FjY2Vzcz0nc2hhcmVkJylcXG4gICAgc2VydmljZV9sb2NhdG9yLnNldF9zdG9yYWdlX2NsaWVudChcXG4gICAgICAgIFNtYXJ0QXBpZnlTdG9yYWdlQ2xpZW50KGNsb3VkX3N0b3JhZ2VfY2xpZW50PWNsb3VkX3N0b3JhZ2VfY2xpZW50KSxcXG4gICAgKVxcblxcbiAgICBhc3luYyB3aXRoIEFjdG9yOlxcbiAgICAgICAgcmVxdWVzdF9xdWV1ZSA9IGF3YWl0IEFjdG9yLm9wZW5fcmVxdWVzdF9xdWV1ZSgpXFxuICAgICAgICBhd2FpdCByZXF1ZXN0X3F1ZXVlLmFkZF9yZXF1ZXN0KCdodHRwczovL2NyYXdsZWUuZGV2JylcXG5cXG5cXG5pZiBfX25hbWVfXyA9PSAnX19tYWluX18nOlxcbiAgICBhc3luY2lvLnJ1bihtYWluKCkpXFxuXCJ9Iiwib3B0aW9ucyI6eyJidWlsZCI6ImxhdGVzdCIsImNvbnRlbnRUeXBlIjoiYXBwbGljYXRpb24vanNvbjsgY2hhcnNldD11dGYtOCIsIm1lbW9yeSI6MTAyNCwidGltZW91dCI6MTgwfX0.TjwfGyN7kn7fMA9rwn-VqJApbuvQIPnOFQVSaFgySPs\&asrc=run_on_apify)

```
import asyncio



from crawlee import service_locator



from apify import Actor

from apify.storage_clients import ApifyStorageClient, SmartApifyStorageClient





async def main() -> None:

    # Use the shared Apify request queue client, which supports multiple

    # consumers working on the same queue at the cost of more API calls.

    cloud_storage_client = ApifyStorageClient(request_queue_access='shared')

    service_locator.set_storage_client(

        SmartApifyStorageClient(cloud_storage_client=cloud_storage_client),

    )



    async with Actor:

        request_queue = await Actor.open_request_queue()

        await request_queue.add_request('https://crawlee.dev')





if __name__ == '__main__':

    asyncio.run(main())
```

## Using cloud storage while running locally[](#using-cloud-storage-while-running-locally)

When developing locally, storages are read from and written to the local filesystem by default. To work with a storage on the Apify platform instead (for example, to read the output of a remote Actor run), pass `force_cloud=True` to [`Actor.open_dataset`](https://docs.apify.com/sdk/python/reference/class/Actor.md#open_dataset), [`Actor.open_key_value_store`](https://docs.apify.com/sdk/python/reference/class/Actor.md#open_key_value_store), or [`Actor.open_request_queue`](https://docs.apify.com/sdk/python/reference/class/Actor.md#open_request_queue). This requires an Apify token, provided via the `APIFY_TOKEN` environment variable.

## Customizing the storage client[](#customizing-the-storage-client)

You can replace either of the underlying clients, for example to keep all local data in memory instead of on disk. To do this, set a `SmartApifyStorageClient` with your chosen sub-clients in the service locator before entering the Actor context (or awaiting [`Actor.init`](https://docs.apify.com/sdk/python/reference/class/Actor.md#init)):

[Run on](https://console.apify.com/actors/HH9rhkFXiZbheuq1V?runConfig=eyJ1IjoiRWdQdHczb2VqNlRhRHQ1cW4iLCJ2IjoxfQ.eyJpbnB1dCI6IntcImNvZGVcIjpcImltcG9ydCBhc3luY2lvXFxuXFxuZnJvbSBjcmF3bGVlIGltcG9ydCBzZXJ2aWNlX2xvY2F0b3JcXG5cXG5mcm9tIGFwaWZ5IGltcG9ydCBBY3RvclxcbmZyb20gYXBpZnkuc3RvcmFnZV9jbGllbnRzIGltcG9ydCBNZW1vcnlTdG9yYWdlQ2xpZW50LCBTbWFydEFwaWZ5U3RvcmFnZUNsaWVudFxcblxcblxcbmFzeW5jIGRlZiBtYWluKCkgLT4gTm9uZTpcXG4gICAgIyBLZWVwIGFsbCBsb2NhbCBkYXRhIGluIG1lbW9yeSBpbnN0ZWFkIG9mIHdyaXRpbmcgaXQgdG8gdGhlIGZpbGVzeXN0ZW1cXG4gICAgIyB3aGVuIHJ1bm5pbmcgb3V0c2lkZSB0aGUgQXBpZnkgcGxhdGZvcm0uXFxuICAgIGxvY2FsX3N0b3JhZ2VfY2xpZW50ID0gTWVtb3J5U3RvcmFnZUNsaWVudCgpXFxuICAgIHNlcnZpY2VfbG9jYXRvci5zZXRfc3RvcmFnZV9jbGllbnQoXFxuICAgICAgICBTbWFydEFwaWZ5U3RvcmFnZUNsaWVudChsb2NhbF9zdG9yYWdlX2NsaWVudD1sb2NhbF9zdG9yYWdlX2NsaWVudCksXFxuICAgIClcXG5cXG4gICAgYXN5bmMgd2l0aCBBY3RvcjpcXG4gICAgICAgIHN0b3JlID0gYXdhaXQgQWN0b3Iub3Blbl9rZXlfdmFsdWVfc3RvcmUoKVxcbiAgICAgICAgYXdhaXQgc3RvcmUuc2V0X3ZhbHVlKCdleGFtcGxlJywgeydoZWxsbyc6ICd3b3JsZCd9KVxcblxcblxcbmlmIF9fbmFtZV9fID09ICdfX21haW5fXyc6XFxuICAgIGFzeW5jaW8ucnVuKG1haW4oKSlcXG5cIn0iLCJvcHRpb25zIjp7ImJ1aWxkIjoibGF0ZXN0IiwiY29udGVudFR5cGUiOiJhcHBsaWNhdGlvbi9qc29uOyBjaGFyc2V0PXV0Zi04IiwibWVtb3J5IjoxMDI0LCJ0aW1lb3V0IjoxODB9fQ.7_beLahfT6WCXKdtWUAssazJ0Q9qHYkIvLMGhLLKHFc\&asrc=run_on_apify)

```
import asyncio



from crawlee import service_locator



from apify import Actor

from apify.storage_clients import MemoryStorageClient, SmartApifyStorageClient





async def main() -> None:

    # Keep all local data in memory instead of writing it to the filesystem

    # when running outside the Apify platform.

    local_storage_client = MemoryStorageClient()

    service_locator.set_storage_client(

        SmartApifyStorageClient(local_storage_client=local_storage_client),

    )



    async with Actor:

        store = await Actor.open_key_value_store()

        await store.set_value('example', {'hello': 'world'})





if __name__ == '__main__':

    asyncio.run(main())
```

note

The Actor's storage client must be a `SmartApifyStorageClient`. Setting a bare `ApifyStorageClient` or `MemoryStorageClient` directly in the service locator raises an error. Wrap it in a `SmartApifyStorageClient` as shown above.

