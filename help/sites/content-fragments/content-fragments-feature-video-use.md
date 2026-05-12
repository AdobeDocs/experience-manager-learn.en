---
title: Authoring Content Fragments in AEM
description: Content Fragments are a content abstraction in AEM that allows text-based content to be authored and managed independently of the channels it supports.
feature: Content Fragments
version: Experience Manager as a Cloud Service
topic: Content Management
role: User
level: Beginner
doc-type: Feature Video
exl-id: d33c033a-9577-4d4e-99be-f3c7e2a4ce73
duration: 665
TQID: https://experienceleague.adobe.com/L-dDY8XxA0C-BTdwX-ZvfrIKWrSKpeA9V-wdSGqvEoo
product_v2:
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: e2c1b6d3-bb7e-4fe8-8c72-f7b403298e91
    internal-label: Authoring
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
level_v2:
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
    internal-label: Metadata
  - id: d3cdead0-685a-4489-9250-4bb709942f66
    internal-label: Data collection
---
# Authoring Content Fragments {#authoring-content-fragments}

Content Fragments are a content abstraction in AEM that allows text-based content to be authored and managed independently of the channels it supports.

AEM Content Fragments are text-based editorial content that may include some structured data elements associated but considered pure content without design or layout information. Content Fragments are typically created as channel-agnostic content, that is intended to be used and re-used across channels, which in turn wrap the content in a context-specific experience.

This video series covers the authoring life-cycle of Content Fragments in AEM. Details about [delivering Content Fragments can be found here](content-fragments-delivery-feature-video-use.md).

1. Enabling and defining Content Fragment Models
2. Authoring Content Fragments
3. Downloading Content Fragments
4. Editorial capabilities

>[!CONTEXTUALHELP]
>id="aemcloud_sites_admin_content_fragments"
>title="Manage Fragments"
>abstract="Learn how Content Fragments allow you to design, create, curate, and use page-independent content."

## Defining Content Fragment Models {#defining-content-fragment-models}

>[!VIDEO](https://video.tv.adobe.com/v/22452?quality=12&learn=on)

AEM Content Fragments Models, the data schemas of Content Fragments, must be enabled via AEM's [[!UICONTROL Configuration Browser]](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/configurations.html), which allows Content Fragment Models to be defined on a per configuration basis.

## Creating Content Fragments {#creating-content-fragments}

>[!VIDEO](https://video.tv.adobe.com/v/22451?quality=12&learn=on)

AEM configurations are applied to AEM Assets folder hierarchies to allow their Content Fragment Models to be created as Content Fragments. Content Fragments support a rich form-based authoring experience allowing content to be modeled as a collection of elements.

Content Fragments can have multiple variants, each variant addressing a different use-case (thought, not necessarily channel) for the content.

*Example athlete biography for import:*  
**[sandra-sprient-bio.txt](assets/sandra-sprient-bio.txt)**

## Downloading Content Fragments {#downloading-content-fragments}

>[!VIDEO](https://video.tv.adobe.com/v/22450?quality=12&learn=on)

AEM Content Fragments can be downloaded from AEM Author as a Zip file containing Variants, Elements, and Metadata.

*Example Content Fragment download Zip file:*  
**[daniel_schreder.zip](assets/daniel_schreder.zip)**

## Content Fragment editorial capabilities {#editorial-capabilities}

>[!VIDEO](https://video.tv.adobe.com/v/25891?quality=12&learn=on)

>[!NOTE]
>
> Annotation and version compare for Content Fragments were introduced in [AEM 6.4 Service Pack 2](https://helpx.adobe.com/experience-manager/aem-releases-updates.html) and [AEM 6.3 Service Pack 3](https://helpx.adobe.com/experience-manager/6-3/release-notes/sp3-release-notes.html).

## Next Steps

Learn about [delivering Content Fragments](content-fragments-delivery-feature-video-use.md).

## Additional Resources {#additional-resources}

* [Delivering Content Fragments](content-fragments-delivery-feature-video-use.md)
* [AEM WCM Core Components](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html)
* [AEM WCM Core Content Fragment Component](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html)

To download and install the package below on an AEM 6.4+ instance for the final state from the video series:

**[aem_demo_fluid-experiencescontent-fragments-100.zip](assets/aem_demo_fluid-experiencescontent-fragments-100.zip)**
