---
title: Using AEM Experience Fragments
seo-title: Using AEM Experience Fragments
description: Experience Fragments is a new feature introduced in AEM 6.3. It allows content authors to reuse content across channels including Sites pages and 3rd party systems.
seo-description: Experience Fragments are a new feature introduced in AEM 6.3 that allows content authors to reuse content across channels including Sites pages and 3rd party systems.
uuid: 0922d3e7-e839-4214-8b96-21495f688ed3
products: SG_EXPERIENCEMANAGER/6.3/ASSETS
products: SG_EXPERIENCEMANAGER/6.3/SITES
topic-tags: authoring
discoiquuid: 27a28286-552f-493b-868c-e7d27302f583
targetaudience: target-audience new
index: y
internal: n
snippet: y
---

# Using Experience Fragments{#using-aem-experience-fragments}

Experience Fragments is a new feature introduced in AEM 6.3. It allows content authors to reuse content across channels including Sites pages and 3rd party systems.

## Experience Fragments Overview

>[!VIDEO](https://video.tv.adobe.com/v/17028/?quality=9)

An Experience Fragment is a set of content that grouped forms an experience that should make sense on its own.

With Experience Fragments marketers can:

* Reuse an experience across channels (both owned channels and 3rd party touch-points)
* Create variations of an experience for specific use-cases
* Keep variations in sync with the use of Live-Copy
* Social Post experiences to Facebook and Pinterest out of the box

## Building Blocks with Experience Fragments

Building blocks is a new enhancement added to Experience Fragment in AEM 6.4. It lets content authors to create a building block consisting of components that could be re-used to create content across different variations and across different templates.

>[!VIDEO](https://video.tv.adobe.com/v/21289/?quality=9)

>[!NOTE]
>
> Editable templates used for creating experience fragments should have the building block component added to its policies.

* Creating a building block makes it easy for content authors to re-use the content across different variations.
* Changing the master copy building block should automatically roll out changes to its references without cancelling inheritance or any layout changes.
* Content authors can easily rename an existing building block or delete it.
* Deleting a building block from an Experience Fragment doesn't delete its references.

## Experience Fragments Full-Text Search

>[!VIDEO](https://video.tv.adobe.com/v/27720/?quality=9)

AEM 6.5, now supports full-text search capabilities for Experience Fragments.

* **Content Authors** (Internal search) can now search for a text part within an Experience Fragment and the result would include the experience fragments containing the text as well as the page that references the experience fragment.
* **Site Users** (External search) can now perform a full-text search using the search component, and the result would include site pages that reference the experience fragment containing the search keyword.
