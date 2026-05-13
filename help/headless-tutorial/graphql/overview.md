---
title: Get started with AEM Headless - GraphQL
description: Learn about the Experience Manager GraphQL APIs and their capabilities.
feature: Content Fragments, GraphQL API, APIs
topic: Headless, Content Management
role: Developer
level: Beginner
exl-id: 0056971f-2f89-43b3-bb6f-dd16c2a50370
thumbnail: 328618.jpg
last-substantial-update: 2022-07-20T00:00:00.000Z
duration: 626
TQID: https://experienceleague.adobe.com/HVveHOVqQ0nfmAXDID-BlVpi-0QNNxFbtIooUfPQpWo
product_v2:
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: a01bfd36-4ab8-4bf8-9dc0-5b45b890552e
    internal-label: APIs
  - id: a453562e-8e72-4640-9a69-9cf95930bcee
    internal-label: Universal Editor
  - id: c124fa01-25c5-42ec-adf6-21d1c114058b
    internal-label: Developer tools
  - id: e2c1b6d3-bb7e-4fe8-8c72-f7b403298e91
    internal-label: Authoring
  - id: f2d27a5f-0d67-4d85-8a24-86a8d8a3574b
    internal-label: Developer tools
subfeature_v2:
  - id: df6f8f89-5d09-489b-b250-e48ea4b6c168
    internal-label: Mobile
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
---
# Getting Started with AEM Headless - GraphQL {#getting-started-with-aem-headless}

AEM's GraphQL APIs for Content Fragments
supports headless CMS scenarios where external client applications render experiences using content managed in AEM.

A modern content delivery API is key for efficiency and performance of Javascript-based frontend applications. Using a REST API introduce challenges:  

* Large number of requests for fetching one object at a time
* Often "over-delivering" content, meaning the application receives more than it needs

To overcome these challenges GraphQL provides a query-based API allowing clients to query AEM for only the content it needs, and to receive using a single API call.

>[!VIDEO](https://video.tv.adobe.com/v/328618?quality=12&learn=on)

This video is an overview of the GraphQL API implemented in AEM. The GraphQL API in AEM is primarily designed to deliver AEM Content Fragment's to downstream applications as part of a headless deployment.

>[!CONTEXTUALHELP]
>id="aemcloud_learn_headless_graphql_overview"
>title="Getting Started with AEM Headless - GraphQL"
>abstract="Learn how to deliver Content Fragments using GraphQL."
>additional-url="https://video.tv.adobe.com/v/328618" text="Overview of GraphQL in AEM"

## AEM Headless GraphQL Video Series

Learn about AEM's GraphQL capabilities through the in-depth walk-through of Content Fragments and and AEM's GraphQL APIs and development tools.

* [AEM Headless GraphQL Video Series](./video-series/modeling-basics.md)

## AEM Headless GraphQL Hands-on Tutorial

Explore AEM's GraphQL capabilities by building out a React App that consumes Content Fragments via AEM's GraphQL APIs.

* [AEM Headless GraphQL Hands-on Tutorial](./multi-step/overview.md)

## AEM GraphQL vs. AEM Content Services

|                                | AEM GraphQL APIs | AEM Content Services |
|--------------------------------|:-----------------|:---------------------|
| Schema definition | Structured Content Fragment Models | AEM Components |
| Content | Content Fragments | AEM Components |
| Content discovery | By GraphQL query | By AEM Page |
| Delivery format | GraphQL JSON | AEM ComponentExporter JSON |
