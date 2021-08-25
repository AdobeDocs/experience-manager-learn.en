---
title: Integrating Adobe Experience Manager with Adobe Target using Cloud Services
seo-title: Integrating Adobe Experience Manager (AEM) with Adobe Target using Legacy Cloud Services
description: Step by step walkthrough on how to integrate Adobe Experience Manager (AEM) with Adobe Target using AEM Cloud Service
seo-description: Step by step walkthrough on how to integrate Adobe Experience Manager (AEM) with Adobe Target using AEM Cloud Service
feature: Experience Fragments
topic: Personalization
role: Developer
level: Intermediate
---

# Using AEM Legacy Cloud Services

In this section, we will discuss how to set up Adobe Experience Manager (AEM) with Adobe Target using Legacy Cloud Services.

>[!NOTE]
>
> The AEM Legacy Cloud Service with Adobe Target is **only** used to establish direct AEM Author to Adobe Target back-end connection facilitating the publication of content from AEM to Target. Adobe Launch is used expose Adobe Target on the public facing Web site experience served by AEM.

In order to use AEM Experience Fragment offers to power you personalization activities, lets proceed to the next chapter, and integrate AEM with Adobe Target using the legacy cloud services. This integration is required to push Experience Fragments from AEM to Target as HTML/JSON offers and to keep the target offers in sync with AEM. This integration is required for implementing [Scenario 1 discussed in the overview section](./overview.md#personalization-using-aem-experience-fragment).

## Prerequisites

* **AEM**

  * AEM author and publish instance are necessary to complete this tutorial. If you haven't set up your AEM instance yet, you can follow the steps [here](./implementation.md#set-up-aem).

* **Experience Cloud**
  * Access to your organizations Adobe Experience Cloud - `https://<yourcompany>.experiencecloud.adobe.com`
  * Experience Cloud provisioned with the following solutions
    * [Adobe Target](https://experiencecloud.adobe.com)
  
    >[!NOTE]
    >
    > Customer needs to be provisioned with Experience Platform Launch and Adobe I/O from [Adobe support](https://helpx.adobe.com/contact/enterprise-support.ec.html) or reach out to your system administrator

### Integrating AEM with Adobe Target

>[!VIDEO](https://video.tv.adobe.com/v/28428?quality=12&learn=on)

1. Create Adobe Target Cloud Service using Adobe IMS Authentication (*Uses Adobe Target API*) (00:34)
2. Obtain Adobe Target Client Code (01:50)
3. Create Adobe IMS Configuration for Adobe Target (02:08)
4. Create a Technical Account for accessing Target API within Adobe I/O Console (02:08)
5. Add Adobe Target Cloud Service to AEM Experience Fragments (04:12)

At this point, you have successfully integrated [AEM with Adobe Target using Legacy Cloud Services](./using-aem-cloud-services.md#integrating-aem-target-options) as detailed in Option 2. You should now be able to create an Experience Fragment within AEM, and publish the Experience Fragment as HTML offer or JSON Offer to Adobe Target, and can then be used to create an activity.
