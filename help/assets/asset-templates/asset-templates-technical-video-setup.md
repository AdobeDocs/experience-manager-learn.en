---
title: Set up Asset Templates with AEM Assets and InDesign Server
description: Asset Templates allows marketers create, manage and deliver digital assets for digital and print. Creating marketing brochures, business cards, flyers, ads and post cards are much easier with Asset Templates when integrated with InDesign server. Configuration of InDesign server with AEM is covered in this section.
version: Experience Manager 6.4, Experience Manager 6.5
topic: Content Management
feature: Templates
role: Developer
level: Intermediate
doc-type: Technical Video
last-substantial-update: 2026-08-28
exl-id: 5b764d86-8ced-46ed-838e-4bd2e75fd64c
duration: 428
TQID: https://experienceleague.adobe.com/kv7VqGa0KlQvD6MJCK71Bv7APDLhe39lbXs0u9dZOTM
product_v2:
  - id: d09181b5-a36a-43de-ba01-36641440bc43
    internal-label: Experience Manager Assets
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: a45b1e7f-e65f-4cd3-be86-5cec5d9449ef
    internal-label: Content management
  - id: da0dfbce-df02-4f8b-b32d-a4e3b1d05085
    internal-label: Configuration
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
    internal-label: Metadata
---
# Set up Asset Templates with InDesign Server {#set-up-asset-templates-with-aem-assets-and-indesign-server}

AEM needs a running InDesign Server to turn InDesign template files into print-ready assets. Without that connection, Asset Templates cannot generate the editable fields marketers rely on. This page walks you through the steps to install InDesign Server and connect it to your AEM instance.

>[!BEGINTABS]

>[!TAB Admin view]

In the Admin view, this video shows how to install InDesign Server and connect it to your AEM instance. It covers how AEM uses that connection to generate InDesign renditions and extract media files once you upload a tagged InDesign file to AEM Assets.

>[!VIDEO](https://video.tv.adobe.com/v/17069?quality=12&learn=on)

>[!NOTE]
>
>AEM **must** be connected to a running InDesign server when the INDD template is uploaded. Part of the initial processing on the INDD file requires InDesign server.

## Download the InDesign Server trial {#download-indesign-server-trial}

Download the [InDesign Server trial](https://www.adobeprerelease.com/).

## Start InDesign Server {#starting-indesign-server}

```shell
# macOS command

$ /Applications/Adobe\ InDesign\ CC\ Server\ 2017/InDesignServer -port 8080
```

>[!ENDTABS]
