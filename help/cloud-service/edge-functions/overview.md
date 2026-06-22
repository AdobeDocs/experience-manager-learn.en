---
title: AEM Edge Functions
description: Learn how AEM Edge Functions enable JavaScript execution at the CDN layer to deliver personalized, low-latency experiences without a round trip to origin.
version: Experience Manager as a Cloud Service
feature: Developing
topic: Development, Architecture, Performance
role: Developer, Architect
level: Intermediate
doc-type: Article
jira: KT-XXXXX
thumbnail: KT-XXXXX.jpeg
last-substantial-update: 2026-06-12
duration: 0
exl-id: TODO-REPLACE-WITH-GENERATED-EXLID
---
# AEM Edge Functions

![AEM Edge Functions](./assets/hero.png)

>[!IMPORTANT]
>
>AEM Edge Functions is currently in beta. Features and documentation may change. For feedback, contact [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com).

## JavaScript at the CDN layer

AEM Edge Functions are JavaScript modules deployed to and executed on Adobe's CDN (powered by Fastly Compute). When a request matches a CDN routing rule, the edge function intercepts it, reads headers, calls backends, transforms responses, and returns the result directly from the edge, without a round trip to origin. This unlocks fast, server-rendered personalization, secure API proxying, and response aggregation, all while benefiting from CDN-level caching.

Edge Functions work with both AEM as a Cloud Service (Java-stack) and Edge Delivery Services environments.

## Key benefits

Edge Functions address four common challenges when building dynamic, CDN-delivered experiences.

| Benefit | Description |
| --- | --- |
| **Performance** | Edge-side execution means lower time-to-first-byte; no origin round trip for common patterns |
| **SEO** | Server-rendered HTML is delivered on first crawl, making it friendly to search engines and AI crawlers |
| **Security** | API credentials and secrets remain server-side; never exposed in client JavaScript |
| **Personalization** | Content can be customized by geo, device, or audience before the page loads |

## Architecture

An edge function sits between the CDN cache and your backends, processing each request before it reaches origin.

```
Browser → CDN Cache → Edge Function → Fetch Cache → Backend (AEM / external API)
```

Two independent cache layers exist: the **CDN cache** (what the browser sees) and the **fetch cache** (what the edge function sees when calling backends). Both require independent invalidation when underlying data changes.

## When to use Edge Functions

Use the following as a guide when deciding between Edge Functions and other AEM extensibility approaches.

| Scenario | Recommended approach |
| --- | --- |
| Run custom logic, call external APIs, personalize responses | **Edge Functions** |
| Complex business logic with full AEM context | OSGi service / Sling servlet at origin |

## Get started

Choose your environment to follow the step-by-step setup guide.

<!-- 
CARDS
{target = _self}

* ./setup-aemcs.md
  {title = Set up with AEM as a Cloud Service}
  {description = Configure and deploy your first edge function on an AEM as a Cloud Service environment using the config pipeline or RDE.}
  {image = ./assets/setup/setup-cs.png}
  {cta = Set up}
* ./setup-eds.md
  {title = Set up with Edge Delivery Services}
  {description = Configure and deploy your first edge function on an Edge Delivery Services environment.}
  {image = ./assets/setup/setup-eds.png}
  {cta = Set up}
-->
<!-- START CARDS HTML - DO NOT MODIFY BY HAND -->
<div class="columns">
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Set up with AEM as a Cloud Service">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="./setup-aemcs.md" title="Set up with AEM as a Cloud Service" target="_self" rel="referrer">
                        <img class="is-bordered-r-small" src="./assets/setup/setup-cs.png" alt="Set up with AEM as a Cloud Service"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="./setup-aemcs.md" target="_self" rel="referrer" title="Set up with AEM as a Cloud Service">Set up with AEM as a Cloud Service</a>
                    </p>
                    <p class="is-size-6">Configure and deploy your first edge function on an AEM as a Cloud Service environment using the config pipeline or RDE.</p>
                </div>
                <a href="./setup-aemcs.md" target="_self" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Set up</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Set up with Edge Delivery Services">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="./setup-eds.md" title="Set up with Edge Delivery Services" target="_self" rel="referrer">
                        <img class="is-bordered-r-small" src="./assets/setup/setup-eds.png" alt="Set up with Edge Delivery Services"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="./setup-eds.md" target="_self" rel="referrer" title="Set up with Edge Delivery Services">Set up with Edge Delivery Services</a>
                    </p>
                    <p class="is-size-6">Configure and deploy your first edge function on an Edge Delivery Services environment.</p>
                </div>
                <a href="./setup-eds.md" target="_self" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Set up</span>
                </a>
            </div>
        </div>
    </div>
</div>
<!-- END CARDS HTML - DO NOT MODIFY BY HAND -->

## Use cases

Each use case builds on the setup above and demonstrates a practical, adaptable pattern.

<!-- 
CARDS
{target = _self}

* ./use-cases/geolocation-based-personalization.md
  {title = Geolocation-based personalization}
  {description = Serve locale-specific content at the edge using CDN geo signals, with no origin round trip.}
  {image = ./assets/use-cases/use-case.png}
  {cta = Learn more}
* ./use-cases/api-aggregation-with-secrets.md
  {title = API aggregation with secrets}
  {description = Fan out to multiple backend APIs using server-side secrets and return a single aggregated response.}
  {image = ./assets/use-cases/use-case.png}
  {cta = Learn more}
* ./use-cases/kv-store-feature-flags.md
  {title = Feature flags with KV store}
  {description = Use the edge KV store to toggle feature flags and conditionally serve content variants.}
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
                    <p class="is-size-6">Serve locale-specific content at the edge using CDN geo signals, with no origin round trip.</p>
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
                    <p class="is-size-6">Fan out to multiple backend APIs using server-side secrets and return a single aggregated response.</p>
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
                    <p class="is-size-6">Use the edge KV store to toggle feature flags and conditionally serve content variants.</p>
                </div>
                <a href="./use-cases/kv-store-feature-flags.md" target="_self" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Learn more</span>
                </a>
            </div>
        </div>
    </div>
</div>
<!-- END CARDS HTML - DO NOT MODIFY BY HAND -->

## Limitations

Keep the following platform limits in mind when designing your edge function logic.

| Limit | Value |
| --- | --- |
| Max outbound fetch calls per invocation | 32 |
| Max edge functions per program (AEM as a Cloud Service) | 1 |
| Max edge functions per program (Edge Delivery Services) | 3 |
| Config/Secret/KV stores in sandbox programs | Not available |
| KV store name | `kv_default` (fixed) |
| Config store name | `config_default` (fixed) |
| Secret store name | `secret_default` (fixed) |

## Additional resources

- [AEM Edge Functions product documentation](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/edge-functions)
- [Traffic Filter and WAF Rules](../security/traffic-filter-and-waf-rules/overview.md)
- [CDN configuration in AEM as a Cloud Service](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn-configuring-traffic)
