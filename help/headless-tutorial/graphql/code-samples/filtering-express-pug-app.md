---
title: Filtering Express app
description: A simple Express app that filters WKND adventures modeled using Content Fragments.
version: Experience Manager as a Cloud Service
feature: Content Fragments, GraphQL API
topic: Headless, Content Management
role: Developer
level: Beginner
jira: KT-11812
thumbnail: KT-11812.jpg
index: false
hide: true
recommendations: noCatalog, noDisplay
exl-id: b64f33ab-cd18-4cbc-a57e-baf505f1442a
duration: 29
TQID: https://experienceleague.adobe.com/e-VvSlOhFjIVd8vgGJNp-h1ht1-eQ0wLv3AkXmcz04I
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
# Filtering Express app

Explore AEM Headless GraphQL APIs ability to filter data using a [Express](https://expressjs.com/) and [Pug](https://pugjs.org/) app. This Express app creates a list of WKND adventures filterable by Activity Type.

This code demonstrates using Adobe's [AEM Headless Client for NodeJS](https://github.com/adobe/aem-headless-client-nodejs#aem-headless-client-for-nodejs) to invoke persisted GraphQL queries using Node.js-based JavaScript. This app uses the `wknd-shared/adventures-all` persisted query to collect all adventures, and derive a list of available Activity Types. When a user selects an Activity Type, the selected type is passed to the `wknd-shared/adventures-by-activity` persisted query and retrieves the adventure details for only those adventures of the specified Activity Type. Adventure details are retrieved from AEM via the `wknd-shared/adventures-by-slug` persisted query.

This code:

+ Connects to an AEM Publish service, and does not require authentication
+ Uses the WKND's persisted queries: `wknd-shared/adventures-all`, `wknd-shared/adventures-by-activity`, and `wknd-shared/adventures-by-slug`
