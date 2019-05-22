---
title: Getting Started with AEM Sites - WKND Tutorial
seo-title: Getting Started with AEM Sites - WKND Tutorial
description: Getting Started with AEM Sites - WKND Tutorial. The WKND tutorial is a multi-part tutorial designed for developers new to Adobe Experience Manager. The tutorial walks through the implementation of an AEM site for a fictitious lifestyle brand, the WKND. The tutorial covers fundamental topics like project setup, Core Components, Editable Templates, client libraries, and component development.
seo-description: Getting Started with AEM Sites - WKND Tutorial. The WKND tutorial is a multi-part tutorial designed for developers new to Adobe Experience Manager. The tutorial walks through the implementation of an AEM site for a fictitious lifestyle brand, the WKND. The tutorial covers fundamental topics like project setup, Core Components, Editable Templates, client libraries, and component development.
uuid: 4b369f63-858c-4c26-b092-a3151b53924a
products: SG_EXPERIENCEMANAGER/6.5/SITES
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: developing
discoiquuid: a0c5006a-7777-45e4-aca7-560a42fd6e56
targetaudience: target-audience new
mini-toc-levels: 1
index: y
---

# Getting Started with AEM Sites - WKND Tutorial {#introduction}

A multi-part tutorial designed for developers new to Adobe Experience Manager. Walks through the implementation of an AEM site for a fictitious lifestyle brand the WKND. Covers fundamental topics like project setup, Core Components, Editable Templates, client libraries, and component development with Adobe Experience Manager Sites.

## WKND Tutorial Overview {#wknd-tutorial-overview}

The goal for this multi-part tutorial is to teach a developer how to implement a website using the latest standards and technologies in Adobe Experience Manager (AEM). After completing this tutorial a developer understands the basic foundation of the platform and has knowledge of common design patterns in AEM.

>[!VIDEO](https://video.tv.adobe.com/v/27305?quality=9)

The implementation works as-is on **AEM 6.5** and **AEM 6.4.2+**. Many of the topics apply to all versions of AEM. The site is implemented using:

* HTL
* Sling Models
* Touch UI
* Core Components v**2.4.0**
* Editable Templates
* Style System
* Maven AEM Project Archetype v**18**

*Estimate 1-2 hours to get through each part of the tutorial.*

>[!NOTE]
>
>A previous version of this tutorial existed that leveraged a different Maven archetype for the project. The finished code for the previous tutorial can be found **[here](https://github.com/Adobe-Marketing-Cloud/aem-guides-wknd)**

## WKND Site Design {#wknd-site}

The WKND is a fictional online magazine and blog that focuses on nightlife, activities, and events in several international cities. To make this tutorial closer to a real-world scenario one of Adobe's talented UX designers created the mockups for the site. Over the course of the tutorial various pieces of the mockup are implemented into a fully author-able AEM site. Special thanks to **Lorenzo Buosi** who created the beautiful design for the WKND site.

The name WKND is fitting because we expect a developer to take the better part of a *weekend* to complete the tutorial.

### Latest {#latest}

To test the latest code before jumping into the tutorial, download and install the latest release:

* **[aem-guides-wknd.ui.apps-0.0.1-SNAPSHOT.zip](https://github.com/adobe/aem-guides-wknd/releases/download/archetype-18.1/aem-guides-wknd.ui.apps-0.0.1-SNAPSHOT.zip)**
* **[aem-guides-wknd.ui.content-0.0.1-SNAPSHOT.zip](https://github.com/adobe/aem-guides-wknd/releases/download/archetype-18.1/aem-guides-wknd.ui.content-0.0.1-SNAPSHOT.zip)**

### Github {#github}

All of the code for the project can be found on Github in the AEM Guide repo:

**[GitHub: WKND Sites Project](https://github.com/adobe/aem-guides-wknd)**

In addition, each part of the tutorial has its own branch in GitHub. A user can begin the tutorial at any point by simply checking out the branch that corresponds to the previous part.

## Table of Contents {#table-of-contents}

In general each Part of the tutorial takes about **1-2 hours**.

### Chapter 1 {#chapter-1}

**[Project Setup](project-setup.md)** - Covers the creation of a Maven Multi Module Project to manage the code and configurations for an AEM Site.

#### Maven, Lazybones Template, Eclipse IDE, Core Components, SCM, and Github

### Chapter 2 {#chapter-2}

**[Creating a Base Page and Template](pages-templates.md)** - Covers the creation of a base page and an editable template. Core Component proxies are inspected.

#### Editable Templates, Core Components, Content Authoring

### Chapter 3 {#chapter-3}

**[Client-Side Libraries and Responsive Grid](client-side-libraries.md)** - Covers creation of AEM Client-Side Libraries or clientlibs to deploy and manage CSS and Javascript for an AEM Sites implementation. Integration with AEM's responsive grid and mobile emulator. [aemfed](https://aemfed.io/) module is used to accelerate front end development.

#### Client-Side Libraries, CSS, Javascript, LESS, aemfed, Responsive Grid

### Chapter 4 {#chapter-4}

**[Developing with the Style System](style-system.md)** - Covers extending Core Components with brand-specific CSS and leveraging the Style System to create multiple variations of components. This part also uses Content Fragments for long form article content and covers some advanced policy configurations of the Template Editor.

#### CSS, Style System, Template Editor Policies

### Chapter 5 {#chapter-5}

**[Creating a custom AEM Component](custom-component.md)** - Covers the end to end creation of a custom byline component that displays authored content. Includes developing a Sling Model to encapsulate business logic to populate the byline component and corresponding HTL to render the component.

#### Sling Models, HTL, Style System, Custom Components

### Chapter 6 {#chapter-6}

**[Unit Testing](unit-testing.md)** - Covers the implementation of a Unit Test that validates the behavior of the Byline component's Sling Model, created in [Chapter 5](custom-component.md) of the tutorial.

#### Unit tests, io.wcm AEM Mocks, Mockito and JUnit

### Chapter 7 {#chapter-7}

**[Header and Footer](header-footer.md)** - Covers dynamic navigation driven by the content hierarchy and fixed navigation populated by content authors. Sling Models, HTL templating language, and dialogs are used to implement the Header and Footer navigation. A Quick Search component is also added to the Header.

#### HTL, Design Dialogs, Composite Components

### Chapter 8 {#chapter-8}

**[Landing Page](landing-page.md)** - Covers the implementation of the Teaser and Carousel components to populate a dynamic and exciting Homepage.

#### Advanced Template Editor Policies, Style System, Teaser and Carousel components
