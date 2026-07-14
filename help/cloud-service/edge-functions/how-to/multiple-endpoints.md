---
title: Serve multiple endpoints with Edge Functions
description: Learn how one AEM Edge Function can expose many HTTP endpoints, and how to organize handler logic as your API surface grows.
version: Experience Manager as a Cloud Service
feature: Developing
topic: Development, Architecture
role: Developer
level: Intermediate
doc-type: Article
last-substantial-update: 2026-07-14
---
# Serve multiple endpoints with Edge Functions

>[!IMPORTANT]
>
>AEM Edge Functions is currently in beta. Features and documentation may change. For feedback, contact [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com).

One AEM Edge Function can expose many HTTP endpoints. The examples in [Build an API endpoint](./build-api-endpoint.md) already show two endpoints (`/status` and `/my-api`) on a single JavaScript function. You _do not deploy a separate function for each endpoint_ but just add endpoint matching logic to the same function.

## Key point

| Layer | What scales |
| --- | --- |
| `edgeFunctions.yaml` | One function declaration with a name, for example `my-edge-function` |
| `cdn.yaml` | One origin selector rule **per endpoint**, all rules share the same (for example, `edgefunction-my-edge-function`) origin, but each rule has its own path matching rule |
| `index.js` | One `if` statement **per endpoint**, and statement body has its own handler logic |


## How to add another endpoint

To expose a new endpoint such as `/api/items`:

1. Add endpoint matching logic in `src/index.js`.
1. Build and deploy the AEM Edge Function.
1. Add an origin selector rule in `config/cdn.yaml` for the endpoint.
1. Deploy the CDN configuration

## How to organize handler logic

Keep `index.js` focused on endpoint matching. Move handler logic into separate files as the API grows.

```text
src/
├── index.js          # fetch event handler and endpoint matching
├── my-api.js         # handler for /my-api
├── items.js          # handler for /api/items
└── lib/
    └── response.js   # shared 404 and 500 helpers
```

## Match on method or path prefix

Endpoint matching is plain JavaScript. You are not limited to exact path equality.

**HTTP method:** Handle `GET` and `POST` on the same path with separate `if` statements.

```js
if (url.pathname === "/api/items" && req.method === "GET") {
  return await listItems(req);
}

if (url.pathname === "/api/items" && req.method === "POST") {
  return await createItem(req);
}
```

**Path prefix:** Group related endpoints under a shared prefix, then dispatch to a handler inside a router module.

```js
// src/index.js
if (url.pathname.startsWith("/api/")) {
  return await apiRouter(req, url);
}
```

```js
// src/api-router.js
async function apiRouter(req, url) {
  // match the segment after the shared /api/ prefix
  switch (url.pathname) {
    case "/api/items":
      return await itemsHandler(req);
    case "/api/orders":
      return await ordersHandler(req);
    default:
      return new Response("Not found", { status: 404 });
  }
}

export { apiRouter };
```

Keep prefix routers shallow, meaning one prefix level that dispatches straight to a handler. If a prefix grows large, split it into separate prefixes with their own origin selector rules (for example, `/api/catalog/` and `/api/checkout/`) instead of nesting routers under one prefix.

## More code examples

The [AEM Edge Functions boilerplate](https://github.com/adobe/aem-edge-functions-boilerplate) ships multiple endpoints in one function:

| Example | File | What it shows |
| --- | --- | --- |
| Endpoint matching | [`src/index.js`](https://github.com/adobe/aem-edge-functions-boilerplate/blob/main/src/index.js) | Several paths in one fetch event handler |
| CDN rules | [`config/cdn.yaml`](https://github.com/adobe/aem-edge-functions-boilerplate/blob/main/config/cdn.yaml) | One origin selector rule per endpoint |
| Handler module | [`src/weather.js`](https://github.com/adobe/aem-edge-functions-boilerplate/blob/main/src/weather.js) | Logic extracted from `index.js` |

## Additional resources

- [Build an API endpoint with Edge Functions](./build-api-endpoint.md)
- [Set up AEM Edge Functions on AEM as a Cloud Service](../setup-aemcs.md)
- [Set up AEM Edge Functions on Edge Delivery Services](../setup-eds.md)
- [AEM Edge Functions product documentation](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/edge-functions)
- [AEM Edge Functions boilerplate](https://github.com/adobe/aem-edge-functions-boilerplate)
