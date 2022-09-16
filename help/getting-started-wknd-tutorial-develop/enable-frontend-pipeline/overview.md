---
title: Enable Front-End Pipeline for Standard AEM Project Archetype
description: Convert a standard AEM project for faster deployment of static resources such as CSS, JavaScript, Fonts, Icons using Front-End pipeline. And separation of Front-End development from full-stack back-end development on AEM.
sub-product: sites
version: Cloud Service
type: Tutorial
feature: AEM Project Archetype, Cloud Manager, CI-CD Pipeline
topic: Content Management, Development, Development, Architecture
role: Developer, Architect, Admin
level: Intermediate
mini-toc-levels: 1
index: y
recommendations: disable
---

# Enable Front-End Pipeline for Standard AEM Project Archetype{#enable-front-end-pipeline-standard-aem-project}

Learn how to enable the standard AEM project created using [AEM Project Archetype](https://github.com/adobe/aem-project-archetype) to deploy static resources such as CSS, JavaScript, Fonts, Icons using Front-End pipeline for faster development-to-deployment cycle. And separation of Front-End development from full-stack back-end development on AEM. You also learn how these static resources are __not__ served from AEM repository but from the CDN, a change in delivery paradigm. 

A new Front-End pipeline is created in Adobe Cloud Manager that only builds and deploys `ui.frontend` artifacts to CDN and informs AEM about its location. During webpage's HTML generation, the `<link>` and `<script>` tags refer this location in the `href` attribute value.

After the standard AEM project conversion, the front-end developers can work separately from and parallel to any full-stack back-end development on AEM, which has its own deployment pipelines.

>[!VIDEO](https://video.tv.adobe.com/v/3409268)

>[!NOTE]
>
>This is only applicable to AEM as a Cloud Service and not for AMS based Adobe Cloud Manager deployments.

