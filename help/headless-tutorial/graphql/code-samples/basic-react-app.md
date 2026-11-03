---
title: Basic React app
description: A basic React app that displays a list of WKND adventures and their details
version: Experience Manager as a Cloud Service
mini-toc-levels: 1
feature: Content Fragments, GraphQL API
topic: Headless, Content Management
role: Developer
level: Beginner
jira: KT-11134
thumbnail: KT-11134.jpg
index: false
hide: true
exl-id: 870be37f-68bb-4b0f-9918-e68b09be830e
duration: 17
TQID: 'https://experienceleague.adobe.com/omAonJ2mmMHE-I7KNek2SJQrqqKIG7u9ENYfFqSzumU'
product_v2:
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: a01bfd36-4ab8-4bf8-9dc0-5b45b890552e
    internal-label: APIs
  - id: bfd4bc52-c397-5127-8f86-8953ba9fc0a3
    internal-label: Headless
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
---
# Basic React app

This [React](https://reactjs.org/) app demonstrates how to query content using AEM's GraphQL APIs using persisted queries. This application renders a filterable of WKND Adventures, and upon selecting an adventure, displays the adventures full details.

This code:

+ Connects to an AEM Publish service, and does not require authentication
+ Uses the WKND's persisted queries: `wknd-shared/adventures-all` and `wknd-shared/adventures-by-slug`

For a more indepth review of how this Next.js app is built, review the [example React app documentation](../example-apps/react-app.md).
