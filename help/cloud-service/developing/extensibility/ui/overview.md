---
title: AEM UI extensibility
description: Learn about AEM UI extensibility using App Builder to create extensions.
feature: Developer Tools
version: Experience Manager as a Cloud Service
topic: Development
role: Developer
level: Beginner
recommendations: noDisplay
last-substantial-update: 2023-06-02
exl-id: 73f5d90d-e007-41a0-9bb3-b8f36a9b1547
duration: 50
---
# AEM UI extensibility {#aem-ui-extensibility}

Adobe Experience Manager (AEM) offers a powerful user interface (UI) for creating digital experiences. To customize and extend the UI, Adobe introduced App Builder. This tool empowers developers to enhance the user experience without complex coding using JavaScript and React.

App Builder provides an implementation layer for creating extensions that are bound to well define extension points in AEM. App Builder seamlessly integrates with AEM, allowing real-time preview and testing. Deploying changes to AEM is quick and streamlined. By using App Builder, developers save time and effort, enabling rapid prototyping and collaboration with stakeholders.

>[!CONTEXTUALHELP]
>id="aemcloud_learn_extensibility_app_builder"
>title="Getting started with Adobe Developer App Builder and AEM Headless"
>abstract="Learn how AEM App Builder enables developers to quickly customize and extend the AEM UIs with JavaScript and React, supporting seamless integration and rapid deployment."

## Develop an AEM UI extension

AEM's various UIs have different extension points, however the basic concepts are the same. 

The videos and walk-throughs provided linked below showcase the use of a Content Fragment Console extension to illustrate various activities. However, it's important to note that the concepts covered can be applied to all AEM UI extensions.

1. [Create an Adobe Developer Console project](./adobe-developer-console-project.md)
1. [Initialize an extension](./app-initialization.md)
1. [Register an extension](./extension-registration.md)
1. Implement an extension point

    Extension points and their implementations vary based on the UI being extended. 

   + [Develop a Content Fragments UI extension](./content-fragments/overview.md)
 
1. [Develop a modal](./modal.md)
1. [Develop an Adobe I/O Runtime action](./runtime-action.md)
1. [Verify an extension](./verify.md)
1. [Deploy an extension](./deploy.md)

## Adobe Developer documentation

Adobe Developer contains developer details on AEM UI extensibility. Please review the [Adobe Developer content for further technical details](https://developer.adobe.com/uix/docs/).
