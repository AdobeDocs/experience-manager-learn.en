---
title: Save and resume letters
description: Learn how to save and retrieve draft letters
feature: Interactive Communication
doc-type: article
version: 6.5
topic: Development
role: Developer
level: Intermediate
jira: KT-10208
exl-id: e032070b-7332-4c2f-97ee-7e887a61aa7a
last-substantial-update: 2022-01-07
duration: 166
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
