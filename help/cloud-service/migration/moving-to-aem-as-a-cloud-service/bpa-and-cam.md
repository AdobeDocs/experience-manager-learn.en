---
title: Set up your BPA and CAM project
description: Learn how Best Practice Analyzer and Cloud Acceleration Manager provides a customized guide for migrating to AEM as a Cloud Service.
version: Cloud Service
feature: Developer Tools
topic: Migration, Upgrade
role: Developer
level: Experienced
kt: 8627
thumbnail: 336957.jpeg
exl-id: f8289dd4-b293-4b8f-b14d-daec091728c0
---
# Best Practice Analyzer and Cloud Acceleration Manager

Learn how Best Practice Analyzer (BPA) and Cloud Acceleration Manager (CAM) provides a customized guide for migrating to AEM as a Cloud Service. 

>[!VIDEO](https://video.tv.adobe.com/v/336957/?quality=12&learn=on)

## Evaluate readiness

![BPA and CAM high level diagram](assets/bpa-cam-diagram.png)

The BPA package should be installed on a clone of the production AEM 6.x environment. The BPA will generate a report that can then be uploaded into CAM, which will provide guidance into the key activities that need to take place in order to move to AEM as a Cloud Service.

### Key Activities

* Make a clone of your production 6.x environment. As you migrate content and refactor code, having a clone of a production environment will be valuable to test various tools and changes.
* Download the latest BPA tool from the [Software Distribution Portal](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html) and install on your AEM 6.x cloned environment.
* Use the BPA tool to generate a report that can be uploaded to Cloud Acceleration Manager (CAM). CAM is accessed through [https://experience.adobe.com/](https://experience.adobe.com/) > **Experience Manager** > **Cloud Acceleration Manager**. 
* Use CAM to provide guidance on what updates need to be made to the current code base and environment in order to move to AEM as a Cloud Service.
