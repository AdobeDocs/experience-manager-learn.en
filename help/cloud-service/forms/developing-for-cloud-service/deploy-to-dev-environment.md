---
title: Deploy to development environment
description: Deploy the code from your cloud manager repository branch
solution: Experience Manager
type: Documentation
role: Developer
level: Beginner, Intermediate
version: Experience Manager as a Cloud Service
topic: Development
feature: Code Deployment
jira: KT-8851
exl-id: daf7d316-e9ec-41b5-89c8-fe4f4ada9701
duration: 23
TQID: https://experienceleague.adobe.com/eZfsMI0v8wOswNgGLrNZhokHfOlXNoSetQebGFrcj04
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
# Deploy to development environment

In the previous step we pushed our master branch from our local git repository into the MyFirstAF branch of the cloud manager repository.

The next step is to deploy the code to the development environment.
Login to cloud manager and select your program

Select the Deploy to Dev as shown below


![first-step](assets/deploy-first-step1.png)


Select Deployment Pipeline as shown
![first-step](assets/deploy1.png)

Select the source code and appropriate Git branch
![first-step](assets/deploy2.png)
Make sure you update your changes

Run the pipeline 
![run-pipeline](assets/run-pipeline.png)

Once the code is deployed, you should see the changes in your cloud service instance of AEM Forms.

## Next Steps

[Updating maven archetype project](./updating-project-archetype.md)
