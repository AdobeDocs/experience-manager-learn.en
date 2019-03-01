---
title: Getting Started with AEM Sites - WKND Tutorial
seo-title: Getting Started with AEM Sites - WKND Tutorial
description: A multi-part tutorial designed for developers new to AEM. Walks through the implementation of an AEM site for a fictitious lifestyle brand the WKND. Covers fundamental topics like project setup, Core Components, Editable Templates, client libraries, and component development.
seo-description: A multi-part tutorial designed for developers new to AEM. Walks through the implementation of an AEM site for a fictitious lifestyle brand the WKND. Covers fundamental topics like project setup, Core Components, Editable Templates, client libraries, Style System, and component development.
uuid: 4b369f63-858c-4c26-b092-a3151b53924a
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: developing
products: SG_EXPERIENCEMANAGER/6.3/SITES
discoiquuid: a0c5006a-7777-45e4-aca7-560a42fd6e56
targetaudience: target-audience new
---

# Getting Started with AEM Sites - WKND Tutorial {#getting-started-with-aem-sites-wknd-tutorial}

A multi-part tutorial designed for developers new to AEM. Walks through the implementation of an AEM site for a fictitious lifestyle brand the WKND. Covers fundamental topics like project setup, Core Components, Editable Templates, client libraries, and component development.

## Overview {#overview}

The goal for this multi-part tutorial is to teach a developer how to implement a website using the latest standards and technologies in Adobe Experience Manager (AEM). After completing this tutorial a developer understands the basic foundation of the platform and has knowledge of common design patterns in AEM.

The implementation works as-is on **AEM 6.4 + SP2** and **AEM 6.3 + SP3**. Many of the topics apply to all versions of AEM. The site is implemented using:

* HTL
* Sling Models
* Touch UI
* Core Components v2
* Editable Templates
* Style System
* Maven AEM Project Archetype 15

*Estimate 1-2 hours to get through each part of the tutorial.*

>[!NOTE]
>
>A previous version of this tutorial existed that leveraged a different Maven archetype for the project. The finished code for the previous tutorial can be found **[here](https://github.com/Adobe-Marketing-Cloud/aem-guides-wknd/tree/legacy/archetype-13)**

### Github {#github}

All of the code for the project can be found on Github in the AEM Guide repo:

**[GitHub: WKND Sites Project](https://github.com/Adobe-Marketing-Cloud/aem-guides-wknd)**

In addition, each part of the tutorial has its own branch in GitHub. A user can begin the tutorial at any point by simply checking out the branch that corresponds to the previous part.

***Any issues or problems with the tutorial please create an [Issue on Github.](https://github.com/Adobe-Marketing-Cloud/aem-guides-wknd/issues)***

### Latest {#latest}

To test the latest code before jumping into the tutorial, download and install the below packages.

[Get File](assets/aem-guides-wknd_uiapps-001-snapshot.zip)

[Get File](assets/aem-guides-wknd_uicontent-001-snapshot.zip)

WKND Solution Package (Chapters 1-8)

[Get File](assets/wknd-solutions.zip)

## WKND Design {#wknd-site}

The WKND is a fictional online magazine and blog that focuses on nightlife, activities, and events in several international cities. To make this tutorial closer to a real-world scenario one of Adobe's talented UX designers created the mockups for the site. Over the course of the tutorial various pieces of the mockup are implemented into a fully author-able AEM site. Special thanks to **Lorenzo Buosi** who created the beautiful design for the WKND site.

Below is an overview video of the site and functionality.

>[!VIDEO](https://video.tv.adobe.com/v/21628?quality=9)

## Table of Contents {#table-of-contents}

In general each Part of the tutorial takes about **1-2 hours**.

### Chapter 1 {#part-1}

[**Project Setup**](part1.md) - Covers the creation of a Maven Multi Module Project to manage the code and configurations for an AEM Site.  
**Maven, Lazybones Template, Eclipse IDE, Core Components, SCM, and Github**.

### Chapter 2 {#part-2}

**[Creating a Base Page and Template](part2.md)** - Covers the creation of a base page and an editable template. Core Components are proxied into the project.  
**Editable Templates, Core Components, Content Authoring**

### Chapter 3 {#part-3}

**[Client-Side Libraries and Responsive Grid](part3.md)** - Covers creation of AEM Client-Side Libraries or clientlibs to deploy and manage CSS and Javascript for an AEM Sites implementation. Integration with AEM's responsive grid and mobile emulator. [aemfed](https://aemfed.io/) module is used to accelerate front end development.  
**Client-Side Libraries, CSS, Javascript, LESS, aemfed, Responsive Grid**

### Chapter 4 {#part-4}

**[Developing with the Style System](part4.md)** - Covers extending Core Components with brand-specific CSS and leveraging the Style System to create multiple variations of components. This part also uses Content Fragments for long form article content and covers some advanced policy configurations of the Template Editor.  
**CSS, Style System, Template Editor Policies**

### Chapter 5 {#part-5}

**[Navigation and Search](part5.md)** - Covers dynamic navigation driven by the content hierarchy and fixed navigation populated by content authors. Sling Models, HTL templating language, and dialogs are used to implement the Header and Footer navigation. A Quick Search component is also added to the Header.  
**HTL, Design Dialogs, Composite Components**

### Chapter 6 {#part-6}

**[Creating a new AEM Component](part6.md)** - Covers the end to end creation of a custom byline component that displays authored content. Includes developing a Sling Model to encapsulate business logic to populate the byline component and corresponding HTL to render the component.  
**Sling Models, HTL, Style System, Custom Components**

### Chapter 7 {#part-7}

**[Teaser and Carousel Extension](part7.md)** - Covers the implementation of the Teaser and Carousel components to populate a dynamic and exciting Homepage.  
**Advanced Template Editor Policies, Style System, Core Components v2**

### Chapter 8 {#part-8}

**[Unit Testing](part8.md)** - Covers the implementation of a Unit Test that validates the behavior of the Byline component's Sling Model, created in [Chapter 6](part6.md) of the tutorial.  
**Unit tests, io.wcm AEM Mocks, Mockito and JUnit**
