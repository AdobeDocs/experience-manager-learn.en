---
title: Storing and Retrieving Form Data from MySQL Database Introduction
description: Multi-Part tutorial to walk you through the steps involved in storing and retrieving form data
feature: Adaptive Forms
type: Tutorial
version: Experience Manager 6.4, Experience Manager 6.5
topic: Development
role: Developer
level: Experienced
exl-id: 95795102-4278-4556-8e0f-1b8a359ab093
last-substantial-update: 2019-07-07T00:00:00.000Z
duration: 236
TQID: https://experienceleague.adobe.com/CYza1ebxfjD8yBJouuHJvWi8hY9wUr3fgYEHPZphtw0
product_v2:
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
---
# Storing and Retrieving Adaptive Form Data from MySQL Database

This tutorial will walk you through the steps involved in saving and retrieving Adaptive Form Data from Database. This tutorial used MySQL database to store Adaptive Form data. Database of your choice can be used to store the data as long as you have deployed the database specific drivers in AEM. At a high-level, the following steps are needed to achieve the use case:

* Use the GuideBridge API get access to the Adaptive Form data

* Make a POST call to a servlet. This servlet stores the data in the database. The stored data is associated with a GUID

* When you want to populate the Adaptive Form with the stored data, you retrieve the data associated with the GUID and populate the Adaptive Form using the **request.setAttribute** method.

## Demonstration of the use case

>[!VIDEO](https://video.tv.adobe.com/v/27829?quality=12&learn=on)


