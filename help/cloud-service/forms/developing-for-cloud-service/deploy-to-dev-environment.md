---
title: Deploy to development environment
description: Deploy the code from your cloud manager repository branch
solution: Experience Manager
type: Documentation
role: Developer
level: Beginner, Intermediate
version: Cloud Service
topic: Development
kt: 8851
exl-id: daf7d316-e9ec-41b5-89c8-fe4f4ada9701
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
