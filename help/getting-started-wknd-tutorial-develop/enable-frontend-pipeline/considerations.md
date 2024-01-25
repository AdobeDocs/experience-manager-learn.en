---
title: Development considerations
description: Consider the impact on the front-end and back-end development process once you enable the front-end pipeline.
version: Cloud Service
feature: AEM Project Archetype, Cloud Manager, CI-CD Pipeline
topic: Content Management, Development, Development, Architecture
role: Developer, Architect, Admin
level: Intermediate
jira: KT-10689
mini-toc-levels: 1
index: y
recommendations: noDisplay, noCatalog
doc-type: Tutorial
exl-id: a3b27d5b-b167-4c60-af49-8f2e8d814c86
duration: 89
---
# Development considerations

After enabling the front-end pipeline to only deploy the front-end resources in AEM as a Cloud Service environment, there is some impact on the local AEM development and you have to tweak the git branching model.

## Objective

* How to have a frictionless front-end and back-end development flow
* Review the dependencies between the full-stack and front-end pipeline


## Local development considerations

>[!VIDEO](https://video.tv.adobe.com/v/3409421?quality=12&learn=on)


## Adjusted development approach

*   For the local development using AEM SDK, the back-end dev team still needs clientlib generation via `ui.frontend` module but during Cloud Manager deployment to AEM as a Cloud Service environment you have to skip it. This surfaces a challenge on how to isolate the project config changes outlined in the [Update Project](update-project.md) chapter.

A __solution__ could be to adjust your git branching model and making sure the AEM project config changes never flow back to the __local development__ branch the AEM back-end developers use.


*   As part of an ongoing enhancement to your AEM project, if you introduce new components or update an existing component that has changes in both `ui.app` and `ui.frontend` module, you have to run both full-stack and front-end pipelines.
