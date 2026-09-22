---
title: Using Social Media Sharing in AEM Sites
description: Explore setting up and using the Social Media Sharing component.
feature: Core Components
version: Experience Manager 6.4, Experience Manager 6.5
topic: Content Management
role: Developer
level: Intermediate
doc-type: Technical Video
exl-id: 569069e8-7964-49f1-96ed-7dfa4f8ed96c
duration: 511
TQID: 'https://experienceleague.adobe.com/-kYLQJNUGu6X6MMsUmtJwGkW2Ft8IGejGzXGjt3Dbs8'
product_v2:
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: 2741637d-a621-529a-b21b-bfe9be07a9c8
    internal-label: Dispatcher
  - id: 523b1ccd-901e-5e3b-9fa7-f3dfd82463d5
    internal-label: Configuring
  - id: c5d917df-d8bd-5e97-a117-6dde1e9f7103
    internal-label: Developing
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
---
# Using Social Media Sharing {#using-social-media-sharing-in-aem-sites}

Explore setting up and using the Social Media Sharing component.

>[!VIDEO](https://video.tv.adobe.com/v/18897?quality=12&learn=on)

This video explores the following facilities of the Social Media Sharing component (part of [AEM Core Components](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html)) using the [We.Retail](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail#weretail) sample web site.

* 0:00 - Adding and configuring the Social Media Sharing component
* 1:00 - Sharing to Facebook
* 3:10 - Sharing to Pinterest
* 6:25 - Using the Social Media Sharing component on a Product page

## Externalizer setup {#externalizer-setup}

![Day CQ Link Externalizer](assets/externalizer.png)

[http://localhost:4502/system/console/configMgr/com.day.cq.commons.impl.ExternalizerImpl](http://localhost:4502/system/console/configMgr/com.day.cq.commons.impl.ExternalizerImpl)

[AEM's externalizer](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/externalizer.html) should be set up on both AEM Author and AEM Publish, to map the publish runmode to the publicly accessible domain used to access AEM Publish.

In this video we use `/etc/hosts` to spoof *www.example.com* to resolve to localhost, and use a [basic AEM Dispatcher configuration](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/getting-started/dispatcher-install.html) to allow www.example.com to front AEM Publish.

## Supporting materials {#supporting-materials}

* [Download the AEM Core Components](https://github.com/adobe/aem-core-wcm-components/releases)
* [Download We.Retail](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/releases)
* [Installing Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/getting-started/dispatcher-install.html)
