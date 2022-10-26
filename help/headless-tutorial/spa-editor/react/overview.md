---
title: Getting Started with the AEM SPA Editor and React
description: Create your first React Single Page Application (SPA) that is editable in Adobe Experience Manager AEM with the WKND SPA. Learn how to create a SPA using the React JS framework with AEM's SPA Editor. This multi-part tutorial walks through the implementation of a React application for a fictitious lifestyle brand, the WKND. The tutorial covers the end to end creation of the SPA and the integration with AEM.
topics: development
version: Cloud Service
doc-type: tutorial
activity: develop
audience: developer
kt: 5912
thumbnail: 5912-spa-react.jpg
feature: SPA Editor
topic: SPA
role: Developer
level: Beginner
exl-id: 38802296-8988-4300-a04a-fcbbe98ac810
last-substantial-update: 2022-08-25
---
# Create your first React SPA in AEM {#overview}

Welcome to a multi-part tutorial designed for developers new to the **SPA Editor** feature in Adobe Experience Manager (AEM). This tutorial walks through the implementation of a React application for a fictitious lifestyle brand, the WKND. The React app is developed and designed to be deployed with AEM's SPA Editor, which maps React components to AEM components. The completed SPA, deployed to AEM, can be dynamically authored with traditional in-line editing tools of AEM.

![Final SPA Implemented](assets/wknd-spa-implementation.png)

*WKND SPA Implementation*

## About

The tutorial is designed to work with **AEM as a Cloud Service** and is backwards compatible with **AEM 6.5.4+** and **AEM 6.4.8+**.

## Latest Code

All of the tutorial code can be found on [GitHub](https://github.com/adobe/aem-guides-wknd-spa).

The [latest code base](https://github.com/adobe/aem-guides-wknd-spa/releases) is available as downloadable AEM Packages.

## Prerequisites

Before starting this tutorial, you'll need the following:

* A basic knowledge of HTML, CSS, and JavaScript
* Basic familiarity with [React](https://reactjs.org/tutorial/tutorial.html)

*While not required, it is beneficial to have a basic understanding of [developing traditional AEM Sites components](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html).*

## Local Development Environment {#local-dev-environment}

A local development environment is necessary to complete this tutorial. Screenshots and video are captured using the AEM as a Cloud Service SDK running on a Mac OS environment with [Visual Studio Code](https://code.visualstudio.com/) as the IDE. Commands and code should be independent of the local operating system, unless otherwise noted.

### Required software

* [AEM as a Cloud Service SDK](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/aem-runtime.html), [AEM 6.5.4+](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/aem-releases-updates.html?lang=en#aem-65) or [AEM 6.4.8+](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/aem-releases-updates.html?lang=en#aem-64)
* [Java](https://downloads.experiencecloud.adobe.com/content/software-distribution/en/general.html)
* [Apache Maven](https://maven.apache.org/) (3.3.9 or newer)
* [Node.js](https://nodejs.org/en/) and [npm](https://www.npmjs.com/)

>[!NOTE]
>
> **New to AEM as a Cloud Service?** Check out the [following guide to setting up a local development environment using the AEM as a Cloud Service SDK](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html).
>
> **New to AEM 6.5?** Check out the [following guide to setting up a local development environment](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/set-up-a-local-aem-development-environment.html).

## Next Steps {#next-steps}

What are you waiting for?! Start the tutorial by navigating to the [Create Project](create-project.md) chapter and learn how to generate a SPA Editor enabled project using the AEM Project Archetype.
