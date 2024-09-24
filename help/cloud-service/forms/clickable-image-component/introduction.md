---
title: Create a Clickable Image Component
description: Create clickable image components in AEM Forms Cloud Service.
type: Documentation
role: Developer
level: Beginner, Intermediate
version: Cloud Service
feature: Adaptive Forms
topic: Development
jira: KT-15968
badgeVersions: label="AEM Forms as a Cloud Service" before-title="false"
exl-id: c451472f-d282-4662-9852-8a3e73c5c853
---
# Introduction to clickable images

Using clickable images in Forms can create a more engaging,intuitive, and visually appealing user experience. For the purpose of this article,we used SVG for clickable images as it offers several advantages particularly in terms of design flexibility, performance, and user experience.
SVG can be created using Adobe Illustrator or any of the free online tools. I have used the [USA Map from](https://simplemaps.com/resources/svg-us)simplemaps for demonstrating the use case.

## Use case for using clickable USA map

The clickable map of the USA allows users to explore state specific form submissions. When a user clicks on a state, the submissions from that state are listed, with the option to open a specific submission.
