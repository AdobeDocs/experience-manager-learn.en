---
title: Getting Started with React and AEM SPA Editor
seo-title: Getting Started with React and AEM SPA Editor
description: A multi-part tutorial on how to develop for the AEM SPA Editor. Walks through the implementation of a Single Page Application, written using React JS, that can be edited within Adobe Experience Manager. Covers foundational topics like project setup, component mapping, front end development tools, and application routing.
seo-description: A multi-part tutorial on how to develop for the AEM SPA Editor. Walks through the implementation of a Single Page Application, written using React JS, that can be edited within Adobe Experience Manager. Covers foundational topics like project setup, component mapping, front end development tools, and application routing.
uuid: 30b7a186-8e04-4c7d-9919-d87653bda128
contentOwner: dgordon
products: SG_EXPERIENCEMANAGER/6.4/SITES
discoiquuid: 48627403-961d-4370-b518-7e1b0b140c88

---

# Getting Started with React and AEM SPA Editor{#getting-started-with-react-and-aem-spa-editor}

## WKND Events for React and AEM SPA Editor {#wknd-events-for-react-and-aem-spa-editor}

![](assets/react-logo.png)

The goal for this multi-part tutorial is to teach a developer how to implement a Single Page Application in [React](https://reactjs.org/) that can edited in Adobe Experience Manager (AEM) with the [AEM SPA Editor.](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/spa-overview.html) The tutorial covers the end to end creation of the SPA and the integration with AEM.

## Overview {#overview}

In a real-world scenario the development activities will be broken down by persona, often involving a **Front End developer** and a **Back End developer**. Each task in the tutorial is labeled with a persona to gain a better idea of the separation of development activities. The tutorial is designed so that anyone can complete it end to end, however if a user wishes he or she can jump in to the tutorial at any stage.

The implementation is designed to work on **AEM 6.4 + SP2**. The SPA implementation is built using the [React JS framework](https://reactjs.org/). An equivalent tutorial and implementation using [Angular](https://angularjs.org/) is also [available](../angular/angular.md). The following modern web development tools are also used in the tutorial:

* [Node.js](https://nodejs.org/en/)
* [npm](https://www.npmjs.com/)
* [webpack](https://webpack.js.org/)
* [Scss](https://sass-lang.com/documentation/file.SCSS_FOR_SASS_USERS.html)
* [React Styleguidist](https://react-styleguidist.js.org/)

>[!NOTE]
>
>More parts of the tutorial are expected to be added in the near future, including:
>
>* Building a custom Map component using Google Maps API
>* Integration of Content Fragments
>* Extending the List Component
>

### Latest {#latest-download}

To test the latest code before jumping into the tutorial, download and install the below packages on a local AEM instance:

`latest-aem-guides-wknd-events.ui.apps-0.0.1-SNAPSHOT.zip`

`latest-aem-guides-wknd-events.ui.content-0.0.1-SNAPSHOT.zip`

![](assets/aem-final.gif) 

### Solution Packages {#solution-set}

Below contains the finished solution for each chapter in the tutorial:

Solutions - React Chapters 0-3

### Github {#github}

All of the code for the project can be found on Github in the [Adobe Experience Cloud](https://github.com/Adobe-Marketing-Cloud) organization:

[GitHub: WKND Events SPA Editor Project](https://github.com/Adobe-Marketing-Cloud/aem-guides-wknd-events)

In addition, each chapter of the tutorial has its own branch in GitHub. A user can begin the tutorial at any point by simply checking out the branch that corresponds to the previous part.

*Any issues or problems with the tutorial please create an [Issue on Github.](https://github.com/Adobe-Marketing-Cloud/aem-guides-wknd-events/issues)*

## Table of Contents - React {#table-of-contents}

Below is the listing of chapters in the tutorial:

* [Overview](react.md)
* [Chapter 0 - Project Setup](chapter-0.md)
* [Chapter 1 - Editable Components](chapter-1.md)
* [Chapter 2 - Front End Development](chapter-2.md)
* [Chapter 3 - Navigation and Routing](chapter-3.md)
* Chapter 4 - Custom Component (Coming Soon)

## Local Development Environment {#local-dev-env}

A local development environment is necessary to complete this tutorial. Screenshots and video are captured from a Mac OS environment but the commands and code used should be independent of the local operating system, unless otherwise noted.

**New to AEM?** Check out [how to set up a local AEM Development Environment](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/local-aem-dev-environment-article-setup.html) for more details and videos.

## Prerequisites {#prerequisites}

The following should be installed:

* [Java 1.8](https://www.oracle.com/technetwork/java/javase/downloads/index.html)
* [AEM 6.4 + SP2](https://helpx.adobe.com/experience-manager/6-4/release-notes/sp-release-notes.html)
* [Apache Maven](https://maven.apache.org/) (3.3.9 or newer)
* [Node.js v10+](https://nodejs.org/en/)
* [npm 6+](https://www.npmjs.com/)

Start by double checking that the above tools have been installed and available via the command line path. Open up a new terminal and run the following commands:

```shell
$ java -version
java version "1.8.+"
Java(TM) SE Runtime Environment (build 1.8.0_111-b14)
Java HotSpot(TM) 64-Bit Server VM (build 25.111-b14, mixed mode)
 
$ mvn -version
Apache Maven 3.3.9
Maven home: /Library/apache-maven-3.3.9
Java version: 1.8.0_111, vendor: Oracle Corporation
Java home: /Library/Java/JavaVirtualMachines/jdk1.8.0_111.jdk/Contents/Home/jre
 
$ node --version
v10.8.0
 
$ npm --version
6.2.0
```

### Integrated Development Environments {#integrated-development-environments}

Popular IDEs like Eclipse, IntelliJ, and Visual Studio code can be used when developing with AEM. Check out the [following guide for detailed instructions and setup](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/local-aem-dev-environment-article-setup.html).

See the following resources for setting these tools up locally:

* [Eclipse IDE with AEM Developer Tools](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/aem-eclipse.html)
* [IntelliJ with AEM IDE Tooling](https://plugins.jetbrains.com/plugin/9563-aem-ide-tooling-4-intellij)
* [Visual Studio - AEM Sync](https://marketplace.visualstudio.com/items?itemName=Yinkai15.aemsync)
* [AEM Repo Tool - Can be integrated with most IDEs or build tools](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/aem-repo-tool.html)

## Next Steps {#next-steps}

Start the tutorial!

* [Chapter 0 - Project Setup](chapter-0.md)

## Help! {#help}



```
Outline Notes

---
product: AEM
audience: developer
user-guide-title: AEM SPA WKND Tutorial
---

# AEM SPA WKND Tutorial {#aem-spa-wknd-tutorial}

+ [Introduction](getting-started-spa-wknd-tutorial-develop.md)
+ Angular and SPA {#angular-spa}
  + [Angular](angular/angular.md)
  + [Introduction](angular/chapter-0.md)
  + [Part 1](angular/chapter-1.md)
  + [Part 2](angular/chapter-2.md)
  + [Part 3](angular/chapter-3.md)
  + [Part 4](angular/chapter-4.md)
  + [Part 5](angular/chapter-5.md)
  + [Part 6](angular/chapter-6.md)
  + [Part 7](angular/chapter-7.md)
  + [Part 8](angular/chapter-8.md)
+ React and SPA {#react-spa}
  + [Introduction](react/react.md)
  + [1 - Project Setup](react/chapter-0.md)
    + [SPA Starter Kit](react/chapter-0.md)
    + [Hello World](textcomponent.md)
      + View the page
    + [Thumbnails](thumbnails.md)
  + [2 - Front-end Development Workflow](react/chapter-2.md)
    + [Proxy JSON](proxy.md)
    + [Mock JSON](mock.md)
  + [3 - Components](react/chapter-1.md)
    + [Component Mapping](container.md)
        + [App]
        + [Page]
        + [Text]
    + [Image Component](imagecomponent.md)
        + [Image JSON](imagejson.md) -->
        + [React Image Component](imagereact.md)
        + [AEM Image Component](aemimage.md)
  + [4 - Branding](blah.md)
    + [Styles](styles.md)
    + [Component Styles](header.md) -> Header, Image caption
    + [Responsive Grid](responsiveGrid.md)
  + [5 - List](react/chapter-3.md)
    + [List JSON]
    + [React List Component]
    + [AEM List Component]
    + [Header Update]()
  + [6 Custom Component]()
    + [JSON Contract]()
    + [React Component]()
    + [AEM Component]()
  + [7 Event Info]()
    + [Event Info JSON]()
    + [React Event Info Component]()
    + [AEM Event Info Component]()
  + [8 Event List]()
    + [Event List JSON]()
    + [React Event List Component]()
    + [AEM Event List Component]()
```
