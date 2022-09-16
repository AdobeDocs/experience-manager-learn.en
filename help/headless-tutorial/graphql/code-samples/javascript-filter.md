---
title: Filtering queries
description: A JavaScript implementation that allows specific Content Fragments to be selected and then their details displayed .
version: Cloud Service
mini-toc-levels: 1
feature: Content Fragments, GraphQL API
topic: Headless, Content Management
role: Developer
level: Beginner
kt: 11135
thumbnail: KT-11135.jpg
index: no
hide: yes
hidefromtoc: yes
---

# Filtering queries

This JavaScript and Handlebars example illustrates how to filter GraphQL results, and display the selected results.

This code:

+ Connects to [wknd.site](https://wknd.site)'s AEM Publish service, and does not require authentication
+ Uses the persisted queries: `wknd-shared/adventures-all` and `wknd-shared/adventures-by-slug`
