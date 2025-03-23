---
title: Debugging AEM with Repository Browser
description: Repository Browser is a powerful tool that provides visibility into AEM's underlying data store, allowing for easy debugging of AEM as a Cloud Service environment.
feature: Developer Tools
version: Experience Manager as a Cloud Service
doc-type: Tutorial
jira: KT-10004
thumbnail: 341464.jpg
topic: Development
role: Developer
level: Beginner
exl-id: 88af40fc-deff-4b92-84b1-88df2dbdd90b
duration: 305
---
# Debugging AEM as a Cloud Service with Repository Browser

Repository Browser is a powerful tool that provides visibility into AEM's underlying data store, allowing for easy debugging of AEM as a Cloud Service environment. Repository Browser supports a read-only view of the resources and properties of AEM on Production, Stage, and Development, as well as Author, Publish, and Preview services.

>[!VIDEO](https://video.tv.adobe.com/v/341464?quality=12&learn=on)

Repository Browser is __ONLY__ available on AEM as a Cloud Service environments (use [CRXDE Lite](../aem-sdk-local-quickstart/other-tools.md#crxde-lite) to debug the local AEM SDK).

## Accessing Repository Browser

To access Repository Browser on AEM as a Cloud Service:

1. Ensure that your user has [the required access](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developer-tools/repository-browser.html#access-prerequisites)
1. Log in to [Cloud Manager](https://my.cloudmanager.adobe.com)
1. Select the Program containing the AEM as a Cloud Service environment to debug
1. Open the [Developer Console](./developer-console.md) corresponding to the AEM as a Cloud Service environment to debug
1. Select the __Repository Browser__ tab
1. Select the AEM service tier to browse
    + All Authors
    + All Publishers
    + All Previews
1. Select __Open Repository Browser__

The Repository Browser opens for the selected service tier (Author, Publish, or Preview) in a read-only mode, displaying resources and properties your user has access to.

## Publish and Preview access

By default, access to Publish or Preview is limited, reducing the available resources in Repository Browser. [To view all resources on Publish (or Preview) add users to a Publish (or Preview) Administrators role.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developer-tools/repository-browser.html#navigate-the-hierarchy)
