---
title: HTTP request filters with Edge Functions
description: Learn how to implement an HTTP request filter that lets you rewrite or redirect requests, or modify HTTP responses.
version: Experience Manager as a Cloud Service
feature: Developing
topic: Development, Architecture
role: Developer
level: Intermediate
doc-type: Article
jira: KT-22059
thumbnail: KT-22059.jpeg
last-substantial-update: 2026-07-15
---
# HTTP request filters with Edge Functions

>[!IMPORTANT]
>
>AEM Edge Functions is currently in beta. Features and documentation may change. For feedback, contact [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com).

Learn how to implement HTTP request filtering with AEM Edge Functions to rewrite or redirect requests, or modify HTTP responses.

## When to filter HTTP requests with Edge Functions

An AEM Edge Function can act as a reverse proxy that performs advanced processing on the request and response before they reach the origin or client.

The two scenarios are:

### Adjust the request before it reaches the origin

Intercept traffic on the way to the origin to:

- **Rewrite the request origin, path, or query.** Route the request to a different backend, path, or query string so the origin receives the correct resource.
- **Rewrite request headers.** Add, remove, or modify headers before the request reaches the origin. For example, add a geo or access header the origin expects, remove headers the origin ignores, or change a header value to alter request behavior.

### Modify the response before it reaches the client

Intercept traffic on the way back to the visitor to:

- **Change the response HTML.** Inject JavaScript, personalized content, rewrite links, or stitch in a header and footer before the page reaches the browser.
- **Redirect at the edge.** Serve a large set of legacy-to-new URL redirects from the CDN, especially when the redirect rules require programmatic logic.
- **Personalize by request context.** Vary a page or section of a page by geolocation, device, or audience for public visitors. This applies to publish traffic on your site domain, not to author traffic.


## Implement HTTP request filtering

HTTP request filtering uses two files. `config/cdn.yaml` decides which traffic to intercept and route to your AEM Edge Function. `src/index.js` performs the request or response adjustment.

The origin selector and the function name must align. If `edgeFunctions.yaml` declares `my-edge-function`, the origin selector uses `edgefunction-my-edge-function` in `cdn.yaml`.

### Configure the CDN filter

```yaml
# config/cdn.yaml (origin selector excerpt)
kind: "CDN"
version: "1"
data:
  originSelectors:
    rules:
      - name: route-to-edge-function
        when:
          allOf:
            - { reqProperty: tier, equals: "publish" } # publish traffic only; skip author
            - { reqProperty: domain, equals: "www.example.com" } # your site hostname
            - { reqProperty: originalPath, matches: "(/[^./]+|\\.html|/)$" } # page URLs; skip static assets (.css, .js, images, fonts)
            # - { reqProperty: method, in: ["GET", "HEAD"] } # optional: navigation only; skip POST, PUT, and other methods with bodies
            - { reqHeader: x-edgefunction-request, exists: false } # skip loopback requests to prevent infinite loops
        action:
          type: selectAemOrigin
          originName: edgefunction-my-edge-function # edgefunction-<name-of-the-function>
```

If any condition fails, the request never reaches your AEM Edge Function. Start with the fewest conditions your function needs and add more only to make routing more precise. For all supported properties and operators, see [Origin selectors](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn-configuring-traffic#origin-selectors).

### Implement the handler

Every AEM Edge Function registers a fetch event handler. Use the handler to adjust the request before it reaches the origin, modify the response before it reaches the client, or both.

The following code snippet demonstrates request filtering and response modification in an AEM Edge Function.

```js
// src/index.js
addEventListener("fetch", (event) => event.respondWith(handleRequest(event)));

async function handleRequest(event) {
  const req = event.request;
  const url = new URL(req.url);

  try {
    // ------------------------------------------------------------
    // --- Request filtering: adjust before origin ---
    // ------------------------------------------------------------

    // Example: Rewrite origin, path, or query
    // Replace origin based on some criteria such as path or query
    const newOriginRequest = new Request(`https://origin.example.com${url.pathname}${url.search}`);
    const newOriginResponse = await fetch(newOriginRequest);
    // Return the new origin response
    return newOriginResponse;

    ...

    // Example: Rewrite request headers before reaching the origin
    const originRequest = new Request(req, {
      headers: new Headers({ ...Object.fromEntries(req.headers), "Authorization": "Bearer <token>" }),
    });
    const originResponse = await fetch(originRequest);
    return originResponse;

    ...

    // ------------------------------------------------------------
    // --- Response filtering: modify before client ---
    // ------------------------------------------------------------

    // Example: Change response HTML (fetch from origin, transform the body)
    const originRequest = new Request(`https://origin.example.com${url.pathname}`);
    const originResponse = await fetch(originRequest);
    const transformedHtml = transformHtml(await originResponse.text());
    return new Response(transformedHtml, { status: 200, headers: originResponse.headers });

    ...

    // Example: Redirect at the edge
    return Response.redirect("https://www.example.com/new-path", 301);

    ...

    // Example: Personalize by request context (geo, device, or audience)
    const originRequest = new Request(`https://origin.example.com${url.pathname}`);
    const originResponse = await fetch(originRequest);
    const personalizedHtml = personalizeHtml(await originResponse.text());
    return new Response(personalizedHtml, { status: 200, headers: originResponse.headers });

    return new Response("Not implemented", { status: 501 });
  } catch (err) {
    console.log(err);
    return new Response("Error", { status: 500 });
  }
}
```

Key points:

| Concept | Detail |
| --- | --- |
| CDN filter | `when` + `allOf` in `cdn.yaml` routes only matching traffic to your AEM Edge Function |
| Request filtering | Build a new `Request` with a different origin, path, query, or headers before `fetch()` to origin |
| Response filtering | Return a new `Response` with transformed HTML, a redirect, or personalized content |
| CDN loopback | Set a sentinel header on internal `fetch()` calls so the CDN routes loopback traffic to origin |

## Design guidelines

- Keep filters as narrow as practical.
- Restrict navigation functions to `GET` and `HEAD`.
- Avoid infinite loops on CDN loopback by setting a sentinel header on internal `fetch()` calls.
- Deploy updated `cdn.yaml` through your Cloud Manager config pipeline.

### Prevent infinite loops on CDN loopback

An infinite loop can occur when an AEM Edge Function fetches content from the origin through the CDN. That fetch re-enters the CDN, matches the same origin selector rule, and routes back into the function.

To prevent this, you can exclude loopback requests from your origin selector rule by setting a sentinel (for example, `x-edgefunction-request`) header. The initial visitor request has no header and reaches the AEM Edge Function. The loopback request carries the header, fails the condition, and routes to origin instead.

The following code and config snippets demonstrate how to prevent infinite loops on CDN loopback.

```js
// src/index.js
addEventListener("fetch", (event) => event.respondWith(handleRequest(event)));
...

// In the handler: set the sentinel on the loopback fetch
const loopbackRequest = new Request(`https://www.example.com${url.pathname}`, {
  headers: { "x-edgefunction-request": "true" },
});
await fetch(loopbackRequest);
```

See [AEM Edge Functions examples](https://github.com/search?q=repo%3Aadobe%2Faem-edge-functions-examples%20x-edgefunction-request&type=code) for how to set the sentinel header in the AEM Edge Function handler.

```yaml
# config/cdn.yaml (origin selector excerpt)
kind: "CDN"
version: "1"
data:
  originSelectors:
    rules:
      - name: route-to-edge-function
        when:
          allOf:
            ...
            - { reqHeader: x-edgefunction-request, exists: false } # skip loopback requests to prevent infinite loops
            ...
```

See [AEM Edge Functions examples](https://github.com/search?q=repo%3Aadobe%2Faem-edge-functions-examples+exists%3A+false&type=code) for how to exclude requests that already carry the sentinel header in the CDN config.

## Complete examples

The [AEM Edge Functions examples](https://github.com/adobe/aem-edge-functions-examples/tree/main/examples) repository includes interceptor functions with full `config/cdn.yaml` rules:

| Example | Repository | What it demonstrates |
| --- | --- | --- |
| AEM as a Cloud Service HTML transformer | [publish-delivery-transformer](https://github.com/adobe/aem-edge-functions-examples/tree/main/examples/publish-delivery-transformer) | Publish page filter for _AEM as a Cloud Service_ sites that injects a JavaScript snippet into the HTML response and prevents CDN loopback |
| Edge Delivery HTML transformer | [edge-delivery-transformer](https://github.com/adobe/aem-edge-functions-examples/tree/main/examples/edge-delivery-transformer) | Publish page filter for _Edge Delivery Services_ sites that injects site header and footer into the HTML response |
| Redirect map lookup | [publish-delivery-redirect-maps](https://github.com/adobe/aem-edge-functions-examples/tree/main/examples/publish-delivery-redirect-maps) | `GET`/`HEAD` page filter that redirects to a legacy URL and prevents CDN loopback |

## Additional resources

- [Build an API endpoint with Edge Functions](./build-api-endpoint.md)
- [Serve multiple endpoints with Edge Functions](./multiple-endpoints.md)
- [Set up AEM Edge Functions on AEM as a Cloud Service](../setup-aemcs.md)
- [Set up AEM Edge Functions on Edge Delivery Services](../setup-eds.md)
- [Origin selectors](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn-configuring-traffic#origin-selectors)
- [AEM Edge Functions product documentation](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/edge-functions)
- [AEM Edge Functions examples](https://github.com/adobe/aem-edge-functions-examples/tree/main/examples)
