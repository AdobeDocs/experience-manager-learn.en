---
title: Storing and Retrieving Form Data with attachments from MySQL Database
description: Multi-Part tutorial to walk you through the steps involved in storing and retrieving form data with attachments
feature: Adaptive Forms
type: Tutorial
version: Experience Manager 6.4, Experience Manager 6.5
jira: KT-6593
thumbnail: 327122.jpg
topic: Development
role: Developer
level: Experienced
exl-id: b278652f-6c09-4abc-b92e-20bfaf2e791a
last-substantial-update: 2020-11-07T00:00:00.000Z
duration: 148
TQID: 'https://experienceleague.adobe.com/SW6dxCPYUqeFlWiqfDfyJXi9H-y-9FpbAQCg6IzUuso'
product_v2:
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: 4876a742-a341-5402-aba7-e749c45e777c
    internal-label: Form Data Model
  - id: a01bfd36-4ab8-4bf8-9dc0-5b45b890552e
    internal-label: APIs
  - id: f013e6ab-27b8-4645-b5a7-31ffa474d04f
    internal-label: APIs
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
---
# Storing and Retrieving Adaptive Form Data with 2FA

This tutorial will walk you through the steps involved in saving and retrieving Adaptive Form Data with attachments using 2FA. This tutorial used MySQL database to store Adaptive Form data. Database of your choice can be used to store the data as long as you have deployed the database specific drivers in AEM. At a high-level, the following steps are needed to achieve the use case:

* Use the GuideBridge API get access to the Adaptive Form data

* Make a POST call to a servlet. This servlet stores the data in the database and the form attachments in the CRX repository. The stored data in the database is associated with a GUID.

* When you want to populate the Adaptive Form with the stored data, you retrieve the data associated with the GUID and populate the Adaptive Form using the **request.setAttribute** method.

## Demonstration of the use case

>[!VIDEO](https://video.tv.adobe.com/v/327122?quality=12&learn=on)

## Prerequisites

The audience of this content is expected to have some experience in the following areas:

* Adaptive Form
* Form Data Model
* OSGi services/components
* AEM Client Libraries


## Next Steps

[Configuring Data Source](./configure-data-source.md)