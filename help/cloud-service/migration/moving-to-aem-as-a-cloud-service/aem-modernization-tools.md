---
title: Using AEM Modernization Tools for moving to AEM as a Cloud Service
description: Learn how AEM Modernization Tools are used to upgrade an existing AEM project and content to be AEM as a Cloud Service compatible.
version: Cloud Service
topic: Migration, Upgrade
feature: Migration
role: Developer
level: Experienced
jira: KT-8629
thumbnail: 336965.jpeg
exl-id: 310f492c-0095-4015-81a4-27d76f288138
duration: 2545
---

# AEM Modernization Tools

Learn how AEM Modernization Tools are used to upgrade an existing AEM Sites content to be AEM as a Cloud Service compatible and align with best practices.

## All-in-One Converter

>[!VIDEO](https://video.tv.adobe.com/v/338802?quality=12&learn=on)

## Page conversion

>[!VIDEO](https://video.tv.adobe.com/v/338799?quality=12&learn=on)

## Component conversion

>[!VIDEO](https://video.tv.adobe.com/v/338788?quality=12&learn=on)

## Policy import

>[!VIDEO](https://video.tv.adobe.com/v/338797?quality=12&learn=on)

## Using AEM Modernization Tools

![AEM Modernization Tools lifecycle](./assets/aem-modernization-tools.png)

AEM Modernization tools automatically convert existing AEM Pages composed of legacy static templates, foundation components, and the parsys - to use modern approaches such as editable templates, AEM Core WCM Components, and Layout Containers.

## Key activities

+ Clone AEM 6.x production to run AEM Modernization tools against
+ Download and install the [latest AEM Modernizations tools](https://github.com/adobe/aem-modernize-tools/releases/latest) on the AEM 6.x production clone via Package Manager

+ [Page Structure Converter](https://opensource.adobe.com/aem-modernize-tools/pages/structure/about.html) updates existing page content from static template to a mapped editable template using layout containers
  + Define conversion rules using OSGi configuration
  + Run Page Structure Converter against existing pages

+ [Component Converter](https://opensource.adobe.com/aem-modernize-tools/pages/component/about.html) updates existing page content from static template to a mapped editable template using layout containers
  + Define conversion rules via JCR node definitions/XML
  + Run the Component Converter tool against existing pages
  
+ [Policy Importer](https://opensource.adobe.com/aem-modernize-tools/pages/policy/about.html) creates policies from Design configuration
  + Define conversion rules using JCR node definitions/XML
  + Run Policy Importer against existing Design definitions
  + Apply imported policies to AEM components and containers

## Hands-on exercise

Apply your knowledge by trying out what you learned with this hands-on exercise.

Prior to trying the hands-on exercise, make sure you've watched and understand the video above, and following materials:

+ [Thinking differently about AEM as a Cloud Service](./introduction.md)
+ [Repository modernization](./repository-modernization.md)
+ [Mutable and immutable content](../../developing/basics/mutable-immutable.md)
+ [AEM project structure](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html)

Also, make sure you have completed the previous hands-on exercise:

+ [BPA and CAM hands-on exercise](./bpa-and-cam.md#hands-on-exercise)

<table style="border-width:0">
    <tr>
        <td style="width:150px">
            <a  rel="noreferrer"
                target="_blank"
                href="https://github.com/adobe/aem-cloud-engineering-video-series-exercises/tree/session2-migration#bootcamp---session-2-migration-methodology"><img alt="Hands-on exercise GitHub repository" src="./assets/github.png"/>
            </a>        
        </td>
        <td style="width:100%;margin-bottom:1rem;">
            <div style="font-size:1.25rem;font-weight:400;">Hands-on with AEM modernization</div>
            <p style="margin:1rem 0">
                Explore using AEM Modernization Tools to update a legacy WKND site to conform with AEM as a Cloud Service best practices.
            </p>
            <a  rel="noreferrer"
                target="_blank"
                href="https://github.com/adobe/aem-cloud-engineering-video-series-exercises/tree/session2-migration#bootcamp---session-2-migration-methodology" class="spectrum-Button spectrum-Button--primary spectrum-Button--sizeM">
                <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Try out the AEM Modernization Tools</span>
            </a>
        </td>
    </tr>
</table>

## Other resources

+ [Download AEM Modernizations tools](https://github.com/adobe/aem-modernize-tools/releases/latest)
+ [AEM Modernization Tools documentation](https://opensource.adobe.com/aem-modernize-tools/)
+ [AEM Gems - Introducing the AEM Modernization Suite](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/Introducing-the-AEM-Modernization-Suite.html)

1. Deploy the newly modernized wknd-legacy site on the local AEM SDK. AEM ASK available for download here: 
    + [Software Distribution Portal](https://experience.adobe.com/#/downloads/content/software-distribution/en/general.html). 
