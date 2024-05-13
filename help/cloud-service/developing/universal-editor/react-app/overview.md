---
title: React app editing using Universal Editor
description: Learn how to edit the contents of a sample React app using Universal Editor.
version: Cloud Service
feature: Developer Tools, Headless
topic: Development, Content Management
role: Architect, Developer
level: Intermediate
doc-type: Tutorial
duration: 0
last-substantial-update: 2024-04-19
jira: KT-15359
thumbnail: KT-15359.png
---

# React app editing using Universal Editor

Learn how to edit the contents of a sample React app using Universal Editor. The contents are stored within Content Fragments in AEM and are fetched using GraphQL APIs.

This tutorial guides you through the process of setting up the local development environment, instrumenting the React app to edit its content, and editing the content using the Universal Editor.

## What you learn

This tutorial covers the following topics:

- A brief overview of Universal Editor
- Setting up the local development environment
    - **AEM SDK**: it provides the contents stored within Content Fragments for the React app using GraphQL APIs.
    - **React app**: a simple user interface that displays the contents from AEM.
    - **Universal Editor Service**: a _local copy of the Universal Editor service_ that binds Universal Editor and the AEM SDK.
- How to instrument the React app to edit the contents using Universal Editor
- How to edit the React app contents using Universal Editor


## Overview of Universal Editor

The Universal Editor empowers content authors and developers (front-end and backend), let's review some of the key benefits of Universal Editor:

- Built to edit headless and headful content in what-you-see-is-what-you-get (WYSIWYG) mode.
- Provides a consistent content editing experience across different front-end technologies like React, Angular, Vue, etc. Thus, the content authors can edit the content without worrying about the underlying front-end technology.
- Very minimal instrumentation is required to enable the Universal Editor in the front-end application. Thus, maximizing the developer's productivity and freeing them to focus on building the experience.
- Separation of concerns across three roles, content authors, front-end developers, and backend developers, allowing each role to focus on its core responsibilities.


## Sample React app

This tutorial uses [**WKND Teams**](https://github.com/adobe/aem-guides-wknd-graphql/tree/main/basic-tutorial#react-app---basic-tutorial---teampersons) as the sample React app. The **WKND Teams** React app displays a list of team members and their details. 

The Team details such as title, description, and team members are stored as _Team_ Content Fragments in AEM. Likewise, the Person details such as name, biography, and profile picture are stored as _Person_ Content Fragments in AEM.

The content for the React app is provided by AEM using GraphQL APIs and the user interface is built using two React components, `Teams` and `Person`.

A corresponding tutorial is available to learn how to build the **WKND Teams** React app. You can find the tutorial [here](https://experienceleague.adobe.com/en/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/overview). 

## Next Step

Learn how to [set up the local development environment](./local-development-setup.md).
