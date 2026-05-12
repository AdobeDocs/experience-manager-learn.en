---
title: Chapter 6 - Exposing the Content on AEM Publish as JSON - Content Services
description: Chapter 6 of the AEM Headless tutorial covers ensuring all the necessary packages, configuration and content are on AEM Publish to allow consumption from the Mobile App.
feature: Content Fragments, APIs
topic: Headless, Content Management
role: Developer
level: Beginner
doc-type: Tutorial
exl-id: b33d1509-531d-40c3-9b26-1d18c8d86a97
duration: 196
TQID: https://experienceleague.adobe.com/dmJzOdwtwcF9r97KNHJI2v13Xud3A1tohrSXze3YLRI
product_v2:
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: a01bfd36-4ab8-4bf8-9dc0-5b45b890552e
    internal-label: APIs
  - id: e2c1b6d3-bb7e-4fe8-8c72-f7b403298e91
    internal-label: Authoring
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
---
# Chapter 6 - Exposing the Content on AEM Publish for Delivery

Chapter 6 of the AEM Headless tutorial covers ensuring all the necessary packages, configuration and content are on AEM Publish to allow consumption by the Mobile App.

## Publishing the Content for AEM Content Services

The configuration and content created to drive the Events through AEM Content Services must be published to AEM Publish so the Mobile App can access it.

Because AEM Content Services is built from Configuration (Content Fragment Models, Editable Templates), Assets (Content Fragments, Images), and Pages all of these pieces automatically enjoy AEM's content management capabilities, including:

* Workflow for review and processing
* and activation/deactivation for pushing and pulling content from the AEM Publish's AEM Content Services end-points

1. Ensure the **[!DNL WKND Mobile] Application Packages**, listed in [Chapter 1](./chapter-1.md#wknd-mobile-application-packages), are installed on **AEM Publish** using [!UICONTROL Package Manager].
    * [http://localhost:4503/crx/packmgr](http://localhost:4503/crx/packmgr)

1. Publish the **[!DNL WKND Mobile Events API] Editable Template**
    1. Navigate to **[!UICONTROL AEM] > [!UICONTROL Tools] > [!UICONTROL General] > [!UICONTROL Templates] > [!DNL WKND Mobile]**
    1. Select the **[!DNL Event API]** template
    1. Tap **[!UICONTROL Publish]** in the top action bar
    1. Publish the **template** and **all references** (content policies, content policy mappings, and templates)

1. Publish the **[!DNL WKND Mobile Events] content fragments**.

    Note that this is required as the Events API uses the Content Fragment List component, which does not specifically reference Content Fragments.
    
    1. Navigate to **[!UICONTROL AEM] > [!UICONTROL Assets] > [!UICONTROL Files] > [!DNL WKND Mobile] > [!DNL English] > [!DNL Events]**
    1. Select all the **[!DNL Event]** content fragments
    1. Tap the **[!UICONTROL Manage Publication]** in the top action bar
    1. Leaving the default **Publish** action as-is, tap **[!UICONTROL Next]** in the top action bar
    1. Select **all** content fragments
    1. Tap **[!UICONTROL Publish]** in the top action bar
        * *The [!DNL Events] Content Fragment Model and references Event Images will automatically be published along with the content fragments.*

1. Publish the **[!DNL Events API] page**.
    1. Navigate to **[!UICONTROL AEM] > [!UICONTROL Sites] > [!DNL WKND Mobile] > [!DNL English] > [!DNL API]**
    1. Select the **[!DNL Events]** page
    1. Tap the **[!UICONTROL Manage Publication]** in the top action bar
    1. Leaving the default **Publish** action as-is, tap **[!UICONTROL Next]** in the top action bar
    1. Select the **[!DNL Events]** page
    1. Tap **[!DNL Publish]** in the top action bar

>[!VIDEO](https://video.tv.adobe.com/v/28343?quality=12&learn=on)

## Verify AEM Publish

1. In a new Web browser, ensure you are logged out of AEM Publish and request the following URLs (substituting `http://localhost:4503` for whatever host:port AEM Publish is running on).

    * [http://localhost:4503/content/wknd-mobile/en/api/events.model.json](http://localhost:4503/content/wknd-mobile/en/api/events.model.tidy.json)

   These requests should return the same JSON response as when the corresponding AEM Author end-points were reviewed. If they do not, ensure all publications succeeded (check the Replication queues), the [!DNL WKND Mobile] `ui.apps` package is installed on AEM Publish, and review the `error.log` for AEM Publish.

## Next step

There are no extra packages to install. Ensure that the content and configuration outlined in this section is published to AEM Publish, else subsequent chapters will not work.

* [Chapter 7 - Consuming AEM Content Services from a Mobile App](./chapter-7.md)
