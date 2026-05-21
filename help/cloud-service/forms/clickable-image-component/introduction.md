---
title: Create a Clickable Image Component
description: Create clickable image components in AEM Forms as a Cloud Service.
type: Documentation
role: Developer
level: Beginner, Intermediate
version: Experience Manager as a Cloud Service
feature: Adaptive Forms
topic: Development
jira: KT-15968
badgeVersions: label="AEM Forms as a Cloud Service" before-title="false"
exl-id: c451472f-d282-4662-9852-8a3e73c5c853
TQID: https://experienceleague.adobe.com/rxHRC6-yFaSr-89UFB7DiLtreIsUn7S6PrIC8I4JeeA
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
---
# Introduction to clickable images

Using clickable images in Forms can create a more engaging,intuitive, and visually appealing user experience. For the purpose of this article,we used SVG for clickable images as it offers several advantages particularly in terms of design flexibility, performance, and user experience.
SVG can be created using Adobe Illustrator or any of the free online tools. I have used the [USA Map from](https://simplemaps.com/resources/svg-us)simplemaps for demonstrating the use case.

## Use case for using clickable USA map

The clickable map of the USA allows users to explore state specific form submissions. When a user clicks on a state, the submissions from that state are listed, with the option to open a specific submission.
