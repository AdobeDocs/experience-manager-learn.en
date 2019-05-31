---
title: Set up Smart Tags with AEM Assets
seo-title: Set up Smart Tags with AEM Assets
description: Provides step by step instructions to configure smart tagging service for AEM Assets.
seo-description: Provides step by step instructions to configure smart tagging service for AEM Assets.
uuid: 8e4619fb-8102-4ce5-8652-511ec70d17a1
products: SG_EXPERIENCEMANAGER/6.3/ASSETS
topic-tags: metadata
topic-tags: search
topic-tags: omnisearch
products: SG_EXPERIENCEMANAGER/6.4/ASSETS
discoiquuid: ccae3a2c-40a8-4441-bd36-230815a4676a
targetaudience: target-audience advanced
---

# Set up Smart Tags with AEM Assets{#set-up-smart-tags-with-aem-assets}

Provides step by step instructions to configure smart tagging service for AEM Assets.

## Smart Tags set up {#smart-tags-set-up}

>[!VIDEO](https://video.tv.adobe.com/v/17023/?quality=9)

>[!NOTE]
>
>Contact your Adobe Account Representative for more information on how to gain access to Smart Tags.

### Here are the key tasks involved in configuring the Smart Tagging cloud service:

* [Creating UPD integration](https://helpx.adobe.com/experience-manager/6-3/assets/using/config-smart-tagging.html#CreatingUDPIntegration)
* [Configuring AEM instance](https://helpx.adobe.com/experience-manager/6-3/assets/using/config-smart-tagging.html#ConfigureAssetsSmartTaggingCloudService)
* Enabling the AEM Smart Tag Assets feature flag
* Configuring the Smart Tagging cloud service in AEM
* Enable auto-tagging in the Update Asset workflow

[Optional Settings](https://helpx.adobe.com/experience-manager/6-3/assets/using/config-smart-tagging.html#OptionalSettings)

* Configuring the DAM Similarity Search service
* Configure Periodic tagging

>[!NOTE]
>
>You require system administrator rights in the Marketing Cloud organization to be able to create UDP integration.

## Showing Smart Tags scores for instructional purposes {#showing-smart-tags-scores-for-instructional-purposes}

A short video illustrating how Smart Tags scores can be displayed in AEM for demo, instructional or explanatory purposes. This is not intended for production use cases as explained in the video.

>[!VIDEO](https://video.tv.adobe.com/v/17768/?quality=9)

This video illustrates how Smart Tags show scores can be enabled to drive conversations around the benefits of Smart Tags and further technical understanding of the effects of confidence scores.

Edit the default metadata schema to create a copy and update the properties

* /conf/global/settings/dam/adminui-extension/metadataschema/default/items/tabs/items/tab1/items/col1/items/autotags@**showConfidenceScore = true**
* /conf/global/settings/dam/adminui-extension/metadataschema/default/items/tabs/items/tab1/items/col1/items/autotags@**fieldLabel = Smart Tags (Prediction Confidence 0-100)**

Overlay the Manage Tags console to /apps

* /libs/dam/gui/content/assets/managetags/jcr:content/body/items/form/items/wizard/items/moderateStep/items/fixedColumns/items/fixedColumn1/items/autotags@**showConfidenceScore = true**

The following adjustments described above are provided in the attached AEM package that can be installed via [AEM Package Manager](http://localhost:4502/crx/packmgr/index.jsp).

Download [Smart Tag Score package](assets/aem63-assets-smarttags-showscores-1.0.0.zip)

## Additional Resources{#additional-resources}

* [AEM Assets Smart Tags documentation](https://helpx.adobe.com/experience-manager/6-3/assets/using/touch-ui-smart-tags.html)
