---
title: Simple SvelteKit app
description: A simple SvelteKit app that displays WKND adventures modeled using Content Fragments.
version: Experience Manager as a Cloud Service
feature: Content Fragments, GraphQL API
topic: Headless, Content Management
role: Developer
level: Beginner
jira: KT-11811
thumbnail: KT-11811.jpg
index: false
hide: true
recommendations: noCatalog, noDisplay
exl-id: 2e5bd50e-c0d7-4292-8097-e0a17f41a91a
duration: 22
TQID: https://experienceleague.adobe.com/JhSWUxFsphhCt9z-hdvDUzCmL9Frc-t1LB3Pk-1jwJw
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
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
---
# Filtering SvelteKit app

Explore AEM Headless GraphQL APIs ability to list data using a [SvelteKit](https://kit.svelte.dev/) app. This SvelteKit app creates a list of WKND adventures, that can be selected to display the adventure's details.

This code demonstrates using Adobe's [AEM Headless Client for JavaScript](https://github.com/adobe/aem-headless-client-js/blob/main/api-reference.md) to invoke persisted GraphQL queries from SvelteKit. This app uses the `wknd-shared/adventures-all` persisted query to collect all adventures, and derive a list of available Activity Types. Adventure details are requested via the `wknd-shared/adventures-by-slug` persisted query.

This code:

+ Connects to an AEM Publish service, and does not require authentication
+ Uses the WKND's persisted queries: `wknd-shared/adventures-all` and `wknd-shared/adventures-by-slug`
