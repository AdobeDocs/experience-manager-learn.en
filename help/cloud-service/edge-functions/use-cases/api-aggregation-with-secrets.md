---
title: API aggregation with secrets using AEM Edge Functions
description: Learn how to fan out to multiple backend APIs using server-side secrets stored in Cloud Manager, and return a single aggregated response, keeping credentials out of client JavaScript.
version: Experience Manager as a Cloud Service
feature: Developing
topic: Development, Security, Architecture
role: Developer
level: Intermediate
doc-type: Tutorial
jira: KT-XXXXX
thumbnail: KT-XXXXX.jpeg
last-substantial-update: 2026-06-12
duration: 0
exl-id: TODO-REPLACE-WITH-GENERATED-EXLID
---
# API aggregation with secrets using AEM Edge Functions

>[!IMPORTANT]
>
>AEM Edge Functions is currently in beta. Features and documentation may change. For feedback, contact [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com).

TODO - Intro: what problem does API key exposure in client JS cause, and how edge functions solve it by keeping secrets server-side. What the reader builds in this tutorial.

## Overview

TODO - Architecture diagram: browser → edge function → (parallel) AEM API + external API → aggregated JSON response.

In this use case you:

1. Store an API token as a Cloud Manager environment secret
1. Reference the secret in `edgeFunctions.yaml`
1. Access it in function code via `SecretStoreManager`
1. Fan out to two backend APIs in parallel
1. Return a single aggregated JSON response

>[!NOTE]
>
>The max outbound fetch calls per edge function invocation is **32**. For aggregation patterns that approach this limit, consider batching or splitting across multiple requests.

## Prerequisites

- Completed [Set up AEM Edge Functions](../setup-aemcs.md)
- A Cloud Manager environment secret (see [Manage environment variables in Cloud Manager](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/environment-variables))
- TODO - Any additional prerequisites

## Step 1: Add a secret to Cloud Manager

TODO - Screenshots and steps for adding an environment secret in Cloud Manager.

![TODO - screenshot: add environment secret in Cloud Manager](../assets/use-cases/TODO-cloud-manager-secret.png)

## Step 2: Reference the secret in `edgeFunctions.yaml`

Add a `secrets` block to your service declaration:

```yaml
kind: "EdgeFunctions"
version: "1"
data:
  services:
    - name: my-edge-function
      secrets:
        - key: API_TOKEN
          value: ${{ API_TOKEN_SECRET }}
```

The `${{ API_TOKEN_SECRET }}` syntax references the Cloud Manager secret by name.

>[!CAUTION]
>
>Secret store is **not available in sandbox programs**. Use a dev or stage environment to test this use case.

## Step 3: Read the secret in function code

TODO - Import and usage of `SecretStoreManager`.

```javascript
// src/index.js
import { SecretStoreManager } from "./lib/config";

export default async function handler(request, context) {
  const apiToken = await SecretStoreManager.getSecret('API_TOKEN');
  // TODO - use token in fetch calls
}
```

## Step 4: Fan out to multiple backends in parallel

TODO - Show `Promise.all()` pattern for parallel fetch calls.

```javascript
// TODO - parallel fetch example
const [aemResponse, externalResponse] = await Promise.all([
  fetch('https://publish-pXXXXX-eYYYYY.adobeaemcloud.com/api/content', {
    headers: { Authorization: `Bearer ${apiToken}` },
  }),
  fetch('https://api.example.com/data', {
    headers: { 'x-api-key': apiToken },
  }),
]);
```

## Step 5: Aggregate and return the response

TODO - Combine the two responses into a single JSON payload.

```javascript
// TODO - aggregation and response example
const aggregated = {
  content: await aemResponse.json(),
  external: await externalResponse.json(),
};

return new Response(JSON.stringify(aggregated), {
  headers: { 'Content-Type': 'application/json' },
});
```

## Test

TODO - How to verify the aggregated response locally and confirm the secret is not exposed in the response.

```bash
curl http://127.0.0.1:7676/your-aggregation-path | jq .
```

## Summary

TODO - Key takeaways: credentials stay server-side, single request to browser, parallel backend calls for performance.

## Related

- [Set up AEM Edge Functions](../setup-aemcs.md)
- [Geolocation-based personalization](./geolocation-based-personalization.md)
- [Feature flags with KV store](./kv-store-feature-flags.md)
- [AEM Edge Functions product documentation](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/edge-functions)
