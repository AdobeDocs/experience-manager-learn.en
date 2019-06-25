---
title: Using Content Fragments in AEM
seo-title: Using Content Fragments in AEM
description: Content Fragments are a content abstraction in AEM that allows text-based content to be authored and managed independently of the channels it supports. 
seo-description: Content Fragments are a content abstraction in AEM that allows text-based content to be authored and managed independently of the channels it supports. 
uuid: 045473d2-5abe-4414-b91c-d369f3069ead
topic-tags: content-fragments
products: SG_EXPERIENCEMANAGER/6.3/SITES
products: SG_EXPERIENCEMANAGER/6.3/ASSETS
products: SG_EXPERIENCEMANAGER/6.4/ASSETS
products: SG_EXPERIENCEMANAGER/6.4/SITES
discoiquuid: 912e0c41-83cf-49f7-b515-09519b6718c1
targetaudience: target-audience new;target-audience ongoing
index: y
internal: n
snippet: y
---

# Using Content Fragments {#using-content-fragments}

Content Fragments are a content abstraction in AEM that allows text-based content to be authored and managed independently of the channels it supports.

>[!NOTE]
>
>The AEM Content Fragment functionality covered in these videos was first introduced in [AEM 6.3 + FP 19008 and FP19614](https://helpx.adobe.com/experience-manager/6-3/release-notes/content-services-fragments-featurepack.html).
>

AEM Content Fragments are text-based editorial content that may include some structured data elements associated but considered pure content without design or layout information. Content Fragments are typically created as channel-agnostic content, that is intended to be used and re-used across channels, which in turn wrap the content in a context-specific experience.

This video series covers the end-to-end life-cycle of Content Fragments in AEM, from definition to delivery.

1. Enabling and defining Content Fragment Models
1. Authoring Content Fragments
1. Downloading Content Fragments
1. Using Content Fragments on web pages
1. Exposing Content Fragments as JSON using AEM Content Services

## Defining Content Fragment Models {#defining-content-fragment-models}

>[!VIDEO](https://video.tv.adobe.com/v/22452/?quality=12)

AEM Content Fragments Models, the data schemas of Content Fragments, must be enabled via AEM's Configuration Browser, which allows Content Fragment Models to be defined on a per configuration basis.

## Authoring Content Fragments {#authoring-content-fragments}

>[!VIDEO](https://video.tv.adobe.com/v/22451/?quality=12)

AEM Configurations must be applied to AEM Assets folder hierarchies to allow their Content Fragment Models to be created as Content Fragments. Content Fragments support a rich form-based authoring experience allowing content to be modeled as a collection of elements.

Content Fragments can have multiple variants, each variant addressing a different use-case (thought, not necessarily channel) for the content.

Example athlete biography for import.

[sandra-sprient-bio.txt](assets/sandra-sprient-bio.txt)

## Downloading Content Fragments {#downloading-content-fragments}

>[!VIDEO](https://video.tv.adobe.com/v/22450/?quality=12)

AEM Content Fragments can be downloaded from AEM Author as a Zip file containing Variants, Elements, and Metadata.

Example Content Fragment download Zip file

[daniel_schreder.zip](assets/daniel_schreder.zip)

## Content Fragment editorial capabilities {#editorial-capabilities}

>[!VIDEO](https://video.tv.adobe.com/v/25891/?quality=12)

*Annotation and version compare for Content Fragments were introduced in [AEM 6.4 Service Pack 2](https://helpx.adobe.com/experience-manager/aem-releases-updates.html) and [AEM 6.3 Service Pack 3](https://helpx.adobe.com/experience-manager/6-3/release-notes/sp3-release-notes.html).*

## Using Content Fragments in Web pages {#using-content-fragments-in-web-pages}

>[!VIDEO](https://video.tv.adobe.com/v/22449/?quality=12)

Content Fragments can be used on AEM Sites pages, or in a similar fashion, Experience Fragments, using the AEM WCM Core Components' [Content Fragment component](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components/tree/master/extension/contentfragment/content/src/content/jcr_root/apps/core/wcm/extension/components/contentfragment/v1/contentfragment).

Content Fragment components can be styled using AEM's Style System to display the content as needed.

## Exposing Content Fragments as JSON {#exposing-content-fragments-as-json}

>[!VIDEO](https://video.tv.adobe.com/v/22448/?quality=12)

AEM Content Services facilitates the creation of AEM Page-based HTTP end-points that rendition content into a normalized JSON format.

Example Content Services end-point JSON payload

[athletes.json](assets/athletes.json)

## Supporting materials {#supporting-materials}

* [AEM Core WCM Components](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components)
* [AEM Core WCM Content Fragment Component](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components/tree/master/extension/contentfragment/content/src/content/jcr_root/apps/core/wcm/extension/components/contentfragment/v1/contentfragment)

To download and install the package below on an AEM 6.4+ instance for the final state from the video series.

[aem_demo_fluid-experiencescontent-fragments-100.zip](assets/aem_demo_fluid-experiencescontent-fragments-100.zip)
