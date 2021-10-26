---
title: Configuring Dispatcher when moving to AEM as a Cloud Service
description: Learn about notable changes to AEM Dispatcher for AEM as a Cloud Service, the Dispatcher conversion tool and how to use the Dispatcher Tools SDK.
version: Cloud Service
feature: Dispatcher
topic: Migration, Upgrade
role: Developer
level: Experienced
kt: 8633
thumbnail: 336962.jpeg
exl-id: 81397b21-b4f3-4024-a6da-a9b681453eff
---
# Dispatcher

Learn about AEM Dispatcher for AEM as a Cloud Service, focusing on notable changes from Dispatcher for AEM 6, the Dispatcher conversion tool and how to use the Dispatcher Tools SDK.

>[!VIDEO](https://video.tv.adobe.com/v/336962/?quality=12&learn=on)

## Dispatcher Converter

![Dispatcher Converter](./assets/dispatcher-converter-diagram.png)

As part of refactoring your code base, use the [AEM Dispatcher Converter](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/dispatcher-transformation-utility-tools.html) to refactor existing on-premise or Adobe Managed Services Dispatcher configurations to AEM as a Cloud Service compatible Dispatcher configuration.

### Key Activities

* Use the [Adobe I/O Dispatcher Converter tool](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#aio-aem-migrationdispatcher-converter) to migrate an existing Dispatcher configuration.
* Reference the Dispatcher module from the [AEM Project Archetype](https://github.com/adobe/aem-project-archetype/tree/develop/src/main/archetype/dispatcher.cloud) as a best practice.
* [Set up local Dispatcher Tools](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/dispatcher-tools.html) to validate dispatcher, before testing in a Cloud Service environment.


