---
title: AEM Headless Web Component deployments
description: Learn about deployment considerations for Web Component/pure JS-based AEM Headless deployments.
version: Experience Manager as a Cloud Service
feature: GraphQL API
topic: Headless, Content Management
role: Developer
level: Intermediate
jira: KT-10797
thumbnail: kt-10797.jpg
exl-id: 9d4aab4c-82af-4917-8c1b-3935f19691e6
duration: 31
TQID: https://experienceleague.adobe.com/F2OY7IC-mwOsX5SEtpw404PSciUEN8meILdY1L-ne-s
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
# AEM Headless Web Component deployments

AEM Headless [Web Component](https://developer.mozilla.org/en-US/docs/Web/Web_Components)/JS deployments are pure JavaScript apps that run in a web browser, that consume and interact with content in AEM in a headless manner. Web Component/JS deployments differ from [SPA deployments](./spa.md) in that they don't use a robust SPA framework, and are expected to be embedded in the context of any website, deliver, to surface content from AEM.


## Deployment configurations

The following deployment configuration must be in-place for Web Component/JS deployments.

| Web Component/JS app connects to →            | AEM Author | AEM Publish | AEM Preview |
|---------------------------------------------------:|:----------:|:-----------:|:-----------:|
| [Dispatcher filters](./configurations/dispatcher-filters.md)      | &#10008;   | &#10004;    | &#10004;    |
| [Cross-origin resource sharing (CORS)](./configurations/cors.md)  | &#10004;   | &#10004;    | &#10004;    |
| [AEM hosts](./configurations/aem-hosts.md)                         | &#10004;   | &#10004;    | &#10004;    |

## Example Web Component

Adobe provides an example Web Component.

<div class="columns is-multiline">
    <!-- Web Component -->
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Web Component" tabindex="0">
       <div class="card">
           <div class="card-image">
               <figure class="image is-16by9">
                   <a href="../example-apps/web-component.md" title="Web Component" tabindex="-1">
                       <img class="is-bordered-r-small" src="../example-apps/assets/web-component/web-component-card.png" alt="Web Component">
                   </a>
               </figure>
           </div>
           <div class="card-content is-padded-small">
               <div class="content">
                   <p class="headline is-size-6 has-text-weight-bold"><a href="../example-apps/web-component.md" title="Web Component">Web Component</a></p>
                   <p class="is-size-6">An example Web Component, written in pure JavaScript, that consumes content from AEM Headless GraphQL APIs.</p>
                   <a href="../example-apps/web-component.md" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM">
                       <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">View example</span>
                   </a>
               </div>
           </div>
       </div>
    </div>
</div>
