---
title: Trigger AEM workflow on HTM5 Form Submission introduction
seo-title: Trigger AEM Workflow on HTML5 Form Submission
description: Continue filling mobile form in offline mode and submit mobile form to trigger AEM workflow
seo-description: Continue filling mobile form in offline mode and submit mobile form to trigger AEM workflow
feature: Mobile Forms
topics: development
audience: developer
doc-type: article
activity: implement
version: 6.4,6.5
topic: Development
role: Developer
level: Experienced
exl-id: 88295af5-3022-4462-9194-46d8c979bc8b
last-substantial-update: 2021-04-07
---
# Downloading partially completed mobile form and submitting to AEM workflow

A common use case is to have the ability to render the XDP as HTML for data capture activities. This works well when the forms are simple and can be filled and submitted online. However, if the form is complex the users may not be able to complete the form online, we need to provide the ability to allow the form fillers to download interactive version of the form to be filled in using Acrobat/Reader in offline manner. Once the form is filled, the user can be online to submit the form.
 To accomplish this use case we need to perform the following steps:

* Ability to generate interactive/fillable PDF with the data entered in the mobile form
* Handle the PDF submission from Acrobat/Reader
* Trigger Adobe Experience Manager (AEM) workflow to review the submitted PDF

This tutorial walks through the steps needed to accomplish the above use case. Sample code and assets related to this tutorial are [available here.](part-four.md)

The following video gives you an overview of the use case

>[!VIDEO](https://video.tv.adobe.com/v/29677?quality=9&learn=on)
