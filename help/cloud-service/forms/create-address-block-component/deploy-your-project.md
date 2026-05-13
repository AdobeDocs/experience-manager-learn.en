---
title: Creating address component
description: Creating new address core component in AEM Forms as a Cloud Service
type: Documentation
role: Developer
level: Beginner, Intermediate
version: Experience Manager as a Cloud Service
feature: Adaptive Forms
topic: Development
jira: KT-15752
exl-id: be25be52-2914-4820-9356-678a326f8edc
TQID: https://experienceleague.adobe.com/V5PbjKY44ewKlGltmIsua-T2O-lx-FNfDF3mpVFPaMY
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
---
# Deploy your project

Before you start to deploy the project to your AEM Forms as a Cloud Service, it is recommended to deploy the project to your local cloud ready instance of AEM Forms.

## Synchronize changes with your AEM project 

Launch IntelliJ and navigate to adaptiveForm folder under the ``ui.apps`` folder as shown below
![intellij](assets/intellij.png)

Right click on ``adaptiveForm`` node and select New | Package
Make sure you add the name **addressblock** to the package

Right click the newly created package ``addressblock`` and select ``repo | Get Command`` as shown below
![repo-sync](assets/sync-repo.png)

This should sync the project with your local cloud ready AEM Forms instance. You can verify the .content.xml file to confirm the properties 
![after-sync](assets/after-sync.png)

## Deploy project to your local instance

Start a new command prompt window and navigate to the root folder of the project and build the project using the command shown below
![deploy](assets/build-project.png)

Once the project is successfully deployed, the 
Address component can now be used in an Adaptive Form

## Deploy the project to cloud environment

If everything looks good on your local development environment, the next step is to deploy to the [cloud instance using cloud manager.](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/forms/developing-for-cloud-service/push-project-to-cloud-manager-git)
