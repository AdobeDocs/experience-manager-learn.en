---
title: Extending Page Properties in AEM Sites
description: Learn how to extend the metadata fields of Page Properties in Adobe Experience Manager Sites. This video details the most effective way to accomplish this using features of the Sling Resource Merger.
topic: Development
feature: Core Components
role: Developer
level: Intermediate
version: Experience Manager as a Cloud Service
jira: KT-243
thumbnail: 25173.jpg
doc-type: Technical Video
exl-id: 500f4e07-2686-42a2-8e44-d96dde02a112
duration: 488
TQID: https://experienceleague.adobe.com/xw-lzKy3-uEzhloVpnR4i8OdLB16ehnSn-Ye4WwIZxA
product_v2:
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: e2c1b6d3-bb7e-4fe8-8c72-f7b403298e91
    internal-label: Authoring
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
    internal-label: Metadata
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
---
# Extending Page Properties {#extending-page-properties-in-aem-sites}

Customizing the metadata fields for the Page Properties is a common requirement in any Sites implementation. This video details the most effective way to accomplish this using features of the Sling Resource Merger.

>[!VIDEO](https://video.tv.adobe.com/v/25173?quality=12&learn=on)

The above video shows customizing the page properties for the [WKND Reference Site](https://github.com/adobe/aem-guides-wknd).

## Sample WKND page properties package

You can use the provided [sample WKND page properties package](./assets/WKND-PageProperties-Example-Dialog-1.0.zip) containing **WKND** and **Basic** tab customizations shown in above video. The **SocialMedia** tab customization is not provided as [WKND Page component](https://github.com/adobe/aem-guides-wknd/blob/main/ui.apps/src/main/content/jcr_root/apps/wknd/components/page/.content.xml#L5) now uses V3 version of WCM Core Components and in V3 version the [social sharing is deprecated](https://github.com/adobe/aem-core-wcm-components/pull/1930). 

However for learning purposes, you can point the WKND Page component to V2 version of WCM Core Components using the `sling:resourceSuperType` property value and overlay the [Social Media](https://github.com/adobe/aem-core-wcm-components/blob/main/content/src/content/jcr_root/apps/core/wcm/components/page/v2/page/_cq_dialog/.content.xml#L95) tab. For more information, see [Configuring your Page Properties](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/page-properties-views.html#configuring-your-page-properties)

This sample package should be installed on local AEM SDK or AEM 6.X.X instance for learning purposes.
