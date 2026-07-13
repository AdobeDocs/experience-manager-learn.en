---
title: Host an API or route
description: Learn how to expose HTTP endpoints with AEM Edge Functions using the fetch handler, route matching, CDN origin selectors, and outbound fetch calls.
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
# Build an API endpoint

>[!IMPORTANT]
>
>AEM Edge Functions is currently in beta. Features and documentation may change. For feedback, contact [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com).

An AEM Edge Function is a JavaScript module that runs on Adobe CDN (Fastly Compute). You expose it as _one or more_ HTTP endpoints by pairing CDN routing rules with a fetch event handler in your code.

This page covers the contract, the key files, and two common handler patterns, compute at the edge and fetch (calling an external API) over the network.

## Prerequisites

- An AEM Edge Functions project based on the [boilerplate template](https://github.com/adobe/aem-edge-functions-boilerplate)
- Adobe CLI with the AEM Edge Functions plugin installed

For first-time setup, see [Set up on AEM as a Cloud Service](../setup-aemcs.md) or [Set up on Edge Delivery Services](../setup-eds.md).

## How a HTTP request reaches your code

A request hits your AEM Edge Function service in two steps: CDN routing, then JavaScript handling.

```text
Browser → CDN origin selector (cdn.yaml) → AEM Edge Function (index.js) → Compute at the edge or fetch over the network
```

| Layer | File | Responsibility |
| --- | --- | --- |
| CDN | `config/cdn.yaml` | Match a path and forward the request to the AEM Edge Function service |
| Function service | `config/edgeFunctions.yaml` | Declare the AEM Edge Function service with the function name and optional `configs`, `secrets`, or `kvs` |
| Code | `src/index.js` | Receives the request, matches routes, delegates to handler modules, and returns a `Response` |

The CDN rule and the function name must align. If `edgeFunctions.yaml` declares `my-edge-function`, the origin selector uses `edgefunction-my-edge-function` in the `cdn.yaml` file.

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
      - name: route-compute-bound-route-to-edge-function # logical name for the origin selector rule
        when: { reqProperty: path, equals: "/my-route" } # path to match
        action:
          type: selectAemOrigin
          originName: edgefunction-my-edge-function # edgefunction-<name-of-the-function>
          skipCache: false # false to use the CDN cache for this route
      - name: route-my-api-to-edge-function # logical name for the origin selector rule
        when: { reqProperty: path, equals: "/my-api" } # path to match
        action:
          type: selectAemOrigin
          originName: edgefunction-my-edge-function # edgefunction-<name-of-the-function>
          skipCache: true # true to bypass the CDN cache for this route
```

Each path you expose needs its own origin selector rule in `cdn.yaml`. One AEM Edge Function service can serve multiple routes, but the CDN must route each path to that function. Set `skipCache: false` to allow CDN caching for stable responses, or `skipCache: true` to bypass the CDN cache for dynamic or personalized routes.

For more information on origin selector options, see [Origin selectors](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn-configuring-traffic#origin-selectors).

## The fetch handler contract

Every AEM Edge Function registers a fetch listener. Adobe CDN (Fastly Compute) invokes your handler for each matching request. The handler reads the incoming `Request`, runs logic, and returns a `Response`.

```js
// src/index.js
import { myApiHandler } from "./my-api.js";
import * as response from "./lib/response.js";

// entry point for the AEM Edge Function, wires every request to your handler
addEventListener("fetch", (event) => event.respondWith(handleRequest(event)));

async function handleRequest(event) {
  // the request object is a standard Fetch API Request (method, URL, headers, body)
  const req = event.request;
  const url = new URL(req.url);

  try {
    // route matching logic
    if (url.pathname === "/my-route" && req.method === "GET") {
      // compute-bound route
      return new Response("OK", { status: 200 });
    } else if (url.pathname === "/my-api" && req.method === "GET") {
      // network-bound route
      return await myApiHandler(req, event.client);
    }
    // add more route matching logic here

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
| Entry point | `addEventListener("fetch", ...)` wires every request to your handler |
| Request object | `event.request` is a standard Fetch API `Request` (method, URL, headers, body) |
| Response object | Return `new Response(body, { status, headers })` to control status, content type, and cache headers |
| Route matching | Match on `url.pathname`, HTTP method, headers, or query parameters inside `handleRequest` |
| Client metadata | `event.client` exposes connection details such as the client IP address |

Route logic lives in `index.js`. For larger functions, move each route into its own module and import it. In the example above, `my-api.js` handles the network-bound route.

## Compute-bound endpoint

A compute-bound handler runs entirely at the edge. It does not call origin or external APIs. Use this pattern for static JSON, lightweight transforms, geo lookups with Fastly built-ins, or HTML fragments built from request data.

```js
if (url.pathname === "/my-route" && req.method === "GET") {
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

Because no origin round trip occurs, compute-bound routes typically have the lowest latency.

## Network-bound endpoint

A network-bound handler calls one or more external APIs with `fetch()`. Use this pattern to proxy APIs, aggregate data from multiple services, or enrich a response with live data while _keeping credentials on the server side_.

```js
// src/my-api.js
async function myApiHandler(req, client) {
  const backendRequest = new Request("https://api.example.com/data");

  // optionally, you can add headers to the request
  //backendRequest.headers.set("Authorization", `Bearer <your-access-token>`);

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

Network-bound handlers follow this pattern:

1. Derive context from the request (`headers`, `event.client`, Fastly geolocation helpers).
2. Build a `Request` to the backend URL.
3. Call `await fetch(request)` (optionally with a named `backend` origin).
4. Parse the backend response and return a new `Response` to the client.

Platform limits apply. Each invocation supports up to **32 outbound fetch calls**. For cache behavior on fetch calls, see [Caching in AEM Edge Functions](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/edge-functions-caching).


## Compare handler patterns

For complete working examples, see the [AEM Edge Functions boilerplate](https://github.com/adobe/aem-edge-functions-boilerplate).

| Pattern | Boilerplate example | Uses fetch() | Typical use |
| --- | --- | --- | --- |
| Compute-bound | [`src/index.js`](https://github.com/adobe/aem-edge-functions-boilerplate/blob/main/src/index.js#L29-L32) | No | Static or dynamic responses built at the edge |
| Network-bound | [`src/weather.js`](https://github.com/adobe/aem-edge-functions-boilerplate/blob/main/src/weather.js) | Yes | API proxy, data aggregation, live enrichment |

Both patterns share the same entry contract in `index.js`. The CDN origin selector delivers the request; your handler decides whether to compute locally or call over the network.

## Next steps

- [Set up on AEM as a Cloud Service](../setup-aemcs.md): deploy the boilerplate end to end
- [AEM Edge Functions product documentation](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/edge-functions)
- [AEM Edge Functions boilerplate](https://github.com/adobe/aem-edge-functions-boilerplate): full project with tests, secrets, config store, and KV store examples
