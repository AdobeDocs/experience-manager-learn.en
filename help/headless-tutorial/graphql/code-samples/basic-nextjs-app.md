---
title: Basic Next.js app
description: A basic Next.js app that displays a list of WKND adventures and their details
version: Experience Manager as a Cloud Service
mini-toc-levels: 1
feature: Content Fragments, GraphQL API
topic: Headless, Content Management
role: Developer
level: Beginner
jira: KT-11368
thumbnail: KT-11368.jpg
index: false
hide: true
exl-id: 2d4396dc-2346-4561-b040-eba0ab62a96f
duration: 22
TQID: https://experienceleague.adobe.com/S8rzOg8HnXzTn8E5pbPhfb651yrXe6MK-QqE4RAxD-o
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
# Basic Next.js app

This [Next.js](https://nextjs.org/) app demonstrates how to query content using AEM's GraphQL APIs using persisted queries. This application renders a filterable of WKND Adventures, and upon selecting an adventure, displays the adventures full details.

This code:

+ Connects to an AEM Publish service, and does not require authentication
+ Uses the WKND's persisted queries: `wknd-shared/adventures-all` and `wknd-shared/adventures-by-slug`

>[!IMPORTANT]
>
> Codesandbox.io does not support editting of Next.js application in the embedded IDE. To edit this code sample, [open the Next.js app directly on codesandbox.io](https://codesandbox.io/s/wknd-next-js-app-u8x5f8).
