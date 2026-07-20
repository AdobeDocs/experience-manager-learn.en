---
title: Store data at the edge
description: Learn how to enable a KV store for an AEM Edge Function to read and write runtime key-value data that persists at the edge across function invocations.
version: Experience Manager as a Cloud Service
feature: Developing
topic: Development, Architecture
role: Developer
level: Intermediate
doc-type: Article
jira: KT-22078
thumbnail: KT-22078.jpeg
last-substantial-update: 2026-07-16
---
# Store data at the edge

>[!IMPORTANT]
>
>AEM Edge Functions is currently in beta. Features and documentation may change. For feedback, contact [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com).

>[!NOTE]
>
>Config, secret, and KV stores are not available in sandbox programs. Use a non-sandbox environment or an RDE to test a KV store.

An AEM Edge Function often needs to keep data at the edge, close to your visitors, and reuse it across function invocations without a round trip to origin. AEM Edge Functions provide this edge data storage through a _KV store_.

A KV store is a key-value store that you read and write at runtime. Its data persists between function invocations, so any part of your AEM Edge Function code can read what another part wrote earlier. Use it to cache computed results, hold redirect maps, or share data across requests.

## When to use a KV store

Unlike `configs`, which you set at deploy time and read only, a KV store is read and written at runtime. One `kv_default` store is provisioned for your AEM Edge Function, and any of its modules or endpoints can read and write to it.

| | `configs` | KV store |
| --- | --- | --- |
| Access | Read-only at runtime | Read and write at runtime |
| Set by | You, at deploy time in `edgeFunctions.yaml` | Your function code at runtime |
| Store name | `config_default` | `kv_default` |
| Use for | Static per-environment settings | Data that changes at runtime |

## Enable the KV store

Set `kvs: true` under `data` in `edgeFunctions.yaml`, as a sibling of `functions`. This one toggle provisions the `kv_default` store for the AEM Edge Function.

```yaml
# config/edgeFunctions.yaml
kind: "EdgeFunctions"
version: "1"
data:
  functions:
    - name: my-edge-function
  kvs: true # enable the KV store
```

Deploy the updated configuration through the Cloud Manager config pipeline, or with `aio aem rde:install -t env-config ./config` on an RDE. See [Set up AEM Edge Functions on AEM as a Cloud Service](../setup-aemcs.md) or [Set up AEM Edge Functions on Edge Delivery Services](../setup-eds.md) for more details.

## Read and write in code

Open the `kv_default` store, then call `get()` and `put()`. Both calls are asynchronous. Values are strings, so serialize objects with `JSON.stringify()` and parse them on read.

```js
// src/index.js or handler file
import { KVStore } from "fastly:kv-store";

// open the KV store
const kv = new KVStore("kv_default");

// write a value (serialize objects to a string)
await kv.put("greeting", JSON.stringify({ text: "Hello from the edge" }));

// read a value (get returns an entry, or null when the key is missing)
const entry = await kv.get("greeting");
const value = entry ? JSON.parse(await entry.text()) : null;
```

## Cache data with a KV store

A common pattern is cache-aside. The handler reads from the KV store first, and only calls the backend on a miss. The KV store does not expire entries for you, so store an expiry with the value on write and check it on read.

```js
// src/lib/cache.js
import { KVStore } from "fastly:kv-store";

const kv = new KVStore("kv_default");

// Get a cached value from the KV store, or null if missing or expired
export async function getCached(key) {
  const entry = await kv.get(key);
  if (!entry) {
    return null;
  }

  // Parse the value and check the stored expiry
  const cached = JSON.parse(await entry.text());
  if (Date.now() > cached.expiresAt) {
    return null;
  }
  return cached.payload;
}

// Set a value in the KV store with an expiry ttlSeconds from now
export async function setCached(key, payload, ttlSeconds) {
  const expiresAt = Date.now() + ttlSeconds * 1000;
  await kv.put(key, JSON.stringify({ expiresAt, payload }));
}
```

In a handler, read the cache, fall back to the backend on a miss, then write the result back.

```js
let data = await getCached("inventory:west");
if (!data) {
  data = await fetchFromBackend();
  await setCached("inventory:west", data, 60); // cache for 60 seconds
}
```

## Populate the KV store

The KV store has no deploy-time seeding in `edgeFunctions.yaml`. Your function code writes every value at runtime. Two common approaches are:

- **On demand.** Fill an entry the first time it is requested, as the cache-aside pattern above does.
- **Through a maintenance endpoint.** Expose an endpoint that rebuilds entries, then call it on a schedule. This suits large, slow-changing data sets such as redirect maps.

## Guidelines

- Enable the store with `kvs: true` before your code reads or writes to it.
- The store is shared by all your AEM Edge Function code. Namespace your keys with a prefix, such as `redirect:` or `inventory:`, so different modules or endpoints do not collide.
- Key names are case-sensitive.
- Values are strings. Serialize objects with `JSON.stringify()` and parse them on read.
- Handle a missing key. `get()` returns `null` when the key does not exist.
- A KV store is eventually consistent. Right after a write, a read can briefly return the previous value, so avoid depending on read-after-write for critical logic.

## Complete example

The [AEM Edge Functions examples](https://github.com/adobe/aem-edge-functions-examples/tree/main/examples) repository includes a KV store example with full `config/` and code:

| Example | Repository | What it demonstrates |
| --- | --- | --- |
| Redirect map lookup | [publish-delivery-redirect-maps](https://github.com/adobe/aem-edge-functions-examples/tree/main/examples/publish-delivery-redirect-maps) | Reads redirect targets from the KV store at request time, rebuilds sharded map entries through a maintenance endpoint, and falls back to origin on a miss |

## Additional resources

- [Build an API endpoint with Edge Functions](./build-api-endpoint.md)
- [Serve multiple endpoints with Edge Functions](./multiple-endpoints.md)
- [HTTP request filters with Edge Functions](./request-filtering.md)
- [Use configs and secrets with Edge Functions](./configs-and-secrets.md)
- [Set up AEM Edge Functions on AEM as a Cloud Service](../setup-aemcs.md)
- [Set up AEM Edge Functions on Edge Delivery Services](../setup-eds.md)
- [AEM Edge Functions product documentation](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/edge-functions)
- [About edge data stores](https://www.fastly.com/documentation/guides/compute/edge-data-storage/about-edge-data-stores/)
