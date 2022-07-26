---
title: Deploying SPA for AEM GraphQL
description: Learn SPA deployment options in regards to AEM GraphQL, Headless.
version: Cloud Service
feature: GraphQL API
topic: Headless, Content Management
role: Developer, Architect
level: Intermediate
kt: 10587
thumbnail: KT-10587.jpg
mini-toc-levels: 2
---


# Deploying a SPA

In this section, we will review an approach for deploying SPA (React, Vue, Angular, etc) that invokes AEM's GraphQL APIs to load the data, however, before that let's understand the high-level artifacts that one has to deploy.

**SPA Build App Artifacts:** 

The files produced by the SPA framework, typically **HTML, CSS, JS**, aka static build artifacts. In the case of React app, the  artifacts from the `build` directory and for Vue artifacts from the `dist` directory. 
The request to your SPA (e.g. https://HOST/my-aem-spa.html) will be served using these build artifacts.

**AEM's GraphQL APIs:**

Clearly, this GraphQL API endpoint (`/graphql/execute.json/<PROJECT-CONFIG>/<PERSISTED-QUERY-NAME>`) has to be hosted on the AEM domain.

In summary SPA deployment architecture has two parts *1. SPA  2. AEM GraphQL API Layer*, so let's review the deployment options for these two parts.

## Deployment Options

| Deployment Option | SPA URL | AEM GraphQL API URL | CORS Config Required? |
| ---------|---------- | ---------|---------- |
| **Same Domain** | https://**HOST**/my-aem-spa.html | https://**HOST**/graphql/execute.json/... | &#10008; |
| **Different Domain** | https://**SPA-HOST**/my-aem-spa.html | https://**AEM-HOST**/graphql/execute.json/... | &#10004; |

**Same Domain:**            
    Both *SPA & AEM GraphQL API Layer* in this option are deployed to the **Same Domain**. Meaning request to SPA URI `/my-aem-spa.html` & GraphQL API layer `/graphql/execute.json/` are served from exact same domain.

**Different Domain:**               
    Both *SPA & AEM GraphQL API Layer* in this option are deployed to **Different Domain**. Meaning request to SPA URI `/my-aem-spa.html` is served from a **different domain** than GraphQL API layer `/graphql/execute.json/` requests. Please note as part of this deployment option, you need to configure CORS on the AEM instance, see details here.

>[!NOTE]
>
>You MUST properly configure CORS on AEM instance, see.

**TODO: Link to DG's CORS**

### Deploying on Same Domain

When deploying on the Same Domain, the domain could be a **primary AEM domain** (On AEM Domain) or **primary SPA domain** (Off AEM Domain), and incoming SPA, AEM GraphQL API requests can be split at any one of the deployment components such as CDN ([Fastly](https://docs.fastly.com/en/guides/routing-assets-to-different-origins), Akamai, [CloudFront](https://aws.amazon.com/premiumsupport/knowledge-center/cloudfront-distribution-serve-content/)), [HTTPD w/ Reverse Proxy](https://httpd.apache.org/docs/2.4/howto/reverse_proxy.html). In other words, you still deploy the SPA build artifacts and AEM GraphQL APIs to different servers but for end users, those are delivered from a single domain and behind the scene routed to a different destination or origin servers.

Also, SPA build artifacts can be hosted in AEM *but are not recommended.* 

| Same Domain Deployment | CDN Split | HTTPD + Reverse Proxy | AEM Hosted SPA Artifacts |
| ---------|---------- | ---------|---------- |
| **ON AEM Domain** | &#10004; | &#10004; | &#10004; |
| **OFF AEM Domain** | &#10004; | &#10004; | **N/A** |

### Deploying on Different Domain

In this scenario, SPA build artifacts are deployed to a different domain than the AEM GraphQL APIs domain and for end users, they will be delivered from two separate domains thus CORS configuration is MUST on AEM, see details here.

**TODO: Add a Screenshot**


