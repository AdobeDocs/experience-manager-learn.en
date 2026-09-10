---
title: Build an API endpoint with Edge Functions
description: Learn how to expose HTTP endpoints with AEM Edge Functions using the fetch event handler, endpoint matching, CDN origin selectors, and outbound fetch calls.
version: Experience Manager as a Cloud Service
feature: Developing
topic: Development, Architecture
role: Developer
level: Intermediate
doc-type: Article
jira: KT-21976
thumbnail: KT-21976.jpeg
last-substantial-update: 2026-07-13
---
# Build an API endpoint with Edge Functions

An AEM Edge Function is a JavaScript module that runs on Adobe CDN (Fastly Compute). You expose it as _one or more_ HTTP endpoints by pairing CDN origin selector rules with a fetch event handler in your code.

This page covers the contract and key files. You can write any logic in the handler, including outbound `fetch()` calls to other systems. Keep the handler fast and short-lived so it fits the edge runtime.

## Prerequisites

- An AEM Edge Functions project based on the [boilerplate template](https://github.com/adobe/aem-edge-functions-boilerplate)
- Adobe CLI with the AEM Edge Functions plugin installed

For first-time setup, see [Set up on AEM as a Cloud Service](../setup-aemcs.md) or [Set up on Edge Delivery Services](../setup-eds.md).

## How an HTTP request reaches your code

A request reaches your AEM Edge Function in two steps: the CDN origin selector routes the endpoint to the function, then your fetch event handler runs.

```text
Browser → CDN origin selector (cdn.yaml) → AEM Edge Function (index.js) → Your handler logic (optional fetch to other systems)
```

| Layer | File | Responsibility |
| --- | --- | --- |
| CDN | `config/cdn.yaml` | Match a path and forward the request to the AEM Edge Function |
| Function | `config/edgeFunctions.yaml` | Declare the AEM Edge Function name and optional `configs`, `secrets`, or `kvs` |
| Code | `src/index.js` | Match endpoints, run handler logic, and return a `Response` |

The origin selector and the function name must align. If `edgeFunctions.yaml` declares `my-edge-function`, the origin selector uses `edgefunction-my-edge-function` in `cdn.yaml`.

```yaml
# config/edgeFunctions.yaml
kind: "EdgeFunctions"
version: "1"
data:
  functions:
    - name: my-edge-function #<name-of-the-function>
```

```yaml
# config/cdn.yaml (origin selector excerpt)
kind: 'CDN'
version: '1'
data:
  originSelectors:
    rules:
      - name: route-status-endpoint-to-edge-function # logical name for the origin selector rule
        when: { reqProperty: path, equals: "/status" } # path to match
        action:
          type: selectAemOrigin
          originName: edgefunction-my-edge-function # edgefunction-<name-of-the-function>
          skipCache: false # false to use the CDN cache for this path
      - name: route-my-api-to-edge-function # logical name for the origin selector rule
        when: { reqProperty: path, equals: "/my-api" } # path to match
        action:
          type: selectAemOrigin
          originName: edgefunction-my-edge-function # edgefunction-<name-of-the-function>
          skipCache: true # true to bypass the CDN cache for this path
```

Each endpoint needs its own origin selector rule in `cdn.yaml`. One AEM Edge Function can serve multiple endpoints, but the CDN must forward each path to that function. Set `skipCache: false` to allow CDN caching for stable responses, or `skipCache: true` to bypass the CDN cache for dynamic or personalized responses.

For origin selector options, see [Origin selectors](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn-configuring-traffic#origin-selectors).

## Handle requests

Every AEM Edge Function registers a fetch event handler. Adobe CDN invokes that handler for each matching request. The handler reads the incoming `Request`, runs your logic, and returns a `Response`.

```js
// src/index.js
import { myApiHandler } from "./my-api.js";
import * as response from "./lib/response.js";

// entry point for the AEM Edge Function
addEventListener("fetch", (event) => event.respondWith(handleRequest(event)));

async function handleRequest(event) {
  // event.request is a standard Fetch API Request (method, URL, headers, body)
  const req = event.request;
  const url = new URL(req.url);

  try {
    // endpoint matching
    if (url.pathname === "/status" && req.method === "GET") {
      return new Response("OK", { status: 200 });
    } else if (url.pathname === "/my-api" && req.method === "GET") {
      return await myApiHandler(req, event.client);
    }
    // add more endpoints here

    return response.notFound();
  } catch (err) {
    console.log(err);
    return response.error();
  }
}
```

Key points:

| Concept | Detail |
| --- | --- |
| Entry point | `addEventListener("fetch", ...)` wires every request to your fetch event handler, see [FetchEvent.respondWith](https://js-compute-reference-docs.edgecompute.app/docs/globals/FetchEvent/prototype/respondWith) |
| Request | `event.request` is a standard Fetch API `Request` (method, URL, headers, body), see [Request reference](https://js-compute-reference-docs.edgecompute.app/docs/globals/Request/) |
| Response | Return `new Response(body, { status, headers })` to control status, content type, and cache headers, see [Response reference](https://js-compute-reference-docs.edgecompute.app/docs/globals/Response/) |
| Endpoint matching | Match on `url.pathname`, HTTP method, headers, or query parameters inside `handleRequest` |
| Client metadata | `event.client` exposes connection details such as the client IP address, see [FetchEvent.client](https://js-compute-reference-docs.edgecompute.app/docs/globals/FetchEvent/) |

Endpoint matching lives in `index.js`. As your endpoints grow, move handler logic into separate files and import them, as `my-api.js` does in the example above. See [Serve multiple endpoints with Edge Functions](./multiple-endpoints.md) for patterns as your API surface expands.

## Write your handler logic

Inside each endpoint handler, you can run any JavaScript that fits the edge runtime. Keep the work fast and short-lived. Prefer lightweight transforms, geo lookups, simple JSON or HTML responses, and small aggregations over long-running or heavy compute.

A minimal response looks like this:

```js
if (url.pathname === "/status" && req.method === "GET") {
  return new Response("OK", { status: 200 });
}
```

You can return JSON, HTML, or plain text. Set headers on the `Response` to control content type and caching:

```js
return new Response(JSON.stringify({ status: "ok" }), {
  status: 200,
  headers: {
    "Content-Type": "application/json",
    "Cache-Control": "public, max-age=300",
  },
});
```

When you need data from another system, call it with `fetch()`. Keep credentials in the AEM Edge Function. Do not expose secrets in client JavaScript.

```js
// src/my-api.js
async function myApiHandler(req, client) {
  const backendRequest = new Request("https://api.example.com/data");

  // optionally, you can add headers to the request
  // backendRequest.headers.set("Authorization", `Bearer <your-access-token>`);

  const backendResponse = await fetch(backendRequest);

  if (!backendResponse.ok) {
    return new Response("Backend error", { status: 502 });
  }

  const data = await backendResponse.json();

  return new Response(JSON.stringify(data), {
    status: 200,
    headers: {
      "Content-Type": "application/json",
      "Cache-Control": "max-age=300",
    },
  });
}

export { myApiHandler };
```

Outbound `fetch()` calls typically follow this pattern:

1. Derive context from the request (`headers`, `event.client`, Fastly geolocation helpers).
2. Build a `Request` to the other system.
3. Call `await fetch(request)` (optionally with a named `backend` origin).
4. Parse the response and return a new `Response` to the client.

Platform limits apply. Each invocation supports up to **32 outbound fetch calls**. For cache behavior on fetch calls, see [Caching in AEM Edge Functions](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/edge-functions-caching).

## More code examples

For complete working examples, see the [AEM Edge Functions boilerplate](https://github.com/adobe/aem-edge-functions-boilerplate):

| Example | File | What it shows |
| --- | --- | --- |
| Simple response | [`src/index.js`](https://github.com/adobe/aem-edge-functions-boilerplate/blob/main/src/index.js) | Route matching and a response built in the handler |
| External API | [`src/weather.js`](https://github.com/adobe/aem-edge-functions-boilerplate/blob/main/src/weather.js) | Geo lookup plus outbound `fetch()` |

## Additional resources

- [Serve multiple endpoints with Edge Functions](./multiple-endpoints.md)
- [Set up AEM Edge Functions on AEM as a Cloud Service](../setup-aemcs.md)
- [Set up AEM Edge Functions on Edge Delivery Services](../setup-eds.md)
- [AEM Edge Functions product documentation](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/edge-functions)
- [AEM Edge Functions boilerplate](https://github.com/adobe/aem-edge-functions-boilerplate)
