---
title: Get started with AEM Headless - GraphQL
description: Learn about the Experience Manager GraphQL APIs and their capabilities.
feature: Content Fragments, GraphQL API, APIs
topic: Headless, Content Management
role: Developer
level: Beginner
exl-id: 0056971f-2f89-43b3-bb6f-dd16c2a50370
---
# Getting Started with AEM Headless - GraphQL

AEM's GraphQL APIs for Content Fragments
supports headless CMS scenarios where external client applications render experiences using content managed in AEM.

A modern content delivery API is key for efficiency and performance of Javascript-based frontend applications. Using a REST API introduce challenges:  

* Large number of requests for fetching one object at a time
* Often "over-delivering" content, meaning the application receives more than it needs

To overcome these challenges GraphQL provides a query-based API allowing clients to query AEM for only the content it needs, and to receive using a single API call.

>[!VIDEO](https://video.tv.adobe.com/v/328618/?quality=12&learn=on)

This video is an overview of the GraphQL API implemented in AEM. The GraphQL API in AEM is primarily designed to deliver AEM Content Fragment's to downstream applications as part of a headless deployment.

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
