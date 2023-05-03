---
title: Extending Page Properties in AEM Sites
description: Learn how to extend the metadata fields of Page Properties in Adobe Experience Manager Sites. This video details the most effective way to accomplish this using features of the Sling Resource Merger.
topic: Development
feature: Core Components
role: Developer
version: Cloud Service
kt: 243
thumbnail: 25173.jpg
exl-id: 500f4e07-2686-42a2-8e44-d96dde02a112
---
# Extending Page Properties {#extending-page-properties-in-aem-sites}

Customizing the metadata fields for the Page Properties is a common requirement in any Sites implementation. This video details the most effective way to accomplish this using features of the Sling Resource Merger.

>[!VIDEO](https://video.tv.adobe.com/v/25173?quality=12&learn=on)

The above video shows customizing the page properties for the [WKND Reference Site](https://github.com/adobe/aem-guides-wknd).

## Sample WKND page properties package

You can use the provided [sample WKND page properties package](./assets/WKND-PageProperties-Example-Dialog-1.0.zip) containing **WKND** and **Basic** tab customizations shown in above video. The **SocialMedia** tab customization is not provided as [WKND Page component](https://github.com/adobe/aem-guides-wknd/blob/main/ui.apps/src/main/content/jcr_root/apps/wknd/components/page/.content.xml#L5) now uses V3 version of WCM Core Components and in V3 version the [social sharing is deprecated](https://github.com/adobe/aem-core-wcm-components/pull/1930). 

However for learning purposes, you can point the WKND Page component to V2 version of WCM Core Components using the `sling:resourceSuperType` property value and overlay the [Social Media](https://github.com/adobe/aem-core-wcm-components/blob/main/content/src/content/jcr_root/apps/core/wcm/components/page/v2/page/_cq_dialog/.content.xml#L95) tab. For more information, see [Configuring your Page Properties](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/page-properties-views.html#configuring-your-page-properties)

This sample package should be installed on local AEM SDK or AEM 6.X.X instance for learning purposes.
