---
title: Debugging a Tags implementation
description: An introduction to some common tools and techniques to debug a Tags implementation. Learn how to use the browser's developer console and the Experience Platform Debugger extension to identify and troubleshoot key aspects of a Tags implementation.
solution: Experience Manager, Data Collection, Experience Platform
jira: KT-6047
thumbnail: 38567.jpg
topic: Integrations
feature: Integrations
role: Developer
level: Intermediate
badgeIntegration: label="Integration" type="positive"
badgeVersions: label="AEM Sites as a Cloud Service, AEM Sites 6.5" before-title="false"
doc-type: Tutorial
exl-id: 647447ca-3c29-4efe-bb3a-d3f53a936a2a
duration: 259
TQID: 'https://experienceleague.adobe.com/fMnRgfOZgLaGgHWCk2bzA0qZlXNu7k-O4TIoTogcwgY'
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
    internal-label: Experience Platform
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: ae478996-b206-4712-9b0c-dc78a2644453
    internal-label: Integrations
  - id: daec7ead-f475-492a-a3b3-02ae08565d6f
    internal-label: ''
  - id: e08599ea-8888-4294-ba74-3ba0a7762a46
    internal-label: Data collection tags
  - id: ed0d8d0e-04b9-4326-be72-a0fbca265377
    internal-label: ''
  - id: f2d27a5f-0d67-4d85-8a24-86a8d8a3574b
    internal-label: Developer tools
  - id: 000dc7ac-a6c3-564d-bf22-5080bf496cc2
    internal-label: Tags
  - id: 33ca0c14-7e3b-55a1-8fd7-8a61b47da4e1
    internal-label: B2B
  - id: 8d89a9fb-a98a-500a-ae8d-4d99599b4f3f
    internal-label: Data Collection
  - id: a50ad69b-1331-40e9-b634-531a085a6a54
    internal-label: Identities
  - id: abc02dd6-664f-446a-9aaa-675bc0f2fe4a
    internal-label: Sources
  - id: fab83459-d777-48a3-933c-16a15046f707
    internal-label: Debugger
subfeature_v2:
  - id: cdd3e38b-fec2-4f39-8b10-83ddaab1ac16
    internal-label: ''
  - id: d9830f6f-ceb6-4faa-9744-f281fe4439f9
    internal-label: ''
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
  - id: d3cdead0-685a-4489-9250-4bb709942f66
    internal-label: Data collection
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
    internal-label: Insights
---
# Debugging a Tags implementation {#debug-tags-implementation}

An introduction to common tools and techniques used to debug a Tags implementation. Learn how to use the browser's developer console and the Experience Platform Debugger extension to identify and troubleshoot key aspects of a Tags implementation.

>[!VIDEO](https://video.tv.adobe.com/v/38567?quality=12&learn=on)

## Client-side debugging via Satellite object

The client-side debugging is helpful to verify Tag property rule loading or order of execution. Whenever a Tag property is added to the website, the `_satellite` JavaScript object is present in the browser to facilitate the client-side event and data tracking.

To enable the client-side debugging, call the `setDebug(true)` method on the `_satellite` object.

1.  Open the browser console, and run below command.

    ```javascript
        _satellite.setDebug(true);
    ```

1.  Reload the AEM site page, and verify console log shows _rule fired_ message like below.

    ![Tag Property on Author and Publish Pages](assets/satellite-object-debugging.png)

## Debugging via Adobe Experience Platform Debugger 

Adobe provides Adobe Experience Platform Debugger [Chrome extension](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob) to debug, understand, and get insight into the integration.

1.  Open the Adobe Experience Platform Debugger extension and open the site page on the Publish instance

2.  In the **Adobe Experience Platform Debugger > Summary > Adobe Experience Platform Tags** section, verify your Tag property details such as Name, Version, Build Date, Environment, and Extensions.

    ![Adobe Experience Platform Debugger and Tag Property Details](assets/tag-property-details.png)

## Additional Resources {#additional-resources}

+   [Introduction to the Adobe Experience Platform Debugger](https://experienceleague.adobe.com/docs/platform-learn/data-collection/debugger/overview.html)

+   [Satellite object reference](https://experienceleague.adobe.com/docs/experience-platform/tags/client-side/satellite-object.html)
