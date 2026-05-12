---
title: Using Dynamic Media Viewers with Adobe Analytics and tags
description: The Dynamic Media Viewers extension for tags, along with the release of Dynamic Media Viewers 5.13, lets customers of Dynamic Media, Adobe Analytics, and tags use events and data specific for the Dynamic Media Viewers in their tags configuration.
sub-product: Dynamic Media
feature: Asset Insights
version: Experience Manager 6.4, Experience Manager 6.5
topic: Content Management
role: User
level: Beginner
doc-type: Feature Video
exl-id: 9d807f4c-999c-45e6-a9db-6c1776bddda1
duration: 576
TQID: https://experienceleague.adobe.com/lY-O6bm3sPgi-ZLcc36nwhYJAKaF10Ke1RD15vA0tSU
product_v2:
  - id: d09181b5-a36a-43de-ba01-36641440bc43
    internal-label: Experience Manager Assets
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: a45b1e7f-e65f-4cd3-be86-5cec5d9449ef
    internal-label: Content management
  - id: ae478996-b206-4712-9b0c-dc78a2644453
    internal-label: Integrations
  - id: bd0d2470-932c-4269-8eca-6d939b72d9ef
    internal-label: Dynamic Media
  - id: da0dfbce-df02-4f8b-b32d-a4e3b1d05085
    internal-label: Configuration
  - id: e17747bc-9b7b-44e6-a443-f54229a02620
    internal-label: Integrations
subfeature_v2:
  - id: c12bda38-aa1a-4647-b62e-42cd4537dac6
    internal-label: Dynamic Media Classic
  - id: d17d085a-e808-49dd-b9a6-85a996b999bd
    internal-label: Viewers
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
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
    internal-label: Insights
---
# Using Dynamic Media Viewers with Adobe Analytics and tags{#using-dynamic-media-viewers-adobe-analytics-tags}

For customers with Dynamic Media and Adobe Analytics, you can now track usage of Dynamic Media Viewers on your website using the Dynamic Media Viewer Extension.

>[!VIDEO](https://video.tv.adobe.com/v/29308?quality=12&learn=on)

>[!NOTE]
>
> Run Adobe Experience Manager in Dynamic Media Scene7 mode for this functionality. You also need to [integrate tags with your AEM instance](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-launch/overview.html).

With the introduction of the Dynamic Media Viewer extension, Adobe Experience Manager now offers advanced analytics support for assets delivered with Dynamic Media viewers (5.13), providing more granular control over event tracking when a Dynamic Media Viewer is used on a Sites page.

If you already have AEM Assets and Sites, you can integrate your tags property with your AEM author instance. Once your launch integration is associated with your website, you can add a dynamic media components to your page with event tracking for viewers enabled.

For AEM Assets-only customers or Dynamic Media Classic customers, user can get embed code for a viewer and add it to the page. Tags Script libraries can then be manually added to the page for viewer event tracking.

The following table lists Dynamic Media Viewer events and their supported arguments:

<table>
   <tbody>
      <tr>
         <td>Viewer event name</td>
         <td>Argument reference</td>
      </tr>
      <tr>
         <td> COMMON </td>
         <td> %event.detail.dm.objID% </td>
      </tr>
      <tr>
         <td>&nbsp;</td>
         <td> %event.detail.dm.compClass% </td>
      </tr>
      <tr>
         <td>&nbsp;</td>
         <td> %event.detail.dm.instName% </td>
      </tr>
      <tr>
         <td>&nbsp;</td>
         <td> %event.detail.dm.timeStamp% </td>
      </tr>
      <tr>
         <td> BANNER <br></td>
         <td> %event.detail.dm.BANNER.asset% </td>
      </tr>
      <tr>
         <td>&nbsp;</td>
         <td> %event.detail.dm.BANNER.frame% </td>
      </tr>
      <tr>
         <td>&nbsp;</td>
         <td> %event.detail.dm.BANNER.label% </td>
      </tr>
      <tr>
         <td> HREF </td>
         <td> %event.detail.dm.HREF.rollover% </td>
      </tr>
      <tr>
         <td> ITEM </td>
         <td> %event.detail.dm.ITEM.rollover% </td>
      </tr>
      <tr>
         <td> LOAD </td>
         <td> %event.detail.dm.LOAD.applicationname% </td>
      </tr>
      <tr>
         <td><strong>&nbsp;</strong></td>
         <td> %event.detail.dm.LOAD.asset% </td>
      </tr>
      <tr>
         <td><strong>&nbsp;</strong></td>
         <td> %event.detail.dm.LOAD.company% </td>
      </tr>
      <tr>
         <td><strong>&nbsp;</strong></td>
         <td> %event.detail.dm.LOAD.sdkversion% </td>
      </tr>
      <tr>
         <td><strong>&nbsp;</strong></td>
         <td> %event.detail.dm.LOAD.viewertype% </td>
      </tr>
      <tr>
         <td><strong>&nbsp;</strong></td>
         <td> %event.detail.dm.LOAD.viewerversion% </td>
      </tr>
      <tr>
         <td> METADATA </td>
         <td> %event.detail.dm.METADATA.length% </td>
      </tr>
      <tr>
         <td>&nbsp;</td>
         <td> %event.detail.dm.METADATA.type% </td>
      </tr>
      <tr>
         <td> MILESTONE </td>
         <td> %event.detail.dm.MILESTONE.milestone% </td>
      </tr>
      <tr>
         <td> PAGE </td>
         <td> %event.detail.dm.PAGE.frame% </td>
      </tr>
      <tr>
         <td>&nbsp;</td>
         <td> %event.detail.dm.PAGE.label% </td>
      </tr>
      <tr>
         <td> PAUSE </td>
         <td> %event.detail.dm.PAUSE.timestamp% </td>
      </tr>
      <tr>
         <td> PLAY </td>
         <td> %event.detail.dm.PLAY.timestamp% </td>
      </tr>
      <tr>
         <td> SPIN </td>
         <td> %event.detail.dm.SPIN.framenumber% </td>
      </tr>
      <tr>
         <td> STOP </td>
         <td> %event.detail.dm.STOP.timestamp% </td>
      </tr>
      <tr>
         <td> SWAP </td>
         <td> %event.detail.dm.SWAP.asset% </td>
      </tr>
      <tr>
         <td> SWATCH </td>
         <td> %event.detail.dm.SWATCH.frame% </td>
      </tr>
      <tr>
         <td>&nbsp;</td>
         <td> %event.detail.dm.SWATCH.label% </td>
      </tr>
      <tr>
         <td> TARG </td>
         <td> %event.detail.dm.TARG.frame% </td>
      </tr>
      <tr>
         <td>&nbsp;</td>
         <td> %event.detail.dm.TARG.label% </td>
      </tr>
      <tr>
         <td> ZOOM </td>
         <td> %event.detail.dm.ZOOM.scale% </td>
      </tr>
   </tbody>
</table>

## Additional Resources{#additional-resources}

* [Integrating AEM with tags in Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-launch/overview.html)
* [Running Adobe Experience Manager on Dynamic Media Scene7 mode](https://experienceleague.adobe.com/docs/experience-manager-65/assets/dynamic/config-dms7.html?lang=en)
* [Integrating Dynamic Media Viewers with Adobe Analytics using tags](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-viewer-extension-use.html)
