---
title: Search and indexing in AEM as a Cloud Service
description: Learn about AEM as a Cloud Service's search indexes, how to convert AEM 6 index definitions, and how to deploy indexes.
version: Cloud Service
feature: Search
topic: Migration, Upgrade
role: Developer
level: Experienced
kt: 8634
thumbnail: 336963.jpeg
exl-id: f752df86-27d4-4dbf-a3cb-ee97b7d9a17e
---
# Search and indexing

Learn about AEM as a Cloud Service's search indexes, how to convert AEM 6 index definitions to be AEM as a Cloud Service compatible, and how to deploy indexes to AEM as a Cloud Service.

>[!VIDEO](https://video.tv.adobe.com/v/336963/?quality=12&learn=on)

## Index Converter Tool

![Index Converter Tool](./assets/index-converter.png)

As part of refactoring your code base, use the [Index converter tool](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#command-aio-aem-migrationindex-converter) to convert custom Oak index definitions to AEM as a Cloud Service compatible index definitions.

### Key Activities

* Use the [Adobe I/O Workflow Migrator](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#command-aio-aem-migrationindex-converter) tool to migrate asset processing workflows to use the Asset Compute microservices.
* Set up a [local development environment](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html) and deploy the customized indices. Ensure that the updated indices are up to date.
* Deploy the updated code base to an AEM as a Cloud Service development environment and continue to validate.
* If modifying an out of the box index **ALWAYS** copy the latest index definition from an AEM as a Cloud Service environment running on the latest release. Modify the copied index definition to fit your needs.