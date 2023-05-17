---
title: AEM Headless first tutorial
description: Learn how to be an AEM Headless first application.
version: Cloud Service
feature: Content Fragments, GraphQL API
topic: Headless, Development
role: Developer
level: Intermediate
doc-type: Tutorial
last-substantial-update: 2023-05-16
jira: KT-13270
thumbnail: KT-13270.jpeg
---

# AEM Headless first tutorial

![AEM Headless First tutorial](./assets/overview/overview.png)

Welcome to the tutorial on building a web experience using React, fully powered by AEM Headless APIs and GraphQL. In this tutorial, we'll guide you through the process of creating a dynamic and interactive web application by combining the power of React, Adobe Experience Manager (AEM) Headless APIs, and GraphQL.

React is a popular JavaScript library for building user interfaces, known for its simplicity, reusability, and component-based architecture. AEM provides robust content management capabilities and exposes Headless APIs that allow developers to access content and data stored in AEM through a variety of channels and applications.

By leveraging AEM Headless APIs, you can retrieve content, assets, and data from your AEM instance and use them to power your React application. GraphQL, a flexible query language for APIs, provides an efficient and precise way to request specific data from your AEM instance, enabling a seamless integration between React and AEM.

Throughout this tutorial, we'll walk you through the step-by-step process of building a web experience using React and AEM Headless APIs with GraphQL. You'll learn how to set up your development environment, establish a connection between React and AEM, retrieve content using GraphQL queries, and render it dynamically in your web application.

We'll cover topics such as configuring your React project, establishing authentication with AEM, querying content from AEM using GraphQL, handling data in your React components, and optimizing performance by utilizing caching and pagination.

By the end of this tutorial, you'll have a solid understanding of how to leverage React, AEM Headless APIs, and GraphQL to build a powerful and engaging web experience. So, let's dive in and start building your next web application!

## Prerequisites

### Skills

+ Proficiency in React
+ Proficiency in GraphQL
+ Basic knowledge of AEM as a Cloud Service

### AEM as a Cloud Service

This tutorial requires Administrator access to an AEM as a Cloud Service environment.

### Software

+   [Node.js v16+](https://nodejs.org/en/)
    + Check your node version by running `node -v` from the command line
+   [npm 6+](https://www.npmjs.com/)
    + Check your npm version by running `npm -v` from the command line
+   [Git](https://git-scm.com/) 
    + Check your git version by running `git -v` from the command line

Use [node version manager (nvm)](https://github.com/nvm-sh/nvm) to address having multiple versions of node.js on the same machine.

Ensure you have privileges to install software globally on your computer.

## Next step

Now that your environment is setup, let's move on to the next step: [Setup and author content in AEM as a Cloud Service](./1-content-modeling.md)
