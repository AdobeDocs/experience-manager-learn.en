---
title: Configure AEM Forms Cummunication API
description: Configure OpenAPI-based AEM Forms Communication APIs for server-to-server authentication
type: Documentation
role: Developer
level: Beginner, Intermediate
version: Cloud Service
feature: Document Services
topic: Development
jira: KT-17479
badgeVersions: label="AEM Forms as a Cloud Service" before-title="false"
exl-id: b9c0b04b-6131-4752-b2f0-58e1fb5f40aa
---
# Configure OpenAPI-based AEM Forms Communication APIs on AEM Forms as a Cloud Service

## Prerequisites

*   Latest instance of AEM Forms as a Cloud Service.
*   All the necessary [product profiles are added to the environment.](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/aem-apis/invoke-openapi-based-aem-apis)

*   Enable AEM API access to the product profile as shown below
![product_profile1](assets/product-profiles1.png)
![product_profile](assets/product-profiles.png) 

## Create Adobe Developer Console Project

Login to [Adobe Developer Console](https://developer.adobe.com/console/) using your Adobe ID.
Create a new project by clicking on the appropriate icon
![new-project](assets/new-project.png)

Give a meaningful name to the project and click on Add API icon
![new-project](assets/new-project2.png)

Select Experience Cloud
![new-project3](assets/new-project3.png)
Select AEM Forms Communications API and click Next
![new-project4](assets/new-project4.png)

Make sure you have selected server-to-server authentication and click next
![new-project5](assets/new-project5.png)
Select the profiles and click on Save configured API button to save your settings
![new-project6](assets/new-project6.png)
Click into the OAuth Server-to-Server
![new-project7](assets/new-project7.png)
Copy the Client ID,Client Secret, and Scopes
![new-project8](assets/new-project8.png)

## Configure AEM instance to enable ADC Project communication

If you already have an AEM Forms project, [please follow these instructions](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/aem-apis/invoke-openapi-based-aem-apis) to enable the Adobe Developer Console Project's OAuth Server-to-Server credential ClientID to communicate with the AEM instance

If you do not have an AEM Forms project, please create an [AEM Forms Project by following this documentation.](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/forms/developing-for-cloud-service/getting-started) and then enable the Adobe Developer Console Project's OAuth Server-to-Server credential ClientID to communicate with the AEM instance [using this documentation.](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/aem-apis/invoke-openapi-based-aem-apis)


## Next Steps

[Generate Access Token](./generate-access-token.md)
