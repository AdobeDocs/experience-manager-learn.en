---
title: Using the Video Player in AEM Dynamic Media
description: AEM Dynamic Media video player used to rely on Flash runtime to support adaptive video streaming on desktop clients and browsers became more aggressive on flash-based content streaming. With the introduction of HLS (Apple's HTTP Live Streaming video delivery protocol), content can now be streamed without relying on flash.
feature: Video Profiles
version: Experience Manager 6.4, Experience Manager 6.5
topic: Content Management
role: User
level: Beginner
doc-type: Feature Video
exl-id: 7e4cb782-836d-4ec0-97d0-645b91ea43e0
duration: 568
TQID: https://experienceleague.adobe.com/5hZIcOnuCUeS2Jk-9YQEMmEjCeFazoDxT07WFtVFNZ8
product_v2:
  - id: d09181b5-a36a-43de-ba01-36641440bc43
    internal-label: Experience Manager Assets
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: a45b1e7f-e65f-4cd3-be86-5cec5d9449ef
    internal-label: Content management
  - id: bd0d2470-932c-4269-8eca-6d939b72d9ef
    internal-label: Dynamic Media
subfeature_v2:
  - id: a0cde32c-c339-4649-bd06-f1111bc952fc
    internal-label: Smart Crop
  - id: cf50b0d2-df62-495c-a741-4fa0284ca4fc
    internal-label: Hybrid mode
  - id: d17d085a-e808-49dd-b9a6-85a996b999bd
    internal-label: Viewers
  - id: d8e79b3c-92b5-4c4d-a46c-5f16d63a14dc
    internal-label: Viewer presets
  - id: d8ea7e82-d45e-442f-bb04-b3788a7abcb0
    internal-label: Video profiles
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
level_v2:
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
---
# Using the Video Player in AEM Dynamic Media{#using-the-video-player-in-aem-dynamic-media}

AEM Dynamic Media video player used to rely on Flash runtime to support adaptive video streaming on desktop clients and browsers became more aggressive on flash-based content streaming. With the introduction of HLS (Apple's HTTP Live Streaming video delivery protocol), content can now be streamed without relying on flash.

>[!VIDEO](https://video.tv.adobe.com/v/16791?quality=12&learn=on)

## Quick look into Non Flash Video Player {#quick-look-into-non-flash-video-player}

>[!VIDEO](https://video.tv.adobe.com/v/17429?quality=12&learn=on)

HLS browser support is as follows, for unsupported browsers we fallback to progressive video delivery

>[!NOTE]
>
> Dynamic Media Hybrid does NOT support video streaming on Internet Explorer 11 as of March 15th, 2022. Please upgrade to 6.5.12 or higher to fall back to progressive playback on IE 11.

<table> 
 <thead> 
  <tr> 
   <th> <p>Device</p> </th>
   <th> <p>Browser</p> </th>
   <th > <p>Video playback mode</p> </th>
  </tr>
 </thead>
 <tbody>
  <tr> 
   <td> <p>Desktop</p> </td>
   <td> <p>Internet Explorer 9 and 10</p> </td>
   <td> <p>Progressive download</p> </td>
  </tr>
  <tr>
   <td> <p>Desktop</p> </td>
   <td> <p>Internet Explorer 11+</p> </td>
   <td> <p>Dynamic Media - Scene 7 mode: HLS video streaming</p> 
        <p>Dynamic Media - Hybrid mode: Progressive download</p>
   </td>
  </tr>
  <tr>
   <td> <p>Desktop</p> </td>
   <td> <p>Firefox 23-44</p> </td>
   <td> <p>Progressive download</p> </td>
  </tr>
  <tr> 
   <td> <p>Desktop</p> </td>
   <td> <p>Firefox 45 or later</p> </td>
   <td> <p>HLS video streaming</p> </td>
  </tr>
  <tr> 
   <td> <p>Desktop</p> </td>
   <td> <p>Chrome</p> </td>
   <td> <p>HLS video streaming</p> </td>
  </tr>
  <tr> 
   <td> <p>Desktop</p> </td>
   <td> <p>Safari (Mac)</p> </td>
   <td> <p>HLS video streaming</p> </td>
  </tr>
  <tr> 
   <td> <p>Mobile</p> </td>
   <td> <p>Chrome (Android 6 or earlier)</p> </td>
   <td> <p>Progressive download</p> </td>
  </tr>
  <tr> 
   <td> <p>Mobile</p> </td>
   <td> <p>Chrome (Android 7 or later)</p> </td>
   <td> <p>HLS video streaming</p> </td>
  </tr>
  <tr> 
   <td> <p>Mobile</p> </td>
   <td> <p>Android (Default browser)</p> </td>
   <td> <p>Progressive download</p> </td>
  </tr>
  <tr> 
   <td> <p>Mobile</p> </td>
   <td> <p>Safari (iOS)</p> </td>
   <td> <p>HLS video streaming</p> </td>
  </tr>
  <tr> 
   <td> <p>Mobile</p> </td>
   <td> <p>Chrome (iOS)</p> </td>
   <td> <p>HLS video streaming</p> </td>
  </tr>
  <tr> 
   <td> <p>Mobile</p> </td>
   <td> <p>Blackberry</p> </td>
   <td> <p>HLS video streaming</p> </td>
  </tr>
 </tbody>
</table>
