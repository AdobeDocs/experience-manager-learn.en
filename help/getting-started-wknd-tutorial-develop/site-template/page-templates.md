---
title: Page templates
seo-title: Getting Started with AEM Sites - Page templates
description: Learn how to create and modify Page Templates. Understand the relationship between a Page Template and a Page. Learn how to configure policies of a Page Template to provide granular governance and brand consistency for content.  A well-structured Magazine Article template will be created based on a mockup from Adobe XD.
sub-product: sites
version: Cloud Service
type: Tutorial
topic: Content Management
feature: Core Components, Editable Templates, Page Editor
role: Developer
level: Beginner
kt: 7498
thumbnail: KT-7498.jpg
---

# Page templates {#page-templates}

>[!CAUTION]
>
> The quick site creation features showcased here will be released in the second half of 2021. The related documentation is available for preview purposes.

In this chapter we will explore the relationship between a Page Template and a Page. We will build out an un-styled Magazine Article template based on some mockups from [AdobeXD](https://www.adobe.com/products/xd.html). In the process of building out the template, Core Components and advanced policy configurations are covered.

## Prerequisites {#prerequisites}

This is a multi-part tutorial and it is assumed that the steps outlined in the [Author content and publish changes](./author-content-publish.md) chapter have been completed.

## Objective

1. Inspect a page design created in Adobe XD and map it to Core Components.
1. Understand the details of Page Templates and how policies can be used to enforce granular control of page content.
1. Learn how Templates and Pages are linked.

## What you will build {#what-you-will-build}

In this part of the tutorial, you will build a new Magazine Article Page template that can be used to create new magazine articles and aligns with a common structure. The template will be based on designs and a UI Kit produced in AdobeXD. This chapter is only focused on building out the structure or skeleton of the template. No styles will be implemented but the template and pages will be functional.

## UI Planning with Adobe XD {#adobexd}

In most cases, planning for a new website starts with mockups and static designs. [Adobe XD](https://www.adobe.com/products/xd.html) is a design tool building user experiences. Next we will inspect a UI Kit and mockups to help plan the structure of the Article Page Template.

>[!VIDEO](https://video.tv.adobe.com/v/30214/?quality=12&learn=on)

**Download the [WKND Article Design File](https://github.com/adobe/aem-guides-wknd/releases/download/aem-guides-wknd-0.0.2/AEM_UI-kit-WKND-article-design.xd)**.

>[!NOTE]
>
> A generic [AEM Core Components UI Kit is also available](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/AEM-CoreComponents-UI-Kit.xd) as a starting point for custom projects.

## Create the Magazine Article Page Template

When creating a page you must select a template, which will be used as the basis for creating the new page. The template defines the structure of the resultant page, initial content, and allowed components.

There are 3 main areas of [Page Templates](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/authoring/features/templates.html):

1. **Structure** - defines components that are a part of the template. These will not be editable by content authors.
1. **Initial Content** - defines components that the template will start with, these can be edited and/or deleted by content authors
1. **Policies** - defines configurations on how components will behave and what options authors will have available.

Next, create a new template in AEM that matches the structure of the mockups. This will occur in a local instance of AEM. Follow the steps in the video below:

>[!VIDEO](https://video.tv.adobe.com/v/332915/?quality=12&learn=on)

### Solution Package

A finished [solution of the Magazine Template](assets/page-templates/WKND-Magazine-Template-SOLUTION-1.0.zip) can be downloaded and installed via Package Manager.

## Update the Header and Footer with Experience Fragments {#experience-fragments}

A common practice when creating global content, such as a header or footer, is to use an [Experience Fragment](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/experience-fragments/experience-fragments-feature-video-use.html). Experience Fragments, allows users to combine multiple components to create a single, reference-able, component. Experience Fragments have the advantage of supporting multi-site management and [localization](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/experience-fragment.html?lang=en#localized-site-structure).

The Site template generated a Header and Footer. Next, update the Experience Fragments to match the mockups. Follow the steps in the video below:

>[!VIDEO](https://video.tv.adobe.com/v/332916/?quality=12&learn=on)

High level steps for the video below:

1. Download the sample content package **[WKND-Starter-Assets-Skate-Article-1.0.zip](assets/page-templates/WKND-Starter-Assets-Skate-Article-1.0.zip)**.
1. Upload and install the content package using Package Manager.
1. Update the Header and Footer Experience Fragments to use the WKND logo

## Create a Magazine article page

Next, create a new page using the Magazine Article Page template. Author the content of the page to match the site mockups. Follow the steps in the video below:

>[!VIDEO](https://video.tv.adobe.com/v/332917/?quality=12&learn=on)

## Congratulations! {#congratulations}

Congratulations, you have just created a new template and page with Adobe Experience Manager Sites.

### Next Steps {#next-steps}

At this point the magazine article page and the site does not match the brand styles for WKND. Follow the [Theming](theming.md) tutorial to learn the best practices for updating CSS and Javascript frontend code used to apply global styles to the site.

### Solution Package

A solution package for this chapter is available to download: [WKND-Magazine-Template-SOLUTION-1.0.zip](assets/page-templates/WKND-Magazine-Template-SOLUTION-1.0.zip).
