---
title: Integrate AEM Sites and Experience Platform Web SDK
description: Learn how to integrate AEM Sites as a Cloud Service with Experience Platform Web SDK. This foundational step is essential for integrating Adobe Experience Cloud products, such as Adobe Analytics, Target, or recent innovative products like Real-Time Customer Data Platform, Customer Journey Analytics, and  Journey Optimizer.
version: Cloud Service
feature: Integrations
topic: Integrations, Architecture
role: Admin, Architect, Data Architect, Developer
level: Beginner, Intermediate
doc-type: Tutorial
last-substantial-update: 2023-04-26
jira: KT-13156
thumbnail: KT-13156.jpeg
badgeIntegration: label="Integration" type="positive"
badgeVersions: label="AEM Sites as a Cloud Service" before-title="false"
exl-id: b5182d35-ec38-4ffd-ae5a-ade2dd3f856d
---
# Integrate AEM Sites and Experience Platform Web SDK

Learn how to integrate AEM as a Cloud Service with Experience Platform [Web SDK](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html). This foundational step is essential for integrating Adobe Experience Cloud products, such as Adobe Analytics, Target, or recent innovative products like Real-Time Customer Data Platform, Customer Journey Analytics, and Journey Optimizer.

You also learn how to collect and send [WKND - sample Adobe Experience Manager project](https://github.com/adobe/aem-guides-wknd#aem-wknd-sites-project) pageview data in the [Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/landing/home.html).

After completing this setup, you have implemented a solid foundation. Also, you are ready to advance the Experience Platform implementation using applications like [Real-Time Customer Data Platform (Real-Time CDP)](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/overview.html), [Customer Journey Analytics (CJA)](https://experienceleague.adobe.com/docs/customer-journey-analytics.html), and [Adobe Journey Optimizer (AJO)](https://experienceleague.adobe.com/docs/journey-optimizer.html). The advanced implementation helps to drive a better customer engagement by standardizing the web and customer data.

## Prerequisites

The following are required when integrating Experience Platform Web SDK.

In **AEM as Cloud Service**: 
    
+ AEM Administrator access to AEM as a Cloud Service environment
+ Deployment Manager access to Cloud Manager
+ Clone and deploy the [WKND - sample Adobe Experience Manager project](https://github.com/adobe/aem-guides-wknd#aem-wknd-sites-project) to your AEM as a Cloud Service environment.

In **Experience Platform**:

+ Access to the default production, **Prod** sandbox.
+ Access to **Schemas** under Data Management
+ Access to **Datasets** under Data Management
+ Access to **Datastreams** under Data Collection
+ Access to **Tags** (formerly known as Launch) under Data Collection

In case you do not have necessary permissions, your system administrator using [Adobe Admin Console](https://adminconsole.adobe.com/) can grant necessary permissions.

>[!VIDEO](https://video.tv.adobe.com/v/3418856?quality=12&learn=on)

## Create XDM Schema - Experience Platform

The Experience Data Model (XDM) Schema helps you to standardize the customer experience data. To collect the **WKND pageview** data, create an XDM Schema and use the Adobe provided field groups `AEP Web SDK ExperienceEvent` for web data collection.

There are generic and industries specific for example Retail, Financial Services, Healthcare, and more, suite of reference data models, see [Industry data models overview](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/industries/overview.html) for more information.


>[!VIDEO](https://video.tv.adobe.com/v/3418894?quality=12&learn=on)

Learn about XDM Schema and related concepts such as field groups, types, classes, and data types from [XDM System overview](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html).

The [XDM System overview](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html) is a great resource to learn about XDM Schema and related concepts such as field groups, types, classes, and data types. It provides a comprehensive understanding of the XDM data model and how to create and manage XDM schemas to standardize data across the enterprise. Explore it to gain a deeper understanding of the XDM schema and how it can benefit your data collection and management processes.

## Create Datastream - Experience Platform

A Datastream instructs the Platform Edge Network where to send the collected data. For example, it can be sent to Experience Platform or Analytics, or Adobe Target.


>[!VIDEO](https://video.tv.adobe.com/v/3418895?quality=12&learn=on)

Familiarize yourself with the concept of Datastreams and related topics such as data governance and configuration by visiting the [Datastreams overview](https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/overview.html) page.

## Create Tag property - Experience Platform

Learn how to create a tag (formerly known as Launch) property in Experience Platform to add the Web SDK JavaScript library to the WKND website. The newly defined tag property has following resources:

+ Tag Extensions: [Core](https://exchange.adobe.com/apps/ec/100223/adobe-launch-core-extension) and [Adobe Experience Platform Web SDK](https://exchange.adobe.com/apps/ec/106387/aep-web-sdk)
+ Data Elements: The data elements of custom code type that extract page-name, site-section, and host-name using WKND site's Adobe Client Data Layer. Also, the XDM Object type data element that complies with newly created WKND XDM schema build-in earlier [Create XDM Schema](#create-xdm-schema---experience-platform) step.
+ Rule: Send data to Platform Edge Network whenever a WKND webpage is visited using the Adobe Client Data Layer triggered `cmp:show` event.

While building and publishing the tag library using the **Publishing Flow**, you can use the **Add All Changed Resources** button. To select all the resources like Data Element, Rule, and Tag Extensions instead of identifying and picking an individual resource. Also, during the development phase, you can publish the library just to the _Development_ environment, then verify and promote it to the _Stage_ or _Production_ environment.

>[!VIDEO](https://video.tv.adobe.com/v/3418896?quality=12&learn=on)


>[!TIP]
>
>The Data Element and Rule-Event code shown in the video is available for your reference, **expand the below accordion element**. However, if you are NOT using Adobe Client Data Layer, you must modify the below code but the concept of defining the Data Elements and using them in the Rule definition still applies.


+++ Data Element and Rule-Event Code

+   The `Page Name` Data Element code.

    ```javascript
    if(event && event.component && event.component.hasOwnProperty('dc:title')) {
        // return value of 'dc:title' from the data layer Page object, which is propogated via 'cmp:show` event
        return event.component['dc:title'];
    }
    ```

+   The `Site Section` Data Element code.

    ```javascript
    if(event && event.component && event.component.hasOwnProperty('repo:path')) {
    let pagePath = event.component['repo:path'];
    
    let siteSection = '';
  
    //Check of html String in URL.
    if (pagePath.indexOf('.html') > -1) { 
     siteSection = pagePath.substring(0, pagePath.lastIndexOf('.html'));

     //replace slash with colon
     siteSection = siteSection.replaceAll('/', ':');
     
     //remove `:content`
     siteSection = siteSection.replaceAll(':content:','');
    }
    
        return siteSection 
    }
    ```

+   The `Host Name` Data Element code.

    ```javascript
    if(window && window.location && window.location.hostname) {
        return window.location.hostname;
    }
    ```

+   The `all pages - on load` Rule-Event code

    ```javascript
    var pageShownEventHandler = function(evt) {
    // defensive coding to avoid a null pointer exception
    if(evt.hasOwnProperty("eventInfo") && evt.eventInfo.hasOwnProperty("path")) {
        //trigger Launch Rule and pass event
        console.debug("cmp:show event: " + evt.eventInfo.path);
        var event = {
            //include the path of the component that triggered the event
            path: evt.eventInfo.path,
            //get the state of the component that triggered the event
            component: window.adobeDataLayer.getState(evt.eventInfo.path)
        };

        //Trigger the Launch Rule, passing in the new 'event' object
        // the 'event' obj can now be referenced by the reserved name 'event' by other Launch data elements
        // i.e 'event.component['someKey']'
        trigger(event);
        }
    }

    //set the namespace to avoid a potential race condition
    window.adobeDataLayer = window.adobeDataLayer || [];

    //push the event listener for cmp:show into the data layer
    window.adobeDataLayer.push(function (dl) {
        //add event listener for 'cmp:show' and callback to the 'pageShownEventHandler' function
        dl.addEventListener("cmp:show", pageShownEventHandler);
    });
    ```
    
+++


The [Tags overview](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html) provides in-depth knowledge about important concepts such as Data Elements, Rules, and Extensions. 

For additional information on integrating AEM Core Components with Adobe Client Data Layer, refer to the [Using the Adobe Client Data Layer with AEM Core Components guide](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/adobe-client-data-layer/data-layer-overview.html).

## Connect Tag property to AEM

Discover how to link the recently created tag property to AEM through Adobe IMS and Adobe Launch Configuration in AEM. When an AEM as a Cloud Service environment is established, several Adobe IMS Technical Account configurations are automatically generated, including Adobe Launch. However, for AEM 6.5 version, you must configure one manually.

After linking the tag property, the WKND site is able to load the tag property's JavaScript library onto the web pages using the Adobe Launch cloud service configuration.

### Verify Tag property loading on WKND 

Using Adobe Experience Platform Debugger [Chrome](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob) or [Firefox](https://addons.mozilla.org/en-US/firefox/addon/adobe-experience-platform-dbg/) extension, verify if the tag property is loading on WKND pages. You can verify,

+ Tag property details such as extension, version, name and more.
+ Platform Web SDK library version, Datastream ID
+ XDM Object as part `events` attribute in Experience Platform Web SDK

>[!VIDEO](https://video.tv.adobe.com/v/3418897?quality=12&learn=on)

## Create Dataset - Experience Platform

The pageview data collected using Web SDK is stored in Experience Platform data lake as datasets. The dataset is a storage and management construct for a collection of data like a database table that follows a schema. Learn how to create a Dataset and configure the earlier created Datastream to send data to the Experience Platform.


>[!VIDEO](https://video.tv.adobe.com/v/3418898?quality=12&learn=on)

The [Datasets overview](https://experienceleague.adobe.com/docs/experience-platform/catalog/datasets/overview.html) provides more information on concepts, configurations, and other ingestion capabilities.


## WKND pageview data in Experience Platform

After the setup of the Web SDK with AEM, particularly on the WKND site, it's time to generate traffic by navigating through the site pages. Then confirm that the pageview data is being ingested into the Experience Platform Dataset. Within the Dataset UI, various details such as total records, size, and ingested batches are displayed along with a visually appealing bar graph.

>[!VIDEO](https://video.tv.adobe.com/v/3418899?quality=12&learn=on)


## Summary 

Great job! You have completed the setup of AEM with Experience Platform Web SDK to collect and ingest data from a website. With this foundation, you can now explore further possibilities to enhance and integrate products like Analytics, Target, Customer Journey Analytics (CJA), and many others to create rich, personalized experiences for your customers. Keep learning and exploring to unleash the full potential of Adobe Experience Cloud.

>[!VIDEO](https://video.tv.adobe.com/v/3418900?quality=12&learn=on)


>[!AVAILABILITY]
>
>If you prefer the **end-to-end video** that covers the entire integration process instead of individual setup step videos, you can click [here](https://video.tv.adobe.com/v/3418905/) to access it.

## Additional Resources

+ [Using the Adobe Client Data Layer with the Core Components](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/adobe-client-data-layer/data-layer-overview.html)
+ [Integrating Experience Platform Data Collection Tags and AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-data-collection-tags/overview.html)
+ [Adobe Experience Platform Web SDK and Edge Network overview](https://experienceleague.adobe.com/docs/platform-learn/data-collection/web-sdk/overview.html)
+ [Data Collection tutorials](https://experienceleague.adobe.com/docs/platform-learn/data-collection/overview.html)
+ [Adobe Experience Platform Debugger overview](https://experienceleague.adobe.com/docs/platform-learn/data-collection/debugger/overview.html)
