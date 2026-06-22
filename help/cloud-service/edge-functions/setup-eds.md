---
title: Set up AEM Edge Functions with Edge Delivery Services
description: Learn how to install the Adobe CLI, configure your first edge function service, route CDN traffic to it, and verify it works locally, for Edge Delivery Services environments.
version: Experience Manager as a Cloud Service
feature: Developing, Edge Delivery Services
topic: Development, Architecture
role: Developer
level: Intermediate
doc-type: Technical Video
jira: KT-XXXXX
thumbnail: KT-XXXXX.jpeg
last-substantial-update: 2026-06-12
duration: 0
exl-id: TODO-REPLACE-WITH-GENERATED-EXLID
---
# Set up AEM Edge Functions with Edge Delivery Services

>[!IMPORTANT]
>
>AEM Edge Functions is currently in beta. Features and documentation may change. For feedback, contact [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com).

This page walks through getting your first edge function deployed on Edge Delivery Services, from CLI installation to a live endpoint. The same setup is the foundation for every use case in this tutorial.

The high-level steps:

1. Install the Adobe CLI and edge functions plugin
1. Initialize and clone the boilerplate
1. Declare the edge function service (`edgeFunctions.yaml`)
1. Route CDN traffic to it (`cdn.yaml`)
1. Deploy the configuration
1. Build and deploy the function code
1. Verify locally with the dev server

## Prerequisites

Ensure the following are in place before starting.

- Access to an Edge Delivery Services site with a connected Cloud Manager program
- **Cloud Manager** Deployment Manager role
- TODO - Any additional EDS-specific prerequisites
- [Node.js](https://nodejs.org/) and npm installed locally

>[!NOTE]
>
>Edge Delivery Services supports up to **three edge functions per program**, compared to one for AEM as a Cloud Service Java-stack environments.

## Step 1: Install the Adobe CLI

Install the `aio` CLI and the edge functions plugin:

```bash
npm install -g @adobe/aio-cli
aio plugins install @adobe/aio-cli-plugin-aem-edge-functions
```

Authenticate and initialize:

```bash
aio login
aio aem edge-functions setup
```

The `setup` command clones the `aem-edge-functions-boilerplate` and prompts for your program and environment IDs.

![TODO - screenshot: aio setup output for EDS](./assets/setup/setup-eds.png)

## Step 2: Explore the boilerplate

Install dependencies in the cloned boilerplate directory:

```bash
npm install
```

The boilerplate provides:

| File / Directory | Purpose |
| --- | --- |
| `src/index.js` | Entry point for your edge function logic |
| `config/edgeFunctions.yaml` | Declares the service name, configs, secrets, and KV toggle |
| `config/cdn.yaml` | CDN routing rules that direct traffic to the edge function |
| `test/` | Mocha unit tests |

## Step 3: Declare your edge function service

Open (or create) `config/edgeFunctions.yaml` and declare a service:

```yaml
kind: "EdgeFunctions"
version: "1"
data:
  services:
    - name: my-edge-function
```

The `name` value is the identifier used in CDN rules and in deploy commands. It must be unique within the program. You can declare up to three services for an EDS program.

>[!NOTE]
>
>You can optionally add `configs`, `secrets`, and `kvs` blocks to this file. These are covered in the use case pages.

## Step 4: Route CDN traffic to the edge function

Add an origin selector rule to `config/cdn.yaml`:

```yaml
kind: 'CDN'
version: '1'
data:
  originSelectors:
    rules:
      - name: route-to-my-edge-function
        when: { reqProperty: path, equals: "/edge-hello" }
        action:
          type: selectAemOrigin
          originName: edgefunction-my-edge-function
```

The `originName` must follow the pattern `edgefunction-<service-name>`. Multiple rules can target the same function.

>[!NOTE]
>
>TODO - Confirm if EDS uses a different `cdn.yaml` structure or origin type than Java-stack AEM as a Cloud Service.

## Step 5: Deploy the configuration

TODO - Confirm the EDS-specific config deployment mechanism. For AEM as a Cloud Service, a Cloud Manager config pipeline is used. Verify whether EDS uses the same pipeline type or a different deployment path.

```bash
# TODO - EDS config deployment command or Cloud Manager pipeline steps
```

![TODO - screenshot: EDS config deployment](./assets/setup/setup-eds.png)

## Step 6: Build and deploy the function code

```bash
aio aem edge-functions build
aio aem edge-functions deploy my-edge-function
```

The function name must match the `name` value in `edgeFunctions.yaml`.

After a successful deploy, the endpoint is reachable at:

```
TODO - EDS endpoint format (e.g., <site>.hlx.live/edge-hello or custom domain)
```

## Step 7: Verify locally

Run the development server:

```bash
aio aem edge-functions serve
```

The server starts at `http://127.0.0.1:7676`. Requests to `http://127.0.0.1:7676/edge-hello` are handled by your local function code.

To stream logs from the deployed function:

```bash
aio aem edge-functions tail-logs my-edge-function
```

To run unit tests:

```bash
npm run test
```

## Next steps

With your edge function deployed and routing confirmed, proceed to the use cases:

<!-- 
CARDS
{target = _self}

* ./use-cases/geolocation-based-personalization.md
  {title = Geolocation-based personalization}
  {description = Serve locale-specific content at the edge using CDN geo signals.}
  {image = ./assets/use-cases/use-case.png}
  {cta = Learn more}
* ./use-cases/api-aggregation-with-secrets.md
  {title = API aggregation with secrets}
  {description = Fan out to multiple backends using server-side secrets and return a combined response.}
  {image = ./assets/use-cases/use-case.png}
  {cta = Learn more}
* ./use-cases/kv-store-feature-flags.md
  {title = Feature flags with KV store}
  {description = Toggle feature flags at the edge using the runtime KV store.}
  {image = ./assets/use-cases/use-case.png}
  {cta = Learn more}
-->
<!-- START CARDS HTML - DO NOT MODIFY BY HAND -->
<div class="columns">
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Geolocation-based personalization">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="./use-cases/geolocation-based-personalization.md" title="Geolocation-based personalization" target="_self" rel="referrer">
                        <img class="is-bordered-r-small" src="./assets/use-cases/use-case.png" alt="Geolocation-based personalization"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="./use-cases/geolocation-based-personalization.md" target="_self" rel="referrer" title="Geolocation-based personalization">Geolocation-based personalization</a>
                    </p>
                    <p class="is-size-6">Serve locale-specific content at the edge using CDN geo signals.</p>
                </div>
                <a href="./use-cases/geolocation-based-personalization.md" target="_self" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Learn more</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="API aggregation with secrets">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="./use-cases/api-aggregation-with-secrets.md" title="API aggregation with secrets" target="_self" rel="referrer">
                        <img class="is-bordered-r-small" src="./assets/use-cases/use-case.png" alt="API aggregation with secrets"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="./use-cases/api-aggregation-with-secrets.md" target="_self" rel="referrer" title="API aggregation with secrets">API aggregation with secrets</a>
                    </p>
                    <p class="is-size-6">Fan out to multiple backends using server-side secrets and return a combined response.</p>
                </div>
                <a href="./use-cases/api-aggregation-with-secrets.md" target="_self" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Learn more</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Feature flags with KV store">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="./use-cases/kv-store-feature-flags.md" title="Feature flags with KV store" target="_self" rel="referrer">
                        <img class="is-bordered-r-small" src="./assets/use-cases/use-case.png" alt="Feature flags with KV store"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="./use-cases/kv-store-feature-flags.md" target="_self" rel="referrer" title="Feature flags with KV store">Feature flags with KV store</a>
                    </p>
                    <p class="is-size-6">Toggle feature flags at the edge using the runtime KV store.</p>
                </div>
                <a href="./use-cases/kv-store-feature-flags.md" target="_self" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Learn more</span>
                </a>
            </div>
        </div>
    </div>
</div>
<!-- END CARDS HTML - DO NOT MODIFY BY HAND -->
