---
title: Getting Started with AEM Headless - Content Services
description: An end-to-end tutorial illustrating how to build-out and expose content using AEM Headless.
feature: Content Fragments, APIs
topic: Headless, Content Management
role: Developer
level: Beginner
exl-id: 5aa32791-861a-48e3-913c-36028373b788
---
# Getting Started with AEM Headless - Content Services

AEM's Content Services leverages traditional AEM Pages to compose headless REST API endpoints, and AEM Components define, or reference, the content to expose on these endpoints.

AEM Content Services allows for the same content abstractions used for authoring web pages in AEM Sites, to define the content and schemas of these HTTP APIs. The use of AEM Pages and AEM Components empowers marketers to quickly compose and update flexible JSON APIs that can power any application.

## Content Services Tutorial

An end-to-end tutorial illustrating how to build-out and expose content using AEM and consumed by a native mobile app, in a headless CMS scenario.

>[!VIDEO](https://video.tv.adobe.com/v/28315/?quality=12&learn=on)

This tutorial explores how AEM Content Services can be used to power the experience of an Mobile App that displays Event information (music, performance, art, etc.) that is curated by the WKND team.

This tutorial will cover the following topics:

* Create content that represent an Event using Content Fragments
* Define an AEM Content Services end-points using AEM Sites' Templates and Pages that expose the Event data as JSON
* Explore how AEM WCM Core Components can be used to enable marketers to author JSON end-points
* Consume AEM Content Services JSON from an Mobile App
  * The use of Android is because it has a cross-platform emulator that all users (Windows, macOS, and Linux) of this tutorial can use to run the native App.

## GitHub Project

The source code, and content packages are available on the [AEM Guides - WKND Mobile GitHub Project](https://github.com/adobe/aem-guides-wknd-mobile).

If you find an issue with the tutorial or the code, please leave a [GitHub issue](https://github.com/adobe/aem-guides-wknd-mobile/issues).

## AEM GraphQL vs. AEM Content Services

|                                | AEM GraphQL APIs | AEM Content Services | 
|--------------------------------|:-----------------|:---------------------|
| Schema definition | Structured Content Fragment Models | AEM Components |
| Content | Content Fragments | AEM Components |
| Content discovery | By GraphQL query | By AEM Page |
| Delivery format | GraphQL JSON | AEM ComponentExporter JSON |
