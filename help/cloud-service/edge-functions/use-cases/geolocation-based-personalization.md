---
title: Geolocation-based personalization with AEM Edge Functions
description: Learn how to read CDN geo signals at the edge and serve locale-specific content without an origin round trip, improving time-to-first-byte and SEO.
version: Experience Manager as a Cloud Service
feature: Developing
topic: Development, Personalization, Performance
role: Developer
level: Intermediate
doc-type: Tutorial
jira: KT-XXXXX
thumbnail: KT-XXXXX.jpeg
last-substantial-update: 2026-06-12
duration: 0
exl-id: TODO-REPLACE-WITH-GENERATED-EXLID
---
# Geolocation-based personalization with AEM Edge Functions

>[!IMPORTANT]
>
>AEM Edge Functions is currently in beta. Features and documentation may change. For feedback, contact [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com).

TODO - 2–3 sentence intro explaining what this use case builds, why it matters (SEO angle: server-rendered on first crawl vs. JS-on-page approach).

## Overview

TODO - Architecture diagram showing: browser → edge function (reads Fastly-Geo-Country header) → returns localized response.

In this use case you:

1. Read the `Fastly-Geo-Country` header injected by the CDN
1. TODO - Step 2
1. TODO - Step 3
1. Set correct `Vary` and cache headers so personalized responses are cached per country

## Prerequisites

- Completed [Set up AEM Edge Functions](../setup-aemcs.md)
- TODO - Any additional prerequisites

## Step 1: Read geo signals from CDN headers

TODO - Explanation of the `Fastly-Geo-Country` header and other available geo signals.

```javascript
// src/index.js
export default async function handler(request, context) {
  const country = request.headers.get('Fastly-Geo-Country') || 'US';
  // TODO - example logic
}
```

## Step 2: Serve locale-specific content

TODO - Show routing to different AEM content paths or injecting locale-specific data into the response.

```javascript
// TODO - expanded code example
```

## Step 3: Set caching headers for cohort-based personalization

TODO - Explanation of `Vary: Fastly-Geo-Country` and recommended TTL strategy.

```javascript
// TODO - setting response headers example
const response = new Response(body, {
  headers: {
    'Content-Type': 'text/html; charset=utf-8',
    'Vary': 'Fastly-Geo-Country',
    'Cache-Control': 'public, max-age=300',
  },
});
return response;
```

>[!CAUTION]
>
>TODO - Warning about cache key explosion if too many Vary dimensions are combined.

## Test

TODO - How to verify geo routing works locally (override header in curl) and in deployed environment.

```bash
# Test with a simulated country header
curl -H "Fastly-Geo-Country: DE" http://127.0.0.1:7676/your-path
```

## Summary

TODO - 2–3 sentences summarizing what was built and key takeaways (edge over JS-on-page, caching strategy).

## Related

- [Set up AEM Edge Functions](../setup-aemcs.md)
- [API aggregation with secrets](./api-aggregation-with-secrets.md)
- [AEM Edge Functions product documentation](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/edge-functions)
