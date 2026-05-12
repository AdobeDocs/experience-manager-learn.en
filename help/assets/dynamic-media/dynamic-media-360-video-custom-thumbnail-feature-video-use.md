---
title: Using Dynamic Media 360 Videos and Custom Video thumbnail with AEM Assets
description: Dynamic Media Viewer enhancements in AEM 6.5 includes the addition of support for 360 video rendering, 360 media viewers (video360Social and video360VR) and the ability to select custom video thumbnails.
feature: Video Profiles
version: Experience Manager 6.4, Experience Manager 6.5
topic: Content Management
role: User
level: Beginner
doc-type: Feature Video
exl-id: 4ee0b68f-3897-4104-8615-9de8dbb8f327
duration: 656
TQID: https://experienceleague.adobe.com/9TMsjbnUN16u-7BVIdsnZKMFuD3ILKgT4CILIXwRYkU
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
  - id: da0dfbce-df02-4f8b-b32d-a4e3b1d05085
    internal-label: Configuration
subfeature_v2:
  - id: a9d2a4a6-0a32-4f6e-8eb1-128ec2b18a80
    internal-label: Components
  - id: cf50b0d2-df62-495c-a741-4fa0284ca4fc
    internal-label: Hybrid mode
  - id: d17d085a-e808-49dd-b9a6-85a996b999bd
    internal-label: Viewers
  - id: d8e79b3c-92b5-4c4d-a46c-5f16d63a14dc
    internal-label: Viewer presets
  - id: d8ea7e82-d45e-442f-bb04-b3788a7abcb0
    internal-label: Video profiles
  - id: ee69dd13-2aba-4eb0-912b-399e82368d73
    internal-label: Scene7 mode
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
level_v2:
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
---
# Using Dynamic Media 360 Videos and Custom Video thumbnail with AEM Assets

Dynamic Media Viewer enhancements in AEM 6.5 includes the addition of support for 360 video rendering, 360 media viewers (video360Social and video360VR) and the ability to select custom video thumbnails.

>[!VIDEO](https://video.tv.adobe.com/v/26391?quality=12&learn=on)

>[!NOTE]
>
>Video assumes that your AEM instance is running on Dynamic Media S7 mode.  [Instructions on setting up AEM with Dynamic Media can be found here](https://helpx.adobe.com/experience-manager/6-3/assets/using/config-dynamic-fp-14410.html). When you upload a video, by default, Dynamic Media processes the footage as a 360 video, if it has an aspect ratio of 2:1. i.e., width to height ratio is 2:1.

>[!NOTE]
>
>Dynamic Media 360 Media components support 360 videos only. 

## Dynamic Media 360 Videos

360-degree videos, also known as spherical videos are video recordings where a view in every direction is recorded at the same time, shot using an omnidirectional camera or collection of cameras. During playback on a flat display, the user has control of the viewing direction, and playback on mobile devices typically leverage built-in gyroscope control.  It lets you expand beyond the limits of single photography. Marketers can provide users an engaging experience with the help of 360 videos.  Let's get started. The panoramic image aspect ratio criterion can be modified in the company's DMS7 configuration by specifying the double property s7PanoramicAR at /conf/global/settings/cloudconfigs/dmscene7/jcr:content.

## Dynamic Media 360 Videos

Dynamic Media video now supports the ability to select a custom thumbnail for your video. A user can either select an existing asset from AEM Assets or select a video frame as the thumbnail.

## Dynamic 360 Media Viewers

<table> 
 <tbody>
   <tr>
      <td>&nbsp;</td>
      <td>**Video360Social Viewer**</td>
      <td>**Video360VR Viewer**</td>
   </tr>
   <tr>
      <td>Dynamic Media Run Mode</td>
      <td>Dynamic Media Scene7 Mode only</td>
      <td>Dynamic Media Scene7 Mode only<br>
         <br>
      </td>
   </tr>
   <tr>
      <td>Use Case</td>
      <td>
         <p>For websites and devices that don't support gyroscope</p>
         <p>&nbsp;</p>
      </td>
      <td>
         <p>Provides a Virtual Reality experience for a device&nbsp;that supports&nbsp;gyroscope&nbsp;</p>
      </td>
   </tr>
   <tr>
      <td>Audio - Stereo Mode</td>
      <td>No</td>
      <td>Yes</td>
   </tr>
   <tr>
      <td>Video Playback</td>
      <td>Yes</td>
      <td>Yes</td>
   </tr>
   <tr>
      <td>Point of view navigation</td>
      <td>
         <ul>
            <li>Mouse drag (on desktop systems)</li>
            <li>Swipe (touch devices)</li>
         </ul>
      </td>
      <td>
         <ul>
            <li>Mouse and drag options are disabled</li>
            <li>Uses built-in gyroscope</li>
         </ul>
      </td>
   </tr>
   <tr>
      <td>HTML5 Player</td>
      <td>Yes</td>
      <td>Yes</td>
   </tr>
   <tr>
      <td>Social sharing options</td>
      <td>Yes</td>
      <td>No</td>
   </tr>
</tbody>
</table>

## Additional Resources{#additional-resources}

[Configuring Dynamic Media in Scene7 mode](https://helpx.adobe.com/experience-manager/6-5/assets/using/config-dms7.html)
