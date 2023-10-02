---
title: Integrate AEM Sites and Adobe Analytics with Platform Web SDK
description: Integrate AEM Sites and Adobe Analytics using the modern Platform Web SDK approach.
version: Cloud Service
feature: Integrations
topic: Integrations, Architecture
role: Admin, Architect, Data Architect, Developer
level: Beginner, Intermediate
doc-type: Tutorial
last-substantial-update: 2023-05-25
jira: KT-13328
thumbnail: KT-13328.jpeg
badgeIntegration: label="Integration" type="positive"
badgeVersions: label="AEM Sites as a Cloud Service, AEM Sites 6.5" before-title="false"
exl-id: 0cc3d3bc-e4ea-4ab2-8878-adbcf0c914f5
---
# Integrate AEM Sites and Adobe Analytics with Platform Web SDK

Learn the **modern approach** on how to integrate Adobe Experience Manager (AEM) and Adobe Analytics using the Platform Web SDK. This comprehensive tutorial guides you through the process of seamlessly collecting [WKND](https://github.com/adobe/aem-guides-wknd#aem-wknd-sites-project) pageview and CTA click data. Gain valuable insights by visualizing the collected data in Adobe Analysis Workspace, where you can explore various metrics and dimensions. Also, explore the Platform Dataset to verify and analyze the data. Join us on this journey to harness the power of AEM and Adobe Analytics for data-driven decision-making.

## Overview

Gaining insights into user behavior is a crucial objective for every marketing team. By understanding how users interact with their content, teams can make informed decisions, optimize strategies, and drive better results. The WKND marketing team, a fictional entity, has set its sights on implementing Adobe Analytics on their website to achieve this goal. The primary objective is to collect data on two key metrics: pageviews and homepage call-to-action (CTA) clicks.

By tracking pageviews, the team is able to analyze which pages are receiving the most attention from users. Also, tracking homepage CTA clicks provides valuable insights into the effectiveness of the team's call-to-action elements. This data may reveal which CTAs are resonating with users, which ones need adjustment, and potentially uncover new opportunities to enhance user engagement and drive conversions.


>[!VIDEO](https://video.tv.adobe.com/v/3419872?quality=12&learn=on)

## Prerequisites

The following are required when integrating Adobe Analytics using Platform Web SDK.

You have completed the setup steps from the **[Integrate Experience Platform Web SDK](./web-sdk.md)** tutorial.

In **AEM as Cloud Service**: 
    
+ [AEM Administrator access to AEM as a Cloud Service environment](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/overview.html)
+ Deployment Manager access to Cloud Manager
+ Clone and deploy the [WKND - sample Adobe Experience Manager project](https://github.com/adobe/aem-guides-wknd#aem-wknd-sites-project) to your AEM as a Cloud Service environment.

In **Adobe Analytics**:

+ Access to create **Report Suite**
+ Access to create **Analysis Workspace**

In **Experience Platform**:

+ Access to the default production, **Prod** sandbox.
+ Access to **Schemas** under Data Management
+ Access to **Datasets** under Data Management
+ Access to **Datastreams** under Data Collection
+ Access to **Tags** (formerly known as Launch) under Data Collection

In case you do not have necessary permissions, your system administrator using [Adobe Admin Console](https://adminconsole.adobe.com/) can grant necessary permissions.

Before delving into the integration process of AEM and Analytics using Platform Web SDK, let's _recap the essential components and key elements_ that were established in the [Integrate Experience Platform Web SDK](./web-sdk.md) tutorial. It provides a solid foundation for the integration.

>[!VIDEO](https://video.tv.adobe.com/v/3419873?quality=12&learn=on)

After the recap of the XDM Schema, Datastream, Dataset, Tag property and, AEM and tag property connection, let's embark on the integration journey.

## Define Analytics Solution Design Reference (SDR) document

As part of the implementation process, it is recommended to create a Solution Design Reference (SDR) document. This document plays a crucial role as a blueprint for defining business requirements and designing effective data collection strategies.

The SDR document provides a comprehensive overview of the implementation plan, ensuring that all stakeholders are aligned and understand the objectives and scope of the project.


>[!VIDEO](https://video.tv.adobe.com/v/3419874?quality=12&learn=on)

For more information on concepts and various elements that should be included in the SDR document visit the [Create and maintain a Solution Design Reference (SDR) Document](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/implementation/implementation-basics/creating-and-maintaining-an-sdr.html). You can also download a sample Excel template, however WKND-specific version is also available [here](./assets/Initial-WKND-WebSDK-BRD-SDR.xlsx).

## Set up Analytics - report suite, Analysis Workspace

The first step is to set up Adobe Analytics, specifically report suite with conversion variables (or eVar) and success events. The conversion variables are used to measure cause and effect. The success events are used to track actions. 

In this tutorial,  `eVar5, eVar6, and eVar7` track  _WKND Page Name, WKND CTA ID, and WKND CTA Name_ respectively, and `event7` is used to track  _WKND CTA Click Event_.

To analyze, gather insights and share those insights with others from the collected data, a project in Analysis Workspace is created. 

>[!VIDEO](https://video.tv.adobe.com/v/3419875?quality=12&learn=on)

To learn more about Analytics setup and concepts, the following resources are highly recommended:

+ [Report Suite](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/manage-report-suites/c-new-report-suite/t-create-a-report-suite.html)
+ [Conversion Variables](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/conversion-variables/conversion-var-admin.html)
+ [Success Events](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/conversion-variables/success-events/success-event.html)
+ [Analysis Workspace](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/home.html)

## Update Datastream - Add Analytics Service

A Datastream instructs the Platform Edge Network where to send the collected data. In the [previous tutorial](./web-sdk.md), a Datastream is configured to send the data to the Experience Platform. This Datastream is updated to send the data to the Analytics report suite that was configured in the [above](#setup-analytics---report-suite-analysis-workspace) step.

>[!VIDEO](https://video.tv.adobe.com/v/3419876?quality=12&learn=on)

## Create XDM Schema 

The Experience Data Model (XDM) Schema helps you to standardize the collected data. In the [previous tutorial](./web-sdk.md), an XDM schema with `AEP Web SDK ExperienceEvent` a field group is created. Also, using this XDM schema a Dataset is created to store the collected data in the Experience Platform. 

However, that XDM Schema does not have Adobe Analytics-specific field groups to send the eVar, event data. A new XDM schema is created instead of updating the existing schema to avoid storing the eVar, event data in the platform.

The newly created XDM schema has `AEP Web SDK ExperienceEvent` and `Adobe Analytics ExperienceEvent Full Extension` field groups.

>[!VIDEO](https://video.tv.adobe.com/v/3419877?quality=12&learn=on)


## Update Tag property

In the [previous tutorial](./web-sdk.md), a tag property is created, it has Data Elements and a Rule to gather, map, and send the pageview data. It must be enhanced for:

+ Mapping the page name to `eVar5`
+ Triggering the **pageview** Analytics call ( or send beacon)
+ Gathering CTA data using the Adobe Client Data Layer
+ Mapping the CTA ID and Name to `eVar6` and `eVar7` respectively. Also, the CTA click count to `event7`
+ Triggering the **link click** Analytics call ( or send beacon)


>[!VIDEO](https://video.tv.adobe.com/v/3419882?quality=12&learn=on)

>[!TIP]
>
>The Data Element and Rule-Event code shown in the video is available for your reference, **expand the below accordion element**. However, if you are NOT using Adobe Client Data Layer, you must modify the below code but the concept of defining the Data Elements and using them in the Rule definition still applies.

+++ Data Element and Rule-Event Code

+   The `Component ID` Data Element code.

    ```javascript
    if(event && event.path && event.path.includes('.')) {    
        // split on the `.` to return just the component ID for e.g. button-06bc532b85, tabs-bb27f4f426-item-cc9c2e6718
        return event.path.split('.')[1];
    }else {
        //return dummy ID
        return "WKND-CTA-ID";
    }
    ```

+   The `Component Name` Data Element code.

    ```javascript
    if(event && event.component && event.component.hasOwnProperty('dc:title')) {
        // Return the Button, Link, Image, Tab name, for e.g. View Trips, Full Article, See Trips
        return event.component['dc:title'];
    }else {
        //return dummy ID
        return "WKND-CTA-Name";    
    }    
    ```

+   The `all pages - on load` **Rule-Condition** code

    ```javascript
    if(event && event.component && event.component.hasOwnProperty('@type') && event.component.hasOwnProperty('xdm:template')) {
        return true;
    }else{
        return false;
    }    
    ```

+   The `home page - cta click` **Rule-Event** code

    ```javascript
    var componentClickedHandler = function(evt) {
    // defensive coding to avoid a null pointer exception
    if(evt.hasOwnProperty("eventInfo") && evt.eventInfo.hasOwnProperty("path")) {
        //trigger Tag Rule and pass event
        console.log("cmp:click event: " + evt.eventInfo.path);
        
        var event = {
            //include the path of the component that triggered the event
            path: evt.eventInfo.path,
            //get the state of the component that triggered the event
            component: window.adobeDataLayer.getState(evt.eventInfo.path)
        };

        //Trigger the Tag Rule, passing in the new `event` object
        // the `event` obj can now be referenced by the reserved name `event` by other Tag Property data elements
        // i.e `event.component['someKey']`
        trigger(event);
    }
    }

    //set the namespace to avoid a potential race condition
    window.adobeDataLayer = window.adobeDataLayer || [];
    //push the event listener for cmp:click into the data layer
    window.adobeDataLayer.push(function (dl) {
    //add event listener for `cmp:click` and callback to the `componentClickedHandler` function
    dl.addEventListener("cmp:click", componentClickedHandler);
    });    
    ```

+   The `home page - cta click` **Rule-Condition** code    

    ```javascript
    if(event && event.component && event.component.hasOwnProperty('@type')) {
        //Check for Button Type OR Teaser CTA type
        if(event.component['@type'] === 'wknd/components/button' ||
        event.component['@type'] === 'wknd/components/teaser/cta') {
            return true;
        }
    }

    // none of the conditions are met, return false
    return false;    
    ```

+++

For additional information on integrating AEM Core Components with Adobe Client Data Layer, refer to the [Using the Adobe Client Data Layer with AEM Core Components guide](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/adobe-client-data-layer/data-layer-overview.html).


>[!INFO]
>
>For a comprehensive understanding of the **Variable Map** tab property details in the Solution Design Reference (SDR) document, access the completed WKND-specific version for download [here](./assets/Final-WKND-WebSDK-BRD-SDR.xlsx). 



## Verify updated Tag property on WKND

To ensure that the updated tag property is built, published, and working correctly on the WKND site pages. Use the Google Chrome web browser's [Adobe Experience Platform Debugger extension](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob):

+   To ensure that the tag property is the latest version, check the build date. 

+   To verify the XDM event data for both PageView and HomePage CTA Click, use the Experience Platform Web SDK menu option within the extension. 

>[!VIDEO](https://video.tv.adobe.com/v/3419883?quality=12&learn=on)

## Simulate web traffic - Selenium automation

To generate a meaningful amount of traffic for testing purposes, a Selenium automation script is developed. This custom script simulates user interactions with the WKND website like page view and clicking CTAs. 

>[!VIDEO](https://video.tv.adobe.com/v/3419884?quality=12&learn=on)

## Dataset verification - WKND pageview, CTA data 

The dataset is a storage and management construct for a collection of data like a database table that follows a schema. The Dataset created in the [previous tutorial](./web-sdk.md) is reused to verify that the pageview and CTA click data is ingested into the Experience Platform Dataset. Within the Dataset UI, various details such as total records, size, and ingested batches are displayed along with a visually appealing bar graph.

>[!VIDEO](https://video.tv.adobe.com/v/3419885?quality=12&learn=on)

## Analytics - WKND pageview, CTA data visualization

Analysis Workspace is a powerful tool within Adobe Analytics that allows to explore and visualize data in a flexible and interactive manner. It provides a drag-and-drop interface to create custom reports, perform advanced segmentation, and apply various data visualizations.

Let's reopen the Analysis Workspace project created in the [Setup Analytics](#setup-analytics---report-suite-analysis-workspace) step. In the **Top Pages** section, examine various metrics such as visits, unique visitors, entries, bounce rate, and more. To assess the performance of WKND pages and home page CTAs, drag-and-drop the WKND-specific dimensions (WKND Page Name, WKND CTA Name) and metrics (WKND CTA Click Event). These insights are valuable for marketers to understand which CTAs are more effective and make data-driven decisions, aligned with their business objectives. 

To visualize user journeys, use the Flow visualization, starting with the **WKND Page Name** and expanding into various paths.

>[!VIDEO](https://video.tv.adobe.com/v/3419886?quality=12&learn=on)

## Summary 

Great job! You have completed the setup of AEM and Adobe Analytics using Platform Web SDK to collect, analyze the pageview and CTA click data. 

Implementing Adobe Analytics is crucial for marketing teams to gain insights into user behavior, make informed decisions, enabling them to optimize their content and make data-driven decisions. 

By implementing the recommended steps and using the provided resources, such as the Solution Design Reference (SDR) document and understanding key Analytics concepts, marketers can effectively collect and analyze data.

>[!VIDEO](https://video.tv.adobe.com/v/3419888?quality=12&learn=on)


>[!AVAILABILITY]
>
>If you prefer the **end-to-end video** that covers the entire integration process instead of individual setup step videos, you can click [here](https://video.tv.adobe.com/v/3419889/) to access it.


## Additional Resources

+ [Integrate Experience Platform Web SDK](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform/web-sdk.html)
+ [Using the Adobe Client Data Layer with the Core Components](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/adobe-client-data-layer/data-layer-overview.html)
+ [Integrating Experience Platform Data Collection Tags and AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-data-collection-tags/overview.html)
+ [Adobe Experience Platform Web SDK and Edge Network overview](https://experienceleague.adobe.com/docs/platform-learn/data-collection/web-sdk/overview.html)
+ [Data Collection tutorials](https://experienceleague.adobe.com/docs/platform-learn/data-collection/overview.html)
+ [Adobe Experience Platform Debugger overview](https://experienceleague.adobe.com/docs/platform-learn/data-collection/debugger/overview.html)
