---
title: Integrate Launch by Adobe with AEM Sites
seo-title: Integrate Launch by Adobe with AEM Sites
description: Technical walk-through of of how to configure the Adobe Experience Manager integration with Launch by Adobe. This integration allows customer to pull the Launch "embed codes" and related JavaScript libraries into AEM Sites.
seo-description: Technical walk-through of of how to configure the Adobe Experience Manager integration with Launch by Adobe. This integration allows customer to pull the Launch "embed codes" and related JavaScript libraries into AEM Sites.
uuid: abc18e60-02f2-438f-bbdf-412abe15ecf4
products: SG_EXPERIENCEMANAGER/6.4
topic-tags: DTM
content-type: video
products: SG_EXPERIENCECLOUD
topic-tags: activation
discoiquuid: 75fc8e92-ac51-40c0-8825-02990cc26514
targetaudience: target-audience ongoing
index: y
internal: n
snippet: y
---

# Integrate Launch by Adobe {#integrate-launch-by-adobe-with-aem-sites}

Technical walk-through of of how to configure the Adobe Experience Manager (AEM) 6.4 integration with Launch by Adobe. This integration allows customer to pull the Launch "embed codes" and related JavaScript libraries into AEM Sites.

## Overview {#overview}

>[!VIDEO](https://video.tv.adobe.com/v/21982/?quality=12)

Launch is Adobe's next-generation tag management platform and the best way to deploy Adobe Analytics, Target, Audience Manager, Experience Cloud ID Service, and all of their 3rd party marketing solutions using Launch by Adobe.

The integration allows for the self-hosting of the Launch JavaScript libraries which gives the customer maximum control over their code, which is especially important for financial services customers. Alternatively, customers can use this integration to host their Launch libraries on Adobe's Akamai instance.

These three videos explain everything you need to know to successfully implement the integration, from creating a property in Launch, connecting Adobe IO to AEM, and configuring the Launch Cloud Service in AEM to finally pull in the embed codes and JavaScript libraries.

## Step 1: Configure the Launch Property {#launch}

In this step we will configure a Launch property with the bare-minimum configuration needed to set up the rest of the integration.

>[!VIDEO](https://video.tv.adobe.com/v/21984/?quality=12)

>[!NOTE]
>
>Full rights in Adobe Launch are required to complete the steps in this video.
>
>More information about using Launch can be found in the [Adobe Launch Videos,](https://marketing.adobe.com/resources/help/en_US/experience-cloud/launch/videos.html) [Help Documentation](https://marketing.adobe.com/resources/help/en_US/experience-cloud/launch/) and [Launch Reference Architectures landing page](https://helpx.adobe.com/experience-manager/kt/integration/using/launch-reference-architecture-guides.html).

## Step 2: Connect Adobe IO and Adobe Experience Manager {#adobeio}

In this step, the Launch Integration will be configured in Adobe I/O and connected to AEM.

>[!VIDEO](https://video.tv.adobe.com/v/21983/?quality=12)

>[!NOTE]
>
>The "Launch, By Adobe" integration in the Adobe I/O interface is now labeled "Experience Platform Launch API" and is located under the "Adobe Experience Platform" heading.
>
>System Administrator rights in the Experience Cloud organization and AEM admin rights are required to configure the Adobe IO integration and set up the IMS Configuration.

## Step 3: Configure the Launch Cloud Service in Adobe Experience Manager {#step-configure-the-launch-cloud-service-in-adobe-experience-manager}

In the final step, the Launch Cloud Configuration will be set up and the correct Launch property will be applied to the AEM site.

>[!VIDEO](https://video.tv.adobe.com/v/21985/?quality=12)

>[!NOTE]
>
>Admin rights in AEM are required to configure the Launch Cloud Service.

## Additional Resources {#additional-resources}

If you have completed the steps above but you are not seeing the Launch embed codes in your own site please see the section "Map an Adobe Launch integration to a site in AEM" in the following article:

* [Integrate AEM with Adobe Launch Via Adobe I/O](https://helpx.adobe.com/experience-manager/using/aem_launch_adobeio_integration.html)
