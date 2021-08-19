---
title: Getting Started with AEM Sites - Project Archetype
description: Getting Started with AEM Sites - Project Archetype. The WKND tutorial is a multi-part tutorial designed for developers new to Adobe Experience Manager. The tutorial walks through the implementation of an AEM site for a fictitious lifestyle brand, the WKND. The tutorial covers fundamental topics like project setup, maven archetypes, Core Components, Editable Templates, client libraries, and component development.
sub-product: sites
version: 6.4, 6.5, Cloud Service
type: Tutorial
feature: Core Components, Page Editor, Editable Templates, AEM Project Archetype
topic: Content Management, Development
role: Developer
level: Beginner
mini-toc-levels: 1
index: y
---

# Getting Started with AEM Sites - Project Archetype {#project-archetype}

Welcome to a multi-part tutorial designed for developers new to Adobe Experience Manager (AEM). This tutorial walks through the implementation of an AEM site for a fictitious lifestyle brand the WKND.

This tutorial starts by using the [AEM Project Archetype](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html) to generate a new project.

The tutorial is designed to work with **AEM as a Cloud Service** and is backwards compatible with **AEM 6.5.5.0+** and **AEM 6.4.8.1+**. The site is implemented using:

* [Maven AEM Project Archetype](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)
* [Core Components](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html)
* [HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/using/getting-started/getting-started.html)
* Sling Models
* [Editable Templates](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/page-authoring/template-editor-feature-video-use.html)
* [Style System](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/page-authoring/style-system-feature-video-use.html)

*Estimate 1-2 hours to get through each part of the tutorial.*

## Local Development Environment {#local-dev-environment}

A local development environment is necessary to complete this tutorial. Screenshots and video are captured using the AEM as a Cloud Service SDK running on a Mac OS environment with [Visual Studio Code](https://code.visualstudio.com/) as the IDE. Commands and code should be independent of the local operating system, unless otherwise noted.

### Required software

The following should be installed locally:

* Local AEM **Author** instance (Cloud Service SDK, 6.5.5+ or 6.4.8.1+)
* [Java 11](https://downloads.experiencecloud.adobe.com/content/software-distribution/en/general.html)
* [Apache Maven](https://maven.apache.org/) (3.3.9 or newer)
* [Node.js](https://nodejs.org/en/) (LTS - Long Term Support)
* [npm 6+](https://www.npmjs.com/)
* [Git](https://git-scm.com/)
* [Visual Studio Code](https://code.visualstudio.com/) or equivalent IDE
  * [VSCode AEM Sync](https://marketplace.visualstudio.com/items?itemName=yamato-ltd.vscode-aem-sync) - Tool used throughout tutorial

>[!NOTE]
>
> **New to AEM as a Cloud Service?** Check out the [following guide to setting up a local development environment using the AEM as a Cloud Service SDK](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html).
>
> **New to AEM 6.5?** Check out the [following guide to setting up a local development environment](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/set-up-a-local-aem-development-environment.html).

## Github {#github}

All of the code for the project can be found on Github in the AEM Guide repo:

**[GitHub: WKND Sites Project](https://github.com/adobe/aem-guides-wknd)**

In addition, each part of the tutorial has its own branch in GitHub. A user can begin the tutorial at any point by simply checking out the branch that corresponds to the previous part.

## Next Steps {#next-steps}

What are you waiting for?! Start the tutorial by navigating to the [Project Setup](project-setup.md) chapter and learn how to generate a new Adobe Experience Manager project using the AEM Project Archetype.
