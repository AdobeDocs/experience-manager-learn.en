---
title: Smart Tags for Images with AEM Assets
description: Learn how Smart Tags automatically add metadata tags to image assets based on image content, and how to review and manage them.
solution: Experience Manager, Experience Manager Assets
sub-product: Experience Manager Assets
feature-set: Experience Manager Assets
topic: Content Management
feature: Smart Tags
role: User
level: Intermediate
version: Experience Manager 6.4, Experience Manager 6.5, Experience Manager as a Cloud Service
jira: KT-645
thumbnail: 17019.jpg
team: TM
last-substantial-update: 2026-08-27
doc-type: Feature Video
exl-id: c72dc489-70e6-48ca-99a8-663d4c0652ba
duration: 574
TQID: https://experienceleague.adobe.com/Bpeu8oeEqhit8HB4mFmghy7lwHmQbGsdTZhakUoL6gM
product_v2:
  - id: d09181b5-a36a-43de-ba01-36641440bc43
    internal-label: Experience Manager Assets
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: a01bfd36-4ab8-4bf8-9dc0-5b45b890552e
    internal-label: APIs
  - id: a45b1e7f-e65f-4cd3-be86-5cec5d9449ef
    internal-label: Content management
  - id: da0dfbce-df02-4f8b-b32d-a4e3b1d05085
    internal-label: Configuration
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
    internal-label: Metadata
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
  - id: eb30f47f-d87a-400f-8f78-63ce7979ff56
    internal-label: Machine learning
---
# Smart Tags for images {#image-smart-tags}

In a large asset library, no one has time to tag every image by hand. Smart Tags scan each image on upload and add descriptive keywords automatically, so every asset stays searchable without extra effort. This saves your team hours of manual work and keeps search results accurate as your library grows.

>[!BEGINTABS]

>[!TAB Admin view]

Smart Tags improve search: they add derived metadata tags to image assets automatically, so it's faster to find the right image.

>[!VIDEO](https://video.tv.adobe.com/v/17019?quality=12&learn=on)

## Set up for AEM 6.x {#set-up}

>[!NOTE]
>Smart Tags for images is automatically provisioned for AEM as a Cloud Service.

>[!VIDEO](https://video.tv.adobe.com/v/17023?quality=12&learn=on)

Before you can use the Smart Content Service, create an integration on Adobe I/O. You need:

* An Adobe ID account with administrator privileges for the organization
* The Smart Content Service enabled for your organization

This video covers the tasks required to configure the Adobe I/O Smart Content service used to Smart Tag images:

* Create a Smart Content Service configuration in AEM to generate a public key, then obtain a public certificate for OAuth integration.
* Create an integration in Adobe I/O and upload the generated public key.
* Configure your AEM instance with the API key and other credentials from Adobe I/O.
* Optionally, enable auto-tagging on asset upload.

## Additional resources

* [AEM Assets Smart Tags documentation](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/manage/smart-tags)

>[!ENDTABS]
