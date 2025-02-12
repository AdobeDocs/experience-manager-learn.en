---
title: Create an AEM site
description: Create a site in AEM Sites for Edge Delivery Services, editable using the Universal Editor.
version: Cloud Service
feature: Edge Delivery Services
topic: Development
role: Developer
level: Beginner
doc-type: Tutorial
jira: KT-15832
duration: 500
exl-id: d1ebcaf4-cea6-4820-8b05-3a0c71749d33
---
# Create an AEM site

The AEM site is where the website's content is edited, managed, and published from. To create an AEM site delivered via Edge Delivery Services and authored using Universal Editor, use the [Edge Delivery Services with AEM authoring site template](https://github.com/adobe-rnd/aem-boilerplate-xwalk/releases) to create a new site on AEM Author.

The AEM site is where the website's content is stored and authored. The final experience is a combination of the AEM site content with the [website's code](./1-new-code-project.md).

![New AEM Site for Edge Delivery Services and Universal Editor](./assets/2-new-aem-site/new-site.png)

Follow the [detailed steps outlined in documentation](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/edge-delivery/wysiwyg-authoring/edge-dev-getting-started#create-aem-site) to create a new AEM site.  Below is a summarized list of the steps, including the values used in this tutorial.
1. **Create a new site** in AEM Author. This tutorial uses the following site naming:
   * Site title: `WKND (Universal Editor)`
   * Site name: `aem-wknd-eds-ue`

     * The site name value must match the site path name [added to `paths.json`](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/edge-delivery/wysiwyg-authoring/path-mapping).

2. **Import the latest template** from the [Edge Delivery Services with AEM authoring site template](https://github.com/adobe-rnd/aem-boilerplate-xwalk/releases).
3. **Name the site** to match the GitHub repository name and set the GitHub URL as the repository's URL.

## Publish the new site to preview

After creating the site in AEM Author, publish it to the Edge Delivery Services preview making the content available to the [local development environment](./3-local-development-environment.md).

1. Log in to **AEM Author** and navigate to **Sites**.
2. Select the **new site** (`WKND (Universal Editor)`) and click **Manage Publications**.
3. Choose **Preview** under **Destinations** and click **Next**.
4. Under **Include Children Settings**, select **Include children**, deselect other options, and click **OK**.
5. Click **Publish** to publish the site's contents to preview.
6. Once published to preview, the pages are available on the Edge Delivery Services preview environment (the pages will not appear on the AEM Preview service).  
