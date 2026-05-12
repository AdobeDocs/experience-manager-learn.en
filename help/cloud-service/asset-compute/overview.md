---
title: Asset Compute microservices extensibility for AEM as a Cloud Service
description: This tutorial walks through the creation of a simple Asset Compute worker that creates an asset rendition by cropping the original asset to a circle, and applies configurable contrast and brightness. While the worker itself is basic, this tutorial uses it to explore creating, developing, and deploying a custom Asset Compute worker for use with AEM as a Cloud Service.
feature: Asset Compute Microservices
version: Experience Manager as a Cloud Service
doc-type: Tutorial
jira: KT-5802
thumbnail: KT-5802.jpg
topic: Integrations, Development
role: Developer
level: Intermediate, Experienced
last-substantial-update: 2022-08-15T00:00:00.000Z
exl-id: 575b12f9-b57f-41f7-bd39-56d242de4747
duration: 277
TQID: https://experienceleague.adobe.com/keTxcNWCic0pwFRC-oNbzhe43IR1aN-MmNVwpaXkFaU
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: a01bfd36-4ab8-4bf8-9dc0-5b45b890552e
    internal-label: APIs
  - id: ae478996-b206-4712-9b0c-dc78a2644453
    internal-label: Integrations
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
    internal-label: Metadata
---
# Asset Compute microservices extensibility

AEM as Cloud Service's Asset Compute microservices support the development and deployment of custom workers that are used to read, and manipulate binary data of assets stored in AEM, most commonly, to create custom asset renditions.

Whereas in AEM 6.x custom AEM Workflow processes were used to read, transform, and write back asset renditions, in AEM as a Cloud Service Asset Compute workers satisfy this need.

## What you will do

>[!VIDEO](https://video.tv.adobe.com/v/40965?quality=12&learn=on)

This tutorial walks through the creation of a simple Asset Compute worker that creates an asset rendition by cropping the original asset to a circle, and applies configurable contrast and brightness. While the worker itself is basic, this tutorial uses it to explore creating, developing, and deploying a custom Asset Compute worker for use with AEM as a Cloud Service.

### Objectives {#objective}

1. Provision and set up the necessary accounts and services to build and deploy an Asset Compute worker
1. Create and configure an Asset Compute project
1. Develop an Asset Compute worker that generates a custom rendition 
1. Write tests for, and learn how to debug the custom Asset Compute worker
1. Deploy the Asset Compute worker, and integrate it AEM as a Cloud Service Author service via Processing Profiles

## Set up

 Learn how to properly prepare for extending Asset Compute workers, and understand what services and accounts must be provisioned and configured, and software installed locally for development.

### Account and service provisioning{#accounts-and-services}

The following accounts and services require provisioning and access to in order to complete the tutorial, AEM as a Cloud Service Dev environment or Sandbox program, access to App Builder and  Microsoft Azure Blob Storage.

+ [Provision accounts and services](./set-up/accounts-and-services.md)

### Local development environment

Local development of Asset Compute projects requires a specific developer tool set, different from traditional AEM development, including: Microsoft Visual Studio Code, Docker Desktop, Node.js and supporting npm modules.
 
+ [Set up local development environment](./set-up/development-environment.md)

### App Builder

Asset Compute projects are specially defined App Builder projects, and as such, require access to App Builder in the Adobe Developer Console in order to set up and deploy them.

+ [Set up App Builder](./set-up/app-builder.md)

## Develop 

Learn how to create and configure an Asset Compute project and then develop a custom worker that generates a bespoke asset rendition.

### Create a new Asset Compute project

Asset Compute projects, which contain one or more Asset Compute workers, are generated using the the interactive Adobe I/O CLI. Asset Compute projects are specially structured App Builder projects, which are in turn Node.js projects. 

+ [Create a new Asset Compute project](./develop/project.md)

### Configure environment variables

Environment variables are maintained in the `.env` file for local development, and are used to provide Adobe I/O credentials and cloud storage credentials required for local development.

+ [Configure the environment variables](./develop/environment-variables.md)

### Configure the manifest.yml

Asset Compute projects contain manifests which define all the Asset Compute workers contained within the project, as well as what resources they have available when deployed to Adobe I/O Runtime for execution.

+ [Configure the manifest.yml](./develop/manifest.md)

### Develop a worker

Developing an Asset Compute worker is the core of extending Asset Compute microservices, as the worker contains the custom code that generates, or orchestrates, the generation of the resultant asset rendition.

+ [Develop an Asset Compute worker](./develop/worker.md)

### Use the Asset Compute Development Tool

The Asset Compute Development Tool provides a local Web harness for deploying, executing and previewing worker-generated renditions, supporting rapid and iterative Asset Compute worker development.

+ [Use the Asset Compute Development Tool](./develop/development-tool.md)

## Test and Debug

Learn how to test custom Asset Compute workers to be confident in their operation, and debug Asset Compute workers to understand and troubleshoot how the custom code is executed.

### Test a worker

Asset Compute provides a test framework for creating test suites for workers, making defining tests that ensure proper behavior is easy.

+ [Test a worker](./test-debug/test.md)

### Debug a worker

Asset Compute workers provide various levels of debugging from traditional `console.log(..)` output, to integrations with __VS Code__ and  __wskdebug__, allowing developers step through worker code as it executes in real time.

+ [Debug a worker](./test-debug/debug.md)

## Deploy

Learn how to integrate custom Asset Compute workers with AEM as a Cloud Service, by first deploying them to Adobe I/O Runtime and then invoking from AEM as a Cloud Service Author via AEM Assets' Processing Profiles.

### Deploy to Adobe I/O Runtime

Asset Compute workers must be deployed to Adobe I/O Runtime to be used with AEM as a Cloud Service.

+ [Using Processing Profiles](./deploy/runtime.md)

### Integrate workers via AEM Processing Profiles

Once deployed to Adobe I/O Runtime, Asset Compute workers can be registered in AEM as a Cloud Service via [Assets Processing Profiles](../../assets/configuring/processing-profiles.md). Processing Profiles are, in turn, applied to asset folders applying to the assets therein.

+ [Integrate with AEM Processing Profiles](./deploy/processing-profiles.md)

## Advanced

These abridged tutorials tackle more advanced use cases building upon foundational learnings established in the prior chapters.

+ [Develop a Asset Compute metadata worker](./advanced/metadata.md) that can write metadata back to the 

## Codebase on Github

The tutorial's codebase is available on Github at:

+ [adobe/aem-guides-wknd-asset-compute](https://github.com/adobe/aem-guides-wknd-asset-compute) @ master branch

The source code does not contain the required `.env` or `config.json` files. These must be added and configured using your [accounts and services](#accounts-and-services) information.

## Additional resources

The following are various Adobe resources that provide further information and useful APIs and SDKs for developing Asset Compute workers.

### Documentation

+ [Asset Compute Service documentation](https://experienceleague.adobe.com/docs/asset-compute/using/extend/understand-extensibility.html)
+ [Asset Compute Development Tool readme](https://github.com/adobe/asset-compute-devtool)
+ [Asset Compute example workers](https://github.com/adobe/asset-compute-example-workers)

### APIs and SDKs

+ [Asset Compute SDK](https://github.com/adobe/asset-compute-sdk)
    + [Asset Compute Commons](https://github.com/adobe/asset-compute-commons)
    + [Asset Compute XMP](https://github.com/adobe/asset-compute-xmp#readme)
+ [Adobe Cloud Blobstore Wrapper library](https://github.com/adobe/node-cloud-blobstore-wrapper)
+ [Adobe Node Fetch Retry library](https://github.com/adobe/node-fetch-retry)
+ [Asset Compute example workers](https://github.com/adobe/asset-compute-example-workers)
