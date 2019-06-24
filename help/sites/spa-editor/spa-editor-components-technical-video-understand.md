---
title: Understanding SPA components in AEM SPA Editor
seo-title: Understanding SPA components in AEM SPA Editor
description: A video series explaining how SPA components, built with AEM's SPA Editor JS SDK's are powered by AEM content.
seo-description: A video series explaining how SPA components, built with AEM's SPA Editor JS SDK's are powered by AEM content.
page-status-flag: de-activated
uuid: c59f46b3-1725-4767-b52e-3347698db387
topic-tags: components
topic-tags: development
topic-tags: single-page-applications
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: spa
discoiquuid: 67cd77bc-c918-49b2-acb5-31da2584b4c7
index: y
internal: n
snippet: y
---

# Understanding SPA components in AEM SPA Editor{#understanding-spa-components-in-aem-spa-editor}

A video series explaining how SPA components, built with AEM's SPA Editor JS SDK's are powered by AEM content.

*Note that while this video uses React as the example, the same paradigms apply to AEM's SPA Editor JavaScript SDK for Angular 6+.*

## Recommended reading {#recommended-reading}

*This video series assumes a basic understanding of both React and the AEM SPA Editor.*

The following resources are recommended for review prior to watching this video series:

* [SPA walkthrough](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/spa-walkthrough.html) - Overview of single page applications in general.
* [SPA Editor feature video](https://helpx.adobe.com/experience-manager/kt/sites/using/spa-editor-framework-feature-video-use.html) - Video overview of the SPA Editor and We.Retail Journal app.
* [React.js tutorial](https://reactjs.org/tutorial/tutorial.html) - An introduction to developing with the React framework.

## Introduction {#introduction}

>[!VIDEO](https://video.tv.adobe.com/v/22798?quality=12)

## The AEM page and JSON content {#aem-json-content}

This video covers:

* The AEM page implementation used to deliver the SPA JavaScript and CSS.
* The AEM resource that provides the JSON content to the SPA.
* How multi-AEM Page content is exposed via JSON and resolved by the SPA.

>[!VIDEO](https://video.tv.adobe.com/v/22799?quality=9)

## Extending the Container component {#extending-the-container-component}

This video covers:

* The Container component provided by the SPA Editor JS SDK.
* The withModel helper function provided by the SPA Editor JS SDK.
* How the Container component resolves and dynamically instantiates SPA components based on AEM's JSON.

>[!VIDEO](https://video.tv.adobe.com/v/22800?quality=9)

## The SPA navigation component {#spa-navigation}

Using the We.Retail Journal's Navigation component, video covers:

* The mapTo helper function provided by the SPA Editor JS SDK.
* The JSON content injection into the (React) SPA component's props.cqModel.
* The AEM resource that provides the JSON content to the SPA.

>[!VIDEO](https://video.tv.adobe.com/v/22801?quality=12)

## The SPA image component {#spa-image}

Using the We.Retail Journal's Image component, this video covers:

* How the Container component is implicitly invoked based on the JSON content.
* The mapTo helper function provided by the SPA Editor JS SDK.
* The JSON content injection into the (React) SPA component's props.cqModel.

>[!VIDEO](https://video.tv.adobe.com/v/22806?quality=12)

## The SPA component's EditConfig {#spa-edit-config}

This video covers:

* The purpose and definition of the SPA Component's EditConfig object.

>[!VIDEO](https://video.tv.adobe.com/v/22807?quality=12)

## Supporting materials {#supporting-materials}

* [@adobe/cq-react-editable-components npm package](https://www.npmjs.com/package/@adobe/cq-react-editable-components)
* [@adobe/cq-angular-editable-components npm package](https://www.npmjs.com/package/@adobe/cq-angular-editable-components)

* [SPA Editor overview documentation](/content/help/en/experience-manager/6-4/sites/developing/using/spa-overview)
* [Sample React application structure documentation](/content/help/en/experience-manager/6-4/sites/developing/using/spa-getting-started-react#SampleApplicationStructure)

