---
title: Filtering Express app
description: A simple Express app that filters WKND adventures modeled using Content Fragments.
version: Cloud Service
feature: Content Fragments, GraphQL API
topic: Headless, Content Management
role: Developer
level: Beginner
jira: KT-11812
thumbnail: KT-11812.jpg
index: no
hide: yes
hidefromtoc: yes
recommendations: noCatalog, noDisplay
exl-id: b64f33ab-cd18-4cbc-a57e-baf505f1442a
duration: 29
---
# Filtering Express app

Explore AEM Headless GraphQL APIs ability to filter data using a [Express](https://expressjs.com/) and [Pug](https://pugjs.org/) app. This Express app creates a list of WKND adventures filterable by Activity Type.

This code demonstrates using Adobe's [AEM Headless Client for NodeJS](https://github.com/adobe/aem-headless-client-nodejs#aem-headless-client-for-nodejs) to invoke persisted GraphQL queries using Node.js-based JavaScript. This app uses the `wknd-shared/adventures-all` persisted query to collect all adventures, and derive a list of available Activity Types. When a user selects an Activity Type, the selected type is passed to the `wknd-shared/adventures-by-activity` persisted query and retrieves the adventure details for only those adventures of the specified Activity Type. Adventure details are retrieved from AEM via the `wknd-shared/adventures-by-slug` persisted query.

This code:

+ Connects to an AEM Publish service, and does not require authentication
+ Uses the WKND's persisted queries: `wknd-shared/adventures-all`, `wknd-shared/adventures-by-activity`, and `wknd-shared/adventures-by-slug`
