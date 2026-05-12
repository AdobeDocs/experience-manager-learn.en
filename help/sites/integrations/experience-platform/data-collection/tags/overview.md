---
title: Integrating tags in Adobe Experience Platform and AEM
description: Tags in Experience Platform Data Collection is Adobe's next-generation tag management solution and the best way to deploy Adobe Analytics, Target, Audience Manager, and many more solutions. Get an overview of tags in Adobe Experience Platform and the recommended integration with Adobe Experience Manager.
solution: Experience Manager, Data Collection, Experience Platform
jira: KT-5979
thumbnail: 39090.jpg
topic: Integrations
feature: Integrations
role: Developer
level: Intermediate
last-substantial-update: 2022-07-10T00:00:00.000Z
badgeIntegration: label="Integration" type="positive"
badgeVersions: label="AEM Sites as a Cloud Service, AEM Sites 6.5" before-title="false"
doc-type: Tutorial
exl-id: bdae56d8-96e7-4b05-9b8b-3c6c2e998bd8
duration: 230
TQID: https://experienceleague.adobe.com/ZEaZ4P4-xDd3ROp23tG8-SWMVFE6SX1R9xlqDNjvJeI
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
    internal-label: Experience Platform
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: ae478996-b206-4712-9b0c-dc78a2644453
    internal-label: Integrations
  - id: e08599ea-8888-4294-ba74-3ba0a7762a46
    internal-label: Data collection
  - id: ed0d8d0e-04b9-4326-be72-a0fbca265377
    internal-label: Integrations
subfeature_v2:
  - id: abc02dd6-664f-446a-9aaa-675bc0f2fe4a
    internal-label: Sources
  - id: d9830f6f-ceb6-4faa-9744-f281fe4439f9
    internal-label: Tags
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
topic_v2:
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
    internal-label: Security
  - id: d3cdead0-685a-4489-9250-4bb709942f66
    internal-label: Data collection
---
# Integrating Experience Platform Data Collection Tags and AEM {#overview}

Learn how to integrate the tags in Adobe Experience Platform with Adobe Experience Manager.

Tags are Adobe Experience Platform's next generation of tag management technology. Tags provide the simplest way to deploy Adobe Analytics, Target, Audience Manager, and many more solutions. Get an overview of Tags and the recommended integration with Adobe Experience Manager.

>[!VIDEO](https://video.tv.adobe.com/v/3417061?quality=12&learn=on)

## Prerequisites

The following are required when integrating Experience Platform Data Collection Tags.

+ AEM administrator access to AEM as a Cloud Service environment
+ A reference site like [WKND](https://github.com/adobe/aem-guides-wknd) deployed onto it.
+ Access to Adobe Experience Platform Data Collection solution
+ System Administrator access to [Adobe Developer Console](https://developer.adobe.com/developer-console/)


## High-level steps

+ In Adobe Experience Platform Data Collection, create a Tag property and edit it to _Add Rule_. Then _Add Library_, select the newly added rule, approve, and publish it.
+ Connect AEM and Tags using existing (or new) IMS configuration
+ In AEM, create a tags cloud service configuration, then apply it to an existing site and finally verify Tags property and its libraries are loaded on the Published or Author site.

## Next Steps

[Create a Tag Property](create-tag-property.md)

## Additional Resources {#additional-resources}

+ [Experience Platform Integrations with Experience Cloud Applications](https://experienceleague.adobe.com/docs/platform-learn/tutorials/intro-to-platform/integrations-with-experience-cloud-applications.html)
+ [Tags overview](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html)
+ [Implementing the Experience Cloud in Websites with Tags](https://experienceleague.adobe.com/docs/platform-learn/implement-in-websites/overview.html)
