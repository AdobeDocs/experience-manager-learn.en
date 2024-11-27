---
title: Creating countries drop down list component
description: Create a countries drop down list component based on a aem forms core drop down component.
solution: Experience Manager, Experience Manager Forms
type: Documentation
role: Developer
level: Beginner, Intermediate
version: Cloud Service
topic: Development
feature: Adaptive Forms
badgeVersions: label="AEM Forms as a Cloud Service" before-title="false"
jira: KT-16517
exl-id: aef151bc-daf1-4abd-914a-6299f3fb58e4
---
# Create a countries drop down component based on a drop down component

Creating a new core component in Adobe Experience Manager (AEM) is an exciting process that involves several steps, including defining the component structure, customizing the dialog, and implementing a Sling model for dynamic functionality.

By the end of this tutorial, you'll have mastered how to:

* Create and use a Sling model to fetch data dynamically.
* Customize the cq-dialog by adding new fields and hiding others.
* Define a robust component structure tailored for reuse.

The component, named "Countries", will allow users to select a continent and dynamically populate a dropdown with countries corresponding to the chosen continent. This will be built on the foundation of the out-of-the-box dropdown list component, enhanced for this specific use case.

Let's dive in and create this dynamic and powerful component!

## Prerequisites

Building a new core component in Adobe Experience Manager (AEM) requires meeting several prerequisites to ensure a smooth development process. Here's what you'll need before getting started:

* AEM Development Environment: A functional cloud ready installation running localy
* Access to AEM Development tools such as Visual Studio Code or IntelliJ
* MAven setup and and AEM project with latest Archetype
* Basic knowledge of AEM concepts
* Basic tools and setup such as Git repository,right version of JDK


## Next Steps

[Create component structure](./component.md)
