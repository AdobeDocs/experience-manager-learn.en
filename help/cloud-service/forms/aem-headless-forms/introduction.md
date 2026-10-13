---
title: Render AEM Adaptive Forms Headlessly Using Node.js
description: Adobe Experience Manager (AEM) Forms provides APIs that allow Adaptive Forms to be consumed independently of the presentation layer. This makes it possible to author and manage forms in AEM while rendering them in a custom web application
solution: Experience Manager,Experience Manager Forms
type: Documentation
role: Developer
level: Beginner, Intermediate
version: Experience Manager as a Cloud Service
feature: Adaptive Forms
topic: Development
jira: KT-22838
---


Adobe Experience Manager (AEM) Forms provides APIs that allow Adaptive Forms to be consumed independently of the presentation layer. This makes it possible to author and manage forms in AEM while rendering them in a custom web application.

This code sample demonstrates a **Node.js and Express application** that retrieves an Adaptive Form definition from AEM Forms as JSON and dynamically renders the form using HTML and JavaScript.

The form structure, including panels, fields, labels, and drop-down options, is authored and managed in AEM Forms. The Node.js application acts as a lightweight proxy between the browser and AEM Forms, while the browser dynamically creates the user interface from the Adaptive Form JSON definition.

## Source Code

The complete source code for this sample is available on GitHub:

[View the AEM Headless Adaptive Form sample on GitHub](https://github.com/gbedekar489/aem-headless-adaptive-form)

To clone the repository:

```bash
git clone https://github.com/gbedekar489/aem-headless-adaptive-form.git
```

### Architecture

The sample uses the following architecture:

```text
AEM Adaptive Form
        |
        v
AEM Forms JSON API
        |
        v
Node.js / Express
        |
        v
Custom JavaScript Renderer
        |
        v
Headless Form UI
```