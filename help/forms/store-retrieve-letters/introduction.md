---
title: Save and resume letters
description: Learn how to save and retrieve draft letters
feature: Interactive Communication
doc-type: article
version: Experience Manager 6.5
topic: Development
role: Developer
level: Intermediate
jira: KT-10208
exl-id: e032070b-7332-4c2f-97ee-7e887a61aa7a
last-substantial-update: 2022-01-07T00:00:00.000Z
duration: 160
TQID: https://experienceleague.adobe.com/5QsUKUrLAlGDDoJzKycXQPCx-NE9NIPU06AwjErrm-s
product_v2:
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
    internal-label: Metadata
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
---
# Introduction

Interactive Communications allow the agents prepraing ad-hoc correspondences to save partially completed correspondences and retrieve the same to continue working. AEM Forms provides you the [Service Provider Interface](https://developer.adobe.com/experience-manager/reference-materials/6-5/forms/javadocs/com/adobe/fd/ccm/ccr/ccrDocumentInstance/api/services/CCRDocumentInstanceService.html). The customer is expected to implement this interface to get the Save and Resume functionality.

This article uses MySQL database to store the metadata of the letter instance. The letter data is stored on the file system.

The following video demonstrates the use case:

>[!VIDEO](https://video.tv.adobe.com/v/342129?quality=12&learn=on)

## Prequisites

You will need the following to implement the solution to meet your needs

* Working experience with AEM Forms
* AEM Server 6.5 with Forms Add on
* Should be familiar in building OSGI bundles
