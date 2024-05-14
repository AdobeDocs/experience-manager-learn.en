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
last-substantial-update: 2022-07-10
badgeIntegration: label="Integration" type="positive"
badgeVersions: label="AEM Sites as a Cloud Service, AEM Sites 6.5" before-title="false"
doc-type: Tutorial
exl-id: bdae56d8-96e7-4b05-9b8b-3c6c2e998bd8
duration: 230
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
