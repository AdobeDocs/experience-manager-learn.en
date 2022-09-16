---
title: React component
description: An example React component that displays a Content Fragment and referenced image assets.
version: Cloud Service
mini-toc-levels: 1
feature: Content Fragments, GraphQL API
topic: Headless, Content Management
role: Developer
level: Beginner
kt: 11134
thumbnail: KT-11134.jpg
index: no
hide: yes
hidefromtoc: yes
---

# React component

This React component consumes a single WKND adventure Content Fragment and displays its content as a promotional banner.

This code:

+ Connects to [wknd.site](https://wknd.site)'s AEM Publish service, and does not require authentication
+ Use the persisted query: `wknd-shared/adventures-by-slug`
