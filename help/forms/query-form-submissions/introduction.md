---
title: Querying form submission
description: Multi-part tutorial to walk you through the steps involved in querying form submissions stored in Azure portal
feature: Adaptive Forms
doc-type: Tutorial
version: Experience Manager 6.5
topic: Development
role: Developer
level: Experienced
jira: KT-14884
last-substantial-update: 2024-03-03T00:00:00.000Z
exl-id: 08c97626-73a9-43d2-955c-b97fbb5f2e9a
duration: 185
TQID: https://experienceleague.adobe.com/YXa13i0pyQF-Oe20Trr2eRiXYkDu8T52Au14rjVl7w0
product_v2:
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
    internal-label: Data management
---
# Overview of the use case

The following video describes the use case

>[!VIDEO](https://video.tv.adobe.com/v/3427096?learn=on)


To follow this tutorial it is recommended that you have access to the following

* AEM 6.5.20 or above with appropriate forms addon package

* Access to Azure portal storage



If you are a developer and would like to understand the code and other details of this use case implementation, please import this [AEM project in either VSCode or IntelliJ.](assets/azuredemoproject.zip)

If you just want to get this sample working on your local system, please follow the steps mentioned [part5 of this tutorial](./part5.md)

The following steps were involved in creating the solution

* Allow the form authors to mark specific form fields as searchable.
* Store form data and attachments in Azure portal.
* Build a simple form to query form submissions.
* Prefill the queried form with submitted data and attachments.

## Next Steps

[Make fields searchable](./part1.md)
