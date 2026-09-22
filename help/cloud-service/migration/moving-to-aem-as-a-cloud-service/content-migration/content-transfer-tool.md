---
title: Content Migration using Content Transfer Tool
description: Learn how Content Transfer Tool helps you migrate content to AEM as a Cloud Service from AEM 6.
version: Experience Manager as a Cloud Service
topic: Migration, Upgrade
feature: Migration
role: Developer
level: Experienced
jira: KT-8919
thumbnail: 336970.jpeg
exl-id: c51ce8e3-e83c-4f8b-a835-70335ed3a5b9
duration: 1362
TQID: 'https://experienceleague.adobe.com/PH59UsmFp3OSlnRFFEWeDvNyWudd0owH3P1XZ5hc3Hg'
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: 2741637d-a621-529a-b21b-bfe9be07a9c8
    internal-label: Dispatcher
  - id: 5be0fc8f-1cff-5c3e-bb92-2903a56a3de6
    internal-label: Migration
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
    internal-label: Metadata
---
# Content Transfer Tool

Learn how Content Transfer Tool helps you migrate content to AEM as a Cloud Service from AEM 6.3+.

>[!VIDEO](https://video.tv.adobe.com/v/336970?quality=12&learn=on)

## Using the Content Transfer Tool

![Content Transfer Tool lifecycle](../assets/content-transfer-tool.png)

The Content Transfer Tool is installed on AEM 6.3+ and transfers content to AEM as a Cloud Service.

## Key activities

+ Download the [latest Content Transfer Tool](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?fulltext=Content*+Transfer*+Tool*&1_group.propertyvalues.property=.%2Fjcr%3Acontent%2Fmetadata%2Fdc%3AsoftwareType&1_group.propertyvalues.operation=equals&1_group.propertyvalues.0_values=software-type%3Atooling&orderby=%40jcr%3Acontent%2Fjcr%3AlastModified&orderby.sort=desc&layout=list&p.offset=0&p.limit=2).
+ Transfer AEM Author 6.3+ final content to AEM as a Cloud Service Author service.
  + Install the Content Transfer Tool on AEM 6.3+ Author containing the final content to transfer.
  + Run the Content Transfer Tool in batches, transferring sets of content.
+ Transfer AEM Publish 6.3+ final content to AEM as a Cloud Service Publish service.
  + Install the Content Transfer Tool on AEM 6.3+ Publish containing the final content to transfer.
  + Run the Content Transfer Tool in batches, transferring sets of content.
+ Optionally, "top-up" content on AEM as a Cloud Service, by transferring new content since the last content transfer

## Hands-on exercise

Apply your knowledge by trying out what you learned with this hands-on exercise.

Prior to trying the hands-on exercise, make sure you've watched and understand the video above, and following materials:

+ [AEM Modernization Tools](../aem-modernization-tools.md)
+ [Onboarding](../onboarding.md)
+ [Cloud Manager](../cloud-manager.md)

Also, make sure you have completed the previous hands-on exercise:

+ [Dispatcher hands-on exercise](../dispatcher.md#hands-on-exercise)

<table style="border-width:0">
    <tr>
        <td style="width:150px">
            <a  rel="noreferrer"
                target="_blank"
                href="https://github.com/adobe/aem-cloud-engineering-video-series-exercises/tree/session6-transfercontent#cloud-acceleration-bootcamp---session-6-content"><img alt="Hands-on exercise GitHub repository" src="../assets/github.png"/>
            </a>        
        </td>
        <td style="width:100%;margin-bottom:1rem;">
            <div style="font-size:1.25rem;font-weight:400;">Hands-on with Content Transfer Tool</div>
            <p style="margin:1rem 0">
                Explore how the Content Transfer Tool can automatically move content from AEM 6 to AEM as a Cloud Service.
            </p>
            <a  rel="noreferrer"
                target="_blank"
                href="https://github.com/adobe/aem-cloud-engineering-video-series-exercises/tree/session6-transfercontent#cloud-acceleration-bootcamp---session-6-content" class="spectrum-Button spectrum-Button--primary spectrum-Button--sizeM">
                <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Try out Content Transfer Tool</span>
            </a>
        </td>
    </tr>
</table>

## Other resources

+ [Download Content Transfer Tool](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?fulltext=Content*+Transfer*+Tool*&1_group.propertyvalues.property=.%2Fjcr%3Acontent%2Fmetadata%2Fdc%3AsoftwareType&1_group.propertyvalues.operation=equals&1_group.propertyvalues.0_values=software-type%3Atooling&orderby=%40jcr%3Acontent%2Fjcr%3AlastModified&orderby.sort=desc&layout=list&p.offset=0&p.limit=2)
+ [Bulk Import Service how-to video](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/migration/bulk-import.html)

