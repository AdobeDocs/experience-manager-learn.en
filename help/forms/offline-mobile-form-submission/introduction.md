---
title: Trigger AEM workflow on PDF Form Submission
description: Continue filling mobile form in offline mode and submit mobile form to trigger AEM workflow
feature: Mobile Forms
doc-type: article
version: Experience Manager 6.4, Experience Manager 6.5
topic: Development
role: Developer
level: Experienced
exl-id: 88295af5-3022-4462-9194-46d8c979bc8b
last-substantial-update: 2021-04-07T00:00:00.000Z
jira: kt-16133
badgeVersions: label="AEM Forms 6.5" before-title="false"
duration: 342
TQID: 'https://experienceleague.adobe.com/J14D4rIYiJkpaawuEj2KZMtaR2Pf6CUatO-X6cToRUk'
product_v2:
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: 59f95943-e802-56ac-990d-21ab923984c1
    internal-label: Mobile Forms
  - id: f6a6f91a-8819-530a-8e7b-c50884a25aef
    internal-label: Workflow
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
---
# Downloading partially completed mobile form and submitting to trigger an AEM workflow

A common use case is to have the ability to render the XDP as HTML for data capture activities. This works well when the forms are simple and can be filled and submitted online. However, if the form is complex the users may not be able to complete the form online, we need to provide the ability to allow the form fillers to download interactive version of the form to be filled in using Acrobat/Reader in offline manner. Once the form is filled, the user can be online to submit the form.
 To accomplish this use case we need to perform the following steps:

* Ability to generate interactive/fillable PDF with the data entered in the mobile form
* Handle the PDF submission from Acrobat/Reader
* Trigger Adobe Experience Manager (AEM) workflow to review the submitted PDF

This tutorial walks through the steps needed to accomplish the above use case. Sample code and assets related to this tutorial are [available here.](./deploy-assets.md)

The following video gives you an overview of the use case

>[!VIDEO](https://video.tv.adobe.com/v/29677?quality=12&learn=on)

## Next Steps

[Create Custom Profile](./custom-profile.md)