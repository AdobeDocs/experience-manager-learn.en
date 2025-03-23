---
title: AEM Headless deployments
description: Learn about the various deployment considerations for AEM Headless apps.
version: Experience Manager as a Cloud Service
feature: GraphQL API
topic: Headless, Content Management
role: Developer, Architect
level: Intermediate
jira: KT-10794
thumbnail: kt-10794.jpg
last-substantial-update: 2022-08-26
exl-id: 6de58ca0-9444-4272-9487-15a9e3c89231
duration: 59
---
# AEM Headless deployments

AEM Headless client deployments take many forms; AEM-hosted SPA, external SPA, web site, mobile app, or even server-to-server process. 

Depending on the client and how it is deployed, AEM Headless deployments have different considerations. 

## AEM service architecture

Before exploring deployment considerations, it's imperative to understand AEM's logical architecture, and the separation and roles of AEM as a Cloud Service's service tiers. AEM as a Cloud Service is comprised of two logical services:

+ __AEM Author__ is the service where teams create, collaborate, and publish Content Fragments (and other assets).
+ __AEM Publish__ is the service that were published Content Fragments (and other assets) are replicated for general consumption.
+ __AEM Preview__ is the service that mimics AEM Publish in behavior, but has content published to it for preview or review purposes. AEM Preview is intended for internal audiences, and not for the general delivery of content. The use of AEM Preview is optional, based on the desired workflow.

![AEM service architecture](./assets/overview/aem-service-architecture.png)

Typical AEM as a Cloud Service headless deployment architecture_

AEM Headless clients operating in a production capacity typically interact with AEM Publish, which contains the approved, published content. Clients interacting with AEM Author need to take special care, as AEM Author is secure by default, requiring authorization for all requests, and may also contain work in progress, or unapproved content.

## Headless client deployments

<div class="columns is-multiline">
    <!-- Single-page App (SPA) -->
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Single-page App (SPA)" tabindex="0">
       <div class="card">
           <div class="card-image">
               <figure class="image is-16by9">
                   <a href="./spa.md" title="Single-page App (SPA)" tabindex="-1">
                       <img class="is-bordered-r-small" src="./assets/spa/spa-card.png" alt="Single-page apps (SPA)">
                   </a>
               </figure>
           </div>
           <div class="card-content is-padded-small">
               <div class="content">
                   <p class="headline is-size-6 has-text-weight-bold"><a href="./spa.md" title="Single-page App (SPA)">Single-page app (SPA)</a></p>
                   <p class="is-size-6">Learn about deployment considerations for single-page apps (SPA).</p>
                   <a href="./spa.md" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM">
                       <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Learn</span>
                   </a>
               </div>
           </div>
       </div>
    </div>
<!-- Web component/JS -->
<div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Web component/JS" tabindex="0">
   <div class="card">
       <div class="card-image">
           <figure class="image is-16by9">
               <a href="./web-component.md" title="Web component/JS" tabindex="-1">
                   <img class="is-bordered-r-small" src="./assets/web-component/web-component-card.png" alt="Web component/JS">
               </a>
           </figure>
       </div>
       <div class="card-content is-padded-small">
           <div class="content">
               <p class="headline is-size-6 has-text-weight-bold"><a href="./web-component.md" title="Web component/JS">Web component/JS</a></p>
               <p class="is-size-6">Learn about deployment considerations for web components and browser-based JavaScript headless consumers.</p>
               <a href="./web-component.md" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM">
                   <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Learn</span>
               </a>
           </div>
       </div>
   </div>
</div>
<!-- Mobile apps -->
<div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Mobile apps" tabindex="0">
   <div class="card">
       <div class="card-image">
           <figure class="image is-16by9">
               <a href="./mobile.md" title="Mobile apps" tabindex="-1">
                   <img class="is-bordered-r-small" src="./assets/mobile/mobile-card.png" alt="Mobile apps">
               </a>
           </figure>
       </div>
       <div class="card-content is-padded-small">
           <div class="content">
               <p class="headline is-size-6 has-text-weight-bold"><a href="./mobile.md" title="Mobile apps">Mobile app</a></p>
               <p class="is-size-6">Learn about deployment considerations for mobile apps.</p>
               <a href="./mobile.md" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM">
                   <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Learn</span>
               </a>
           </div>
       </div>
   </div>
</div>
<!-- Server-to-server apps -->
<div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Server-to-server apps" tabindex="0">
   <div class="card">
       <div class="card-image">
           <figure class="image is-16by9">
               <a href="./server-to-server.md" title="Server-to-server apps" tabindex="-1">
                   <img class="is-bordered-r-small" src="./assets/server-to-server/server-to-server-card.png" alt="Server-to-server apps">
               </a>
           </figure>
       </div>
       <div class="card-content is-padded-small">
           <div class="content">
               <p class="headline is-size-6 has-text-weight-bold"><a href="./server-to-server.md" title="Server-to-server apps">Server-to-server app</a></p>
               <p class="is-size-6">Learn about deployment considerations for server-to-server apps</p>
               <a href="./server-to-server.md" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM">
                   <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Learn</span>
               </a>
           </div>
       </div>
   </div>
</div>
</div>
