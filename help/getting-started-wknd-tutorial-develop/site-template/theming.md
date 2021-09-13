---
title: Theming workflow
seo-title: Getting Started with AEM Sites - Theming workflow
description: Learn how to update the theme sources of an Adobe Experience Manager Site to apply brand specific styles. Learn how to use a proxy server to view a live preview of CSS and Javascript updates. This tutorial will also cover how to deploy theme updates to an AEM Site using GitHub Actions.
sub-product: sites
version: Cloud Service
type: Tutorial
feature: Core Components
topic: Content Management, Development
role: Developer
level: Beginner
kt: 7498
thumbnail: KT-7498.jpg
exl-id: 98946462-1536-45f9-94e2-9bc5d41902d4
---
# Theming workflow {#theming}

>[!CAUTION]
>
> The quick site creation features showcased here will be released in the second half of 2021. The related documentation is available for preview purposes.

In this chapter we will update the theme sources of an Adobe Experience Manager Site to apply brand specific styles. We will earn how to use a proxy server to view a preview of CSS and Javascript updates as we code against the live site.. This tutorial will also cover how to deploy theme updates to an AEM Site using GitHub Actions. 

In the end our site will be updated to include styles to match the WKND brand.

## Prerequisites {#prerequisites}

This is a multi-part tutorial and it is assumed that the steps outlined in the [Page Templates](./page-templates.md) chapter have been completed.

## Objectives

1. Learn how the theme sources for a site can be downloaded and modified.
1. Learn how code against the live site for a real-time preview.
1. Understand the end-to-end workflow of delivering compiled CSS and JavaScript updates as part of a theme using GitHub Actions.

## Update a theme {#theme-update}

Next, make changes to the theme sources so that the site matches the look and feel of the WKND Brand.

>[!VIDEO](https://video.tv.adobe.com/v/332918/?quality=12&learn=on)

High level steps for the video:

1. Create a local user in AEM for use with a proxy development server.
1. Download the theme sources from AEM and open using a local IDE, like VSCode.
1. Modify the theme sources and use a proxy dev server to preview CSS and JavaScript changes in real time.
1. Update the theme sources so that the magazine article matches the WKND branded styles and mockups.

### Solution Files

Download the finished styles for the [WKND Theme](assets/theming/WKND-THEME-src.zip)

## Deploy a theme {#deploy-theme}

Deploy updates to a theme to an AEM environment using GitHub Actions.

>[!VIDEO](https://video.tv.adobe.com/v/332919/?quality=12&learn=on)

High level steps for the video:

1. Add your theme sources project to [GitHub as a new repository](https://docs.github.com/en/github/importing-your-projects-to-github/adding-an-existing-project-to-github-using-the-command-line).
1. Create [a personal access token in GitHub](https://docs.github.com/en/github/authenticating-to-github/creating-a-personal-access-token) and save to a secure location.
1. Configure the GitHub Settings in your AEM environment to point to your GitHub repository and include your personal access token.
1. Create the following [encrypted secrets](https://docs.github.com/en/actions/reference/encrypted-secrets) in your GitHub Repository:
    * **AEM_SITE** - root of your AEM site (i.e `wknd`)
    * **AEM_URL** - url of your AEM Author environment
    * **GIT_TOKEN** - Personal access token from Step 2.
1. Run the GitHub Action: **Build and deploy Github artifacts**. This will have the downstream effect of running the action: **Update theme config on AEM with artifact id**, which will deploy the theme sources to the AEM environment as specified by `AEM_URL` and `AEM_SITE`.

### Example repos

There are a couple of example GitHub repos that can be used as a reference:

* [aem-site-template-basic-theme-e2e](https://github.com/adobe/aem-site-template-basic-theme-e2e) - Used as an example for "real-world" projects.
* [https://github.com/godanny86/wknd-theme](https://github.com/godanny86/wknd-theme) - Used as an example for those following the tutorial.

## Congratulations! {#congratulations}

Congratulations, you have just created just updated and deployed a theme to AEM!

### Next Steps {#next-steps}

Take a deeper dive in to AEM development and understand more of the underlying technology by creating a site using the [AEM Project Archetype](../project-archetype/overview.md).
