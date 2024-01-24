---
title: Configuring Dispatcher when moving to AEM as a Cloud Service
description: Learn about notable changes to AEM Dispatcher for AEM as a Cloud Service, the Dispatcher conversion tool and how to use the Dispatcher Tools SDK.
version: Cloud Service
feature: Dispatcher
topic: Migration, Upgrade
role: Developer
level: Experienced
jira: KT-8633
thumbnail: 336962.jpeg
exl-id: 81397b21-b4f3-4024-a6da-a9b681453eff
duration: 1634
---

# Dispatcher

Learn about AEM Dispatcher for AEM as a Cloud Service, focusing on notable changes from Dispatcher for AEM 6, the Dispatcher conversion tool and how to use the Dispatcher Tools SDK.

>[!VIDEO](https://video.tv.adobe.com/v/336962?quality=12&learn=on)

## Dispatcher Converter

![Dispatcher Converter](./assets/dispatcher-converter-diagram.png)

As part of refactoring your code base, use the [AEM Dispatcher Converter](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/dispatcher-transformation-utility-tools.html) to refactor existing on-premise or Adobe Managed Services Dispatcher configurations to AEM as a Cloud Service compatible Dispatcher configuration.

## Key activities

+ Use the [Adobe I/O Dispatcher Converter tool](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#aio-aem-migrationdispatcher-converter) to migrate an existing Dispatcher configuration.
+ Reference the Dispatcher module from the [AEM Project Archetype](https://github.com/adobe/aem-project-archetype/tree/develop/src/main/archetype/dispatcher.cloud) as a best practice.
+ [Set up local Dispatcher Tools](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/dispatcher-tools.html) to validate dispatcher, before testing in a Cloud Service environment.

## Hands-on exercise

Apply your knowledge by trying out what you learned with this hands-on exercise.

Prior to trying the hands-on exercise, make sure you've watched and understand the video above, and following materials:

+ [AEM Modernization Tools](./aem-modernization-tools.md)
+ [Onboarding](./onboarding.md)
+ [Cloud Manager](./cloud-manager.md)

Also, make sure you have completed the previous hands-on exercise:

+ [Cloud Manager hands-on exercise](./cloud-manager.md#hands-on-exercise)

<table style="border-width:0">
    <tr>
        <td style="width:150px">
            <a  rel="noreferrer"
                target="_blank"
                href="https://github.com/adobe/aem-cloud-engineering-video-series-exercises/tree/session5-dispatcher#cloud-acceleration-bootcamp---session-5-dispatcher"><img alt="Hands-on exercise GitHub repository" src="./assets/github.png"/>
            </a>        
        </td>
        <td style="width:100%;margin-bottom:1rem;">
            <div style="font-size:1.25rem;font-weight:400;">Hands-on with Dispatcher Tools</div>
            <p style="margin:1rem 0">
                Explore using the AEM SDK's Dispatcher Tools to validate Dispatcher configurations as well as running AEM Dispatcher locally using Docker.
            </p>
            <a  rel="noreferrer"
                target="_blank"
                href="https://github.com/adobe/aem-cloud-engineering-video-series-exercises/tree/session5-dispatcher#cloud-acceleration-bootcamp---session-5-dispatcher" class="spectrum-Button spectrum-Button--primary spectrum-Button--sizeM">
                <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Try out Dispatcher Tools</span>
            </a>
        </td>
    </tr>
</table>
