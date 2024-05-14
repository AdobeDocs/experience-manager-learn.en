---
title: Filtering Vue app
description: A simple Vue app that filters WKND adventures modeled using Content Fragments.
version: Cloud Service
feature: Content Fragments, GraphQL API
topic: Headless, Content Management
role: Developer
level: Beginner
jira: KT-11366
thumbnail: KT-11366.jpg
index: no
hide: yes
hidefromtoc: yes
exl-id: 8f96093a-4449-4249-9257-028e2ffd979b
duration: 26
---
# Filtering Vue app

Explore AEM Headless GraphQL APIs ability to filter data using a [Vue](https://vuejs.org/) app. This React app creates a list of WKND adventures filterable by Activity Type.

This code demonstrates using Adobe's [AEM Headless Client for JavaScript](https://github.com/adobe/aem-headless-client-js/blob/main/api-reference.md) to invoke persisted GraphQL queries from Vue. This app uses the `wknd-shared/adventures-all` persisted query to collect all adventures, and derive a list of available Activity Types. When a user selects an Activity Type, the selected type is passed to the `wknd-shared/adventures-by-activity` persisted query and retrieves the adventure details for only those adventures of the specified Activity Type.

This code:

+ Connects to an AEM Publish service, and does not require authentication
+ Uses the WKND's persisted queries: `wknd-shared/adventures-all` and `wknd-shared/adventures-by-activity`
