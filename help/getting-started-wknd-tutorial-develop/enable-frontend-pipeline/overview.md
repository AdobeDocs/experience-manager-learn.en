---
title: Enable front-end pipeline for standard AEM project Archetype
description: Learn how to enable a Front-End pipeline for standard AEM project for faster deployment of static resources such as CSS, JavaScript, Fonts, Icons. Also separation of front-end development from full-stack back-end development on AEM.
sub-product: sites
version: Cloud Service
type: Tutorial
feature: AEM Project Archetype, Cloud Manager, CI-CD Pipeline
topic: Content Management, Development, Development, Architecture
role: Developer, Architect, Admin
level: Intermediate
kt: 10689
mini-toc-levels: 1
index: y
recommendations: disable
---

# Enable front-end pipeline for standard AEM project Archetype{#enable-front-end-pipeline-standard-aem-project}

Learn how to enable the [AEM WKND Sites Project](https://github.com/adobe/aem-guides-wknd) (aka Standard AEM Project) created using [AEM Project Archetype](https://github.com/adobe/aem-project-archetype) to deploy front-end resources such as CSS, JavaScript, Fonts, and Icons using a front-end pipeline for a faster development-to-deployment cycle. The separation of front-end development from full-stack back-end development on AEM. You also learn how these front-end resources are __not__ served from the AEM repository but from the CDN, a change in delivery paradigm.


A new front-end pipeline is created in Adobe Cloud Manager that only builds and deploys `ui.frontend` artifacts to the built-in CDN and informs AEM about its location. On AEM during the webpage's HTML generation, the `<link>` and `<script>` tags, refer to this artifact location in the `href` attribute value.

However, after the WKND Sites AEM project conversion, the front-end developers can work separately from and parallel to any full-stack back-end development on AEM, which has its own deployment pipelines.

>[!IMPORTANT]
>
>Generally speaking, the front-end pipeline is typically used with the [AEM Quick Site Creation](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/site-creation/quick-site/overview.html?lang=en), there is a related tutorial [Getting Started with AEM Sites - Quick Site Creation](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/site-template/overview.html) to learn more about it. So in this tutorial and associated videos you come across references to it, this is to make sure that subtle differences are called out and there is some direct or indirect comparison to explain crucial concepts.


A related [multi-step tutorial](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/site-template/overview.html) walks through implementing an AEM site for a fictitious lifestyle brand the WKND using the Quick Site Creation feature. Reviewing the [Theming workflow](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/site-template/theming.html) to understand the front-end Pipeline workings is also helpful.

## Overview, benefits, and considerations for front-end pipeline

>[!VIDEO](https://video.tv.adobe.com/v/3409343/)
          

>[!NOTE]
>
>This only applies to AEM as a Cloud Service and not for AMS-based Adobe Cloud Manager deployments.

## Prerequisites

The deployment step in this tutorial takes place in an Adobe Cloud Manager, ensure that you have a __Deployment Manager__ role, see Cloud Manage [Role Definitions](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/requirements/users-and-roles.html?lang=en#role-definitions). 

Make sure to use the [Sandbox program](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/programs/introduction-sandbox-programs.html) and [Development environment](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-environments.html) when completing this tutorial.

## Next steps {#next-steps}

A step-by-step tutorial walks through the [AEM WKND Sites Project](https://github.com/adobe/aem-guides-wknd) conversion to enable it for the front-end pipeline.

What are you waiting for? Start the tutorial by navigating to the [Review Full-stack Project](review-uifrontend-module.md) chapter and recap the front-end development life cycle in the context of the standard AEM Sites Project.

