---
title: Filtering with jQuery and Handlebars
description: A JavaScript implementation using jQuery and Handlebars that filters WKND Adventures to display. .
version: Cloud Service
mini-toc-levels: 1
feature: Content Fragments, GraphQL API
topic: Headless, Content Management
role: Developer
level: Beginner
jira: KT-11135
thumbnail: KT-11135.jpg
index: no
hide: yes
hidefromtoc: yes
exl-id: 75ffd84a-62b1-480f-b05f-3664f54bb171
duration: 33
---
# Filtering with jQuery and Handlebars

Explore AEM Headless GraphQL APIs ability to filter data using a JavaScript app that uses [jQuery](https://jquery.com/) and [Handlebars](https://handlebarsjs.com/). This app creates a list of WKND adventures filterable by Activity Type.

This code demonstrates using Adobe's [AEM Headless Client for JavaScript](https://github.com/adobe/aem-headless-client-js/blob/main/api-reference.md) to invoke persisted GraphQL queries. This app uses the `wknd-shared/adventures-all` persisted query to collect all adventures, and derive a list of available Activity Types. When a user selects an Activity Type, the selected type is passed to the `wknd-shared/adventures-by-activity` persisted query and retrieves the adventure details for only those adventures of the specified Activity Type.

This code:

+ Connects to an AEM Publish service, and does not require authentication
+ Uses the WKND's persisted queries: `wknd-shared/adventures-all` and `wknd-shared/adventures-by-activity`
