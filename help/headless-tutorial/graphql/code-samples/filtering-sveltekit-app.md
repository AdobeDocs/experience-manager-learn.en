---
title: Simple SvelteKit app
description: A simple SvelteKit app that displays WKND adventures modeled using Content Fragments.
version: Cloud Service
feature: Content Fragments, GraphQL API
topic: Headless, Content Management
role: Developer
level: Beginner
kt: 11811
thumbnail: KT-11811.jpg
index: no
hide: yes
recommendations: noCatalog, noDisplay
hidefromtoc: yes
exl-id: 2e5bd50e-c0d7-4292-8097-e0a17f41a91a
---
# Filtering SvelteKit app

Explore AEM Headless GraphQL APIs ability to list data using a [SvelteKit](https://kit.svelte.dev/) app. This SvelteKit app creates a list of WKND adventures, that can be selected to display the adventure's details.

This code demonstrates using Adobe's [AEM Headless Client for JavaScript](https://github.com/adobe/aem-headless-client-js/blob/main/api-reference.md) to invoke persisted GraphQL queries from SvelteKit. This app uses the `wknd-shared/adventures-all` persisted query to collect all adventures, and derive a list of available Activity Types. Adventure details are requested via the `wknd-shared/adventures-by-slug` persisted query.

This code:

+ Connects to an AEM Publish service, and does not require authentication
+ Uses the WKND's persisted queries: `wknd-shared/adventures-all` and `wknd-shared/adventures-by-slug`
