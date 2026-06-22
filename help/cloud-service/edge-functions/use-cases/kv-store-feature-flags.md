---
title: Feature flags with KV store using AEM Edge Functions
description: Learn how to use the edge KV store to manage feature flags at the CDN layer, enabling instant content variant toggling without redeployment.
version: Experience Manager as a Cloud Service
feature: Developing
topic: Development, Architecture
role: Developer
level: Intermediate
doc-type: Tutorial
jira: KT-XXXXX
thumbnail: KT-XXXXX.jpeg
last-substantial-update: 2026-06-12
duration: 0
exl-id: TODO-REPLACE-WITH-GENERATED-EXLID
---
# Feature flags with KV store using AEM Edge Functions

>[!IMPORTANT]
>
>AEM Edge Functions is currently in beta. Features and documentation may change. For feedback, contact [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com).

TODO - Intro: what problem feature flags solve (deploy code vs. toggle behavior), why doing it at the edge is fast, what this tutorial builds.

## Overview

TODO - Architecture diagram: flag written to KV store (admin/script) → edge function reads flag → conditionally serves variant A or B.

In this use case you:

1. Enable the KV store for your edge function service
1. Write a feature flag value into the KV store
1. Read the flag in function code and conditionally serve content
1. Toggle the flag without redeploying code

>[!NOTE]
>
>The KV store (`kv_default`) is **not available in sandbox programs**. Use a dev or stage environment to test this use case.

## Prerequisites

- Completed [Set up AEM Edge Functions](../setup-aemcs.md)
- TODO - Any additional prerequisites

## Step 1: Enable KV store in `edgeFunctions.yaml`

Add `kvs: true` to your service declaration:

```yaml
kind: "EdgeFunctions"
version: "1"
data:
  services:
    - name: my-edge-function
      kvs: true
```

Redeploy the config after this change (pipeline or `aio aem rde:install`).

## Step 2: Write a feature flag to the KV store

TODO - Explain how to write to the KV store (CLI tool, script, or admin interface; confirm which is available in beta).

```bash
# TODO - command or script to write a flag value
# aio aem edge-functions kv put my-edge-function feature-new-header true
```

## Step 3: Read the flag in function code

```javascript
// src/index.js
import { KVStore } from "fastly:kv-store";

export default async function handler(request, context) {
  const kv = new KVStore('kv_default');
  const entry = await kv.get('feature-new-header');
  const isEnabled = entry ? (await entry.text()) === 'true' : false;

  // TODO - use isEnabled to conditionally serve content
}
```

## Step 4: Conditionally serve content variants

TODO - Show serving variant A vs variant B based on the flag value.

```javascript
// TODO - conditional response example
if (isEnabled) {
  // serve variant with new feature
  return new Response(/* ... */);
} else {
  // serve default
  return fetch(request);
}
```

## Step 5: Toggle the flag without redeployment

TODO - Show updating the KV entry to flip the flag, and confirm the change takes effect on the next request with no code redeploy.

```bash
# TODO - update command
```

>[!TIP]
>
>Combine this pattern with a simple admin UI (a small script or Cloud Manager environment variable) to give non-developers control over feature rollout.

## Test

TODO - How to verify both states (flag on / flag off) locally and in deployed environment.

```bash
# Test flag-off state
curl http://127.0.0.1:7676/your-path

# Write flag, then re-test
# TODO - write command
curl http://127.0.0.1:7676/your-path
```

## Summary

TODO - Key takeaways: KV store enables runtime control without redeployment, edge-layer toggling means zero origin impact.

## Related

- [Set up AEM Edge Functions](../setup-aemcs.md)
- [Geolocation-based personalization](./geolocation-based-personalization.md)
- [API aggregation with secrets](./api-aggregation-with-secrets.md)
- [AEM Edge Functions product documentation](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/edge-functions)
