---
title: Theming workflow | AEM Quick Site Creation
description: Learn how to update the theme sources of an Adobe Experience Manager Site to apply brand specific styles. Learn how to use a proxy server to view a live preview of CSS and Javascript updates. This tutorial will also cover how to deploy theme updates to an AEM Site using Adobe Cloud Manager's Front End Pipeline.
version: Cloud Service
feature: Core Components
topic: Content Management, Development
role: Developer
level: Beginner
jira: KT-7498
thumbnail: KT-7498.jpg
doc-type: Tutorial
exl-id: 98946462-1536-45f9-94e2-9bc5d41902d4
recommendations: noDisplay, noCatalog
duration: 1275
---
# Theming workflow {#theming}

In this chapter we update the theme sources of an Adobe Experience Manager Site to apply brand specific styles. We learn how to use a proxy server to view a preview of CSS and Javascript updates as we code against the live site. This tutorial will also cover how to deploy theme updates to an AEM Site using Adobe Cloud Manager's Front End Pipeline.

In the end our site is updated to include styles to match the WKND brand.

## Prerequisites {#prerequisites}

This is a multi-part tutorial and it is assumed that the steps outlined in the [Page Templates](./page-templates.md) chapter have been completed.

## Objectives

1. Learn how the theme sources for a site can be downloaded and modified.
1. Learn how code against the live site for a real-time preview.
1. Understand the end-to-end workflow of delivering compiled CSS and JavaScript updates as part of a theme using Adobe Cloud Manager's Front End Pipeline.

## Update a theme {#theme-update}

Next, make changes to the theme sources so that the site matches the look and feel of the WKND Brand.

>[!VIDEO](https://video.tv.adobe.com/v/332918?quality=12&learn=on)

High level steps for the video:

1. Create a local user in AEM for use with a proxy development server.
1. Download the theme sources from AEM and open using a local IDE, like VSCode.
1. Modify the theme sources and use a proxy dev server to preview CSS and JavaScript changes in real time.
1. Update the theme sources so that the magazine article matches the WKND branded styles and mockups.

### Solution Files

Download the finished styles for the [WKND Sample Theme](assets/theming/WKND-THEME-src-1.1.zip)

## Deploy a theme using a Front End Pipeline {#deploy-theme}

Deploy updates to a theme to an AEM environment using Cloud Manager's Front End Pipeline.

>[!VIDEO](https://video.tv.adobe.com/v/338722?quality=12&learn=on)

High level steps for the video:

1. Create a new git [repository in Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/cloud-manager-repositories.html)
1. Add your theme sources project to the Cloud Manager git repository:

    ```shell
    $ cd <PATH_TO_THEME_SOURCES_FOLDER>
    $ git init -b main
    $ git add .
    $ git commit -m "initial commit"
    $ git remote add origin <CLOUD_MANAGER_GIT_REPOSITORY_URL>
    ```

1. Configure a [Front End Pipeline](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/cicd-pipelines/introduction-ci-cd-pipelines.html) in Cloud Manager to deploy the front end code.
1. Run the Front End Pipeline to deploy updates to the target AEM environment.

### Example repos

There are a couple of example GitHub repos that can be used as a reference:

* [aem-site-template-standard](https://github.com/adobe/aem-site-template-standard)
* [aem-site-template-basic-theme-e2e](https://github.com/adobe/aem-site-template-basic-theme-e2e) - Used as an example for "real-world" projects.

## Congratulations! {#congratulations}

Congratulations, you have just updated and deployed a theme to AEM!

### Next Steps {#next-steps}

Take a deeper dive in to AEM development and understand more of the underlying technology by creating a site using the [AEM Project Archetype](../project-archetype/overview.md).
