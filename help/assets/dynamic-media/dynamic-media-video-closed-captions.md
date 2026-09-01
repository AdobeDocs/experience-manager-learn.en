---
title: Closed Captions for Video in Dynamic Media
description: Learn to create captions for videos via AI. Closed captions are auto-generated once a video file is uploaded to Dynamic Media.
version: Experience Manager as a Cloud Service
feature: Dynamic Media
role: User
level: Intermediate
doc-type: Feature Video
duration: 233
last-substantial-update: 2026-08-28
jira: KT-15930
exl-id: ffbe2da8-1ffe-4d61-a3fa-c76136933dc2
TQID: https://experienceleague.adobe.com/OCg9P9xAXbsQwwzZjWgWlzKEynufUZJjVGoukr781CM
product_v2:
  - id: d09181b5-a36a-43de-ba01-36641440bc43
    internal-label: Experience Manager Assets
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: bd0d2470-932c-4269-8eca-6d939b72d9ef
    internal-label: Dynamic Media
subfeature_v2:
  - id: d17d085a-e808-49dd-b9a6-85a996b999bd
    internal-label: Viewers
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
    internal-label: Metadata
---
# Video closed captions {#video-closed-captions}

Generate AI captions for a video in more than 60 languages, directly from the video's properties.

>[!BEGINTABS]

>[!TAB Admin view]

## Generate captions with AI

Convert captions from an existing audio track, or translate an existing caption file into additional languages, then preview the result in the viewer.

>[!VIDEO](https://video.tv.adobe.com/v/3432627/?learn=on)


## No downloadable original {#no-downloadable-original}

An Adaptive Video Sets (AVS) asset used for adaptive bitrate streaming is a logical container referencing multiple already-encoded renditions, for example, several H.264 MP4s at different bitrates. It does not hold a single master binary itself. Hence, the **[!UICONTROL Export]** option is disabled for AVS assets in the Scene7 Console. This is an expected container architecture, not a defect. If a downloadable original is needed, it must come from the separate master or source asset, not the AVS container.

## AEM-managed captions {#aem-managed-captions}

Manage caption (Web Video Text Tracks or VTT) files exclusively from within the Adobe Experience Manager (AEM), never directly in Dynamic Media Classic. Deleting or editing caption subassets in Dynamic Media Classic desynchronizes AEM and Dynamic Media, which can silently drop the CC or captions icon from the player and remove subtitle tracks from the Adaptive Video Set manifest with no explicit error. To recover, delete the captions from the AEM **[!UICONTROL Captions and Audio Tracks]** page, re-upload them, and republish the caption subassets through **[!UICONTROL Manage Publication]** with the **[!UICONTROL /subassets]** option. Folder synchronization or publish settings (**[!UICONTROL Sync everything]** and **[!UICONTROL Immediate publish]**) affect how quickly such caption changes propagate to Dynamic Media.

>[!ENDTABS]

