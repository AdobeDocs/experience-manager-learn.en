---
title: Debugging AEM as a Cloud Service
description: on self-service, scalable, cloud infrastructure, which makes requires AEM developers to understand how to understand and debug various facets of AEM as a Cloud Service, from build and deploy to obtaining details of running AEM applications.
feature: Developer Tools
version: Experience Manager as a Cloud Service
doc-type: Tutorial
jira: KT-5346
topic: Development
role: Developer
level: Beginner, Intermediate
exl-id: 8092fbb4-234f-472e-a405-8a45734b7c65
duration: 60
TQID: https://experienceleague.adobe.com/ph7dEAgPXgV-wDxYyW0UhBho34r03Zm134l6Dytqm-s
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: f2d27a5f-0d67-4d85-8a24-86a8d8a3574b
    internal-label: Developer tools
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
topic_v2:
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
    internal-label: Insights
---
# Debugging AEM as a Cloud Service

AEM as a Cloud Service is the cloud-native way of leveraging the AEM applications. AEM as a Cloud Service runs on self-service, scalable, cloud infrastructure, which requires AEM developers to understand how to understand and debug various facets of AEM as a Cloud Service, from build and deploy to obtaining details of running AEM applications.

## Logs

Logs provide details into how your application is functioning in AEM as a Cloud Service, as well as insights into issues with deployments.

[Debugging AEM as a Cloud Service using logs](./logs.md)

## Build and deployment

Adobe Cloud Manager pipelines deploys AEM application through a series of steps to determine code quality and viability when deployed to AEM as a Cloud Service. Each of the steps may result in failure, making it important to understand how to debug builds in order to determine the root cause of, and how to resolve any failures.

[Debugging AEM as a Cloud Service build and deployment](./build-and-deployment.md)

## Developer Console

The Developer console provides a variety of information and introspections into AEM as a Cloud Service environments that are useful to understand how your application is recognized by and functions within AEM as a Cloud Service.

[Debugging AEM as a Cloud Service with the Developer Console](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/aem-developer-console)   

## Repository Browser

Repository Browser is a powerful tool that provides visibility into AEM's underlying data store, allowing for easy debugging of AEM as a Cloud Service environment. Repository Browser supports a read-only view of the resources and properties of AEM on Production, Stage, and Development, as well as Author, Publish, and Preview services.

[Debugging AEM as a Cloud Service with Repository Browser](./repository-browser.md)
