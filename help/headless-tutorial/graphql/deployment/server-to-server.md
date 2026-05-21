---
title: AEM Headless server-to-server deployments
description: Learn about deployment considerations for server-to-server AEM Headless deployments.
version: Experience Manager as a Cloud Service
feature: GraphQL API
topic: Headless, Content Management
role: Developer
level: Intermediate
jira: KT-10798
thumbnail: kt-10798.jpg
exl-id: d4ae08d9-dc43-4414-ab75-26853186a301
duration: 48
TQID: https://experienceleague.adobe.com/KEhhvL3mfqF0fV-YzhaCNntAmXjRpQvRMrxHf-m2Lig
product_v2:
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: a01bfd36-4ab8-4bf8-9dc0-5b45b890552e
    internal-label: APIs
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
---
# AEM Headless server-to-server deployments

AEM Headless server-to-server deployments involve server-side applications or processes that consume and interact with content in AEM in a headless manner.

Server-to-server deployments require minimal configuration, as HTTP connections to AEM Headless APIs are not initiated in the context of a browser.

## Deployment configurations

The following deployment configuration must be in-place for server-to-server app deployments.

| Server-to-server app connects to →                             | AEM Author | AEM Publish | AEM Preview |
|---------------------------------------------------------------:|:----------:|:-----------:|:-----------:|
| [Dispatcher filters](./configurations/dispatcher-filters.md)   | &#10008;   | &#10004;    | &#10004;    |
| Cross-origin resource sharing (CORS)                           | &#10008;   | &#10008;    | &#10008;    |
| [AEM hosts](./configurations/aem-hosts.md)                     | &#10004;   | &#10004;    | &#10004;    |

## Authorization requirements

Authorized requests to AEM GraphQL APIs they typically occur in the context of server-to-server apps, since other app types, such as [single-page apps](./spa.md), [mobile](./mobile.md), or [Web Components](./web-component.md), typically do use authorization as it is difficult to secure the credentials . 
 
When authorizing requests to AEM as a Cloud Service, use [service credentials-based token authentication](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis.html). To learn more about authenticating requests to AEM as a Cloud Service, review the [token-based authentication tutorial](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/overview.html). The tutorial explores token-based authentication using [AEM Assets HTTP APIs](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/mac-api-assets.html) but the same concepts and approaches are applicable to apps interacting with AEM Headless GraphQL APIs.

## Example server-to-server app

Adobe provides an example server-to-server app coded in Node.js.

<div class="columns is-multiline">
    <!-- Server-to-server app -->
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Server-to-server app" tabindex="0">
       <div class="card">
           <div class="card-image">
               <figure class="image is-16by9">
                   <a href="../example-apps/server-to-server-app.md" title="Server-to-server app" tabindex="-1">
                       <img class="is-bordered-r-small" src="../example-apps/assets/server-to-server-app/server-to-server-card.png" alt="Server-to-server app">
                   </a>
               </figure>
           </div>
           <div class="card-content is-padded-small">
               <div class="content">
                   <p class="headline is-size-6 has-text-weight-bold"><a href="../example-apps/server-to-server-app.md" title="Server-to-server app">Server-to-server app</a></p>
                   <p class="is-size-6">An example server-to-server app, written in Node.js, that consumes content from AEM Headless GraphQL APIs.</p>
                   <a href="../example-apps/server-to-server-app.md" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM">
                       <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">View example</span>
                   </a>
               </div>
           </div>
       </div>
    </div>
</div>
