---
title: Create a code project
description: Create a code project for Edge Delivery Services, editable using the Universal Editor.
version: Experience Manager as a Cloud Service
feature: Edge Delivery Services
topic: Development
role: Developer
level: Beginner
doc-type: Tutorial
jira: KT-15832
duration: 900
exl-id: e1fb7a58-2bba-4952-ad53-53ecf80836db
TQID: https://experienceleague.adobe.com/2s43XBpChUC5TOJn3NXD9ohkNaCecW4GBoIvL9fl4Do
product_v2:
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: a453562e-8e72-4640-9a69-9cf95930bcee
    internal-label: Universal Editor
  - id: e2c1b6d3-bb7e-4fe8-8c72-f7b403298e91
    internal-label: Authoring
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
---
# Create an Edge Delivery Services code project

To build AEM websites for Edge Delivery Services and Universal Editor, use Adobe's [AEM Boilerplate XWalk project template](https://github.com/adobe-rnd/aem-boilerplate-xwalk). This template creates a new code project that contains the CSS and JavaScript used to create the website experience. This template creates a new GitHub repository, and loads it with Adobe's boilerplate code and configuration, providing a solid foundation for your AEM website project.

Remember, [AEM websites delivered by Edge Delivery Services](https://experienceleague.adobe.com/en/docs/experience-manager-learn/sites/edge-delivery-services/overview) only have client-side (browser) code. Website code is not executed in the AEM Author or Publish services.

![New Edge Delivery Services project](./assets/1-new-project/new-project.png)

Follow the [detailed steps outlined in documentation](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/edge-delivery/wysiwyg-authoring/edge-dev-getting-started#create-github-project) for creating an Edge Delivery Services code project whose content is editable in Universal Editor.  Below is a summarized list of the steps, including the values used in this tutorial.

1. **Set up a GitHub account.** If you're creating a project for your organization, make sure that the organization has a GitHub account, and you're a member.
2. **Create a new code project** using the [AEM Boilerplate XWalk project template](https://github.com/adobe-rnd/aem-boilerplate-xwalk).
3. **Install the AEM Code Sync GitHub app** and grant access to the repository. You can find the [app here](https://github.com/apps/aem-code-sync).
4. **Configure your new project's `fstab.yaml`** to point to the correct AEM Author service.

    * To experiment, you can use lower AEM as a Cloud Service environments (Stage or Dev), however real websites implementations should be configured to use a production AEM service.

5. **Edit your new project's `paths.json`** to map the AEM Author service path to your website's root.

This Git repository is cloned in the [local development environment](https://experienceleague.adobe.com/en/docs/experience-manager-learn/sites/edge-delivery-services/developing/universal-editor/3-local-development-environment) chapter, and where code is developed.

