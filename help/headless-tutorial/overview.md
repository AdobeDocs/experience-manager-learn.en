---
title: AEM Headless tutorials
description: A collection of tutorials on how to use Adobe Experience Manager as a Headless CMS.
feature: Content Fragments, APIs
topic: Headless, Content Management
role: Developer
level: Beginner
---

# AEM Headless tutorials

Adobe Experience Manager has multiple options for defining headless endpoints and delivering its content as JSON. Use hands-on tutorials to explore how to use the various options and chose what's right for you.

## AEM GraphQL APIs tutorial

>[!CAUTION]
>
> The AEM GraphQL API for Content Fragments Delivery is available on request.
> Please reach out to Adobe Support to enable the API for your AEM as a Cloud Service program.

AEM's GraphQL APIs for Content Fragments
supports headless CMS scenarios where external client applications render experiences using content managed in AEM.

A modern content delivery API is key for efficiency and performance of Javascript-based frontend applications. Using a REST API introduce challenges:  

* Large number of requests for fetching one object at a time
* Often "over-delivering" content, meaning the application receives more than it needs

To overcome these challenges GraphQL provides a query-based API allowing clients to query AEM for only the content it needs, and to receive using a single API call.

* Learn how to use AEM's GraphQL APIs in the [Getting Started with AEM GraphQL APIs tutorial](./graphql/overview.md)

## Token-based authentication tutorial

AEM exposes a variety of HTTP endpoints that can be interacted with in a headless manner, from GraphQL, AEM Content Services to Assets HTTP API. Often, these headless consumers may need to authenticate to AEM in order to access protected content or actions. To facilitate this, AEM supports token-based authentication of HTTP requests from external applications, services or systems. 

* Learn how to authenticate to AEM over HTTP using access tokens in the [Authenticating to AEM as a Cloud Service from an external application tutorial](./authentication/overview.md)

## AEM Content Services tutorial

AEM's Content Services leverages traditional AEM Pages to compose headless REST API endpoints, and AEM Components define, or reference, the content to expose on these endpoints.

AEM Content Services allows for the same content abstractions used for authoring web pages in AEM Sites, to define the content and schemas of these HTTP APIs. The use of AEM Pages and AEM Components empowers marketers to quickly compose and update flexible JSON APIs that can power any application.

* Learn how to use AEM's Content Services in the [Getting Started with AEM Content Services tutorial](./content-services/overview.md)

## AEM GraphQL vs. AEM Content Services

|                                | AEM GraphQL APIs | AEM Content Services | 
|--------------------------------|:-----------------|:---------------------|
| Schema definition | Structured Content Fragment Models | AEM Components |
| Content | Content Fragments | AEM Components |
| Content discovery | By GraphQL query | By AEM Page |
| Delivery format | GraphQL JSON | AEM ComponentExporter JSON |

## Other helpful tutorials

Other AEM tutorials pertaining to headless concepts include:

* [Getting Started with the AEM SPA Editor and Angular](https://experienceleague.adobe.com/docs/experience-manager-learn/spa-angular-tutorial/overview.html)
* [Getting Started with the AEM SPA Editor and React](https://experienceleague.adobe.com/docs/experience-manager-learn/spa-react-tutorial/overview.html)