---
title: Using Panorama and Vertical Image Viewer with AEM Assets Dynamic Media
description: Dynamic Media Viewer enhancements in AEM 6.4 includes the addition of Panoramic Image Viewer, Panoramic Virtual Reality Image Viewer, and Vertical Image Viewer. Panoramic Viewer provides an easy way to deliver an engaging, immersive experience of the room, property, location or landscape without any custom development.
feature: Video Profiles, Video Profiles, 360 VR Video
version: Experience Manager 6.4, Experience Manager 6.5
topic: Content Management
role: User
level: Beginner
doc-type: Feature Video
exl-id: 6b2f7533-8ce0-4134-b1ae-b3c5d15a05e6
duration: 535
TQID: https://experienceleague.adobe.com/t90Zw7V7ah2x-SGVLJyFO7SeKsSmbpiT7GgAZKYgJ4Y
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
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
    internal-label: Metadata
---
# Using Panorama and Vertical Image Viewer with AEM Assets Dynamic Media{#using-panorama-and-vertical-image-viewer-with-aem-assets-dynamic-media}

Dynamic Media Viewer enhancements in AEM 6.4 includes the addition of Panoramic Image Viewer, Panoramic Virtual Reality Image Viewer, and Vertical Image Viewer. Panoramic Viewer provides an easy way to deliver an engaging, immersive experience of the room, property, location or landscape without any custom development.

>[!VIDEO](https://video.tv.adobe.com/v/24156?quality=12&learn=on)

>[!NOTE]
>
>Video assumes that your AEM instance is running on Dynamic Media S7 mode. [Instructions on setting up AEM with Dynamic Media can be found here.](https://helpx.adobe.com/experience-manager/6-3/assets/using/config-dynamic-fp-14410.html)

## Panoramic and Panoramic VR Viewer

An image is considered panoramic based on its aspect ratio or keywords. By default, an image with aspect ratio of 2 is considered as a panoramic image. Panoramic Image viewer presets become available for an image preview if it satisfies the above criteria. The panoramic image aspect ratio criterion can be modified in the company's DMS7 configuration by specifying the double property s7PanoramicAR at /conf/global/settings/cloudconfigs/dmscene7/jcr:content. The keywords are stored in the dc:keyword property of the asset's metadata node. If the keywords contain any of the following combination :

* equirectangular,
* spherical + panoramic,
* spherical + panorama,

it is considered as a Panoramic Image asset regardless of its aspect ratio.

## Vertical Image Viewer

With horizontal swatches, depending on the consumer's desktop screen size, sometimes the swatches would not be visible until user scrolls down the page. By using vertical image viewer and placing vertical swatches, it ensures that the swatches are visible no matter what the screen size is. It also maximizes the main image size. With horizontal swatches, it was necessary to reserve space on the page to ensure they have a high likelihood of being visible and would decrease the size of the main image. With a vertical layout, you do not need to worry about allocating this space and therefore can maximize the main image size.

<table> 
 <tbody>
  <tr>
   <td> </td>
   <td>Panoramic and VR Viewer</td>
   <td>Vertical Image Viewer</td>
  </tr>
  <tr>
   <td>Dynamic Media Run Mode</td>
   <td>Dynamic Media Scene7 Mode only</td>
   <td>DMS7 and Dynamic Media</td>
  </tr>
  <tr>
   <td>Use Case</td>
   <td><p>Panoramic viewer and Virtual Reality viewer provide users a more engaging experience. A user can check out a hotel room even before he or she makes a booking, or check out a rental property without having to schedule an appointment. A user can check out a location and many more possibilities. The primary focus here is to provide consumer a better experience when they visit your website and eventually increase your conversion rate.</p> <p> </p> </td> 
   <td><p>Vertical Image viewer helps maximize product imagery viewing experience to give consumers the best representation of the product, thereby driving conversion and minimizing returns.</p> <p> </p> </td>
  </tr>
  <tr>
   <td>Available </td>
   <td>OOTB</td>
   <td>OOTB</td>
  </tr>
 </tbody>
</table>

[Configuring Dynamic Media in Scene7 mode](https://helpx.adobe.com/experience-manager/6-5/assets/using/config-dms7.html)

[Configuring Dynamic Media in Hybrid mode](https://helpx.adobe.com/experience-manager/6-5/assets/using/config-dynamic.html)

>[!NOTE]
>
>Panoramic viewers work with panoramic images and are not meant to be used with normal images.
