---
title: Understand Adobe Cloud Manager
description: Adobe Cloud Manager provides a simple, yet robust solution that allows easy management, introspects, and self-service of AEM environments.
sub-product: Experience Manager Cloud Manager, Experience Manager
doc-type: Feature Video
topic: Architecture
feature: Cloud Manager
role: Architect
level: Beginner
exl-id: 53279cbb-70c8-4319-b5bb-9a7d350a7f72
last-substantial-update: 2022-05-10
thumbnail: understand-cloud-manager.jpg
duration: 1026
---
# Understand Adobe Cloud Manager

Adobe Cloud Manager provides a simple, yet robust solution that allows easy management, introspects, and self-service of AEM environments.

## Cloud Manager Overview

This video series explores the key features of Cloud Manager's for AEM including:

* [Programs](#programs)
* [Environments](#environments)
* [Reports](#reports)
* [CI/CD Production Pipeline](#cicd-production-pipeline)
* [CI/CD Non-production Pipelines](#cicd-non-production-pipeline)
* [Activity](#activity)

For a complete overview, please review the [Cloud Manager User Guide](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/introduction.html).

## Programs {#programs}

[Cloud Manager Programs](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/getting-started/program-setup.html) represent sets of AEM environments supporting logical sets of business initiatives, typically corresponding to a purchased Service Level Agreement (SLA). For example, one Program may represent the AEM resources to support the global public Web sites, while another Program represents an internal Central DAM.

>[!VIDEO](https://video.tv.adobe.com/v/26313?quality=12&learn=on)

## Environments {#environments}

[Cloud Manager Environments](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/using/managing-environments.html) are composed of AEM Author, AEM Publish and Dispatcher instances. Different environments support roles and can be engaged using different CI/CD Pipelines (described below). Cloud Manager environments typically have one Production environment and one Stage environment.

>[!VIDEO](https://video.tv.adobe.com/v/26318?quality=12&learn=on)

## Reports {#reports}

[Cloud Manager Reports](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/using/monitoring-environments.html) provide a view into the Program's Environments and AEM instances through a set of charts that report on and track various metrics for each AEM instance.

>[!VIDEO](https://video.tv.adobe.com/v/26315?quality=12&learn=on)

## CI/CD Production Pipeline {#cicd-production-pipeline}

*[Use the CI/CD Pipeline in Adobe Cloud Manager](./use-the-cicd-pipeline-in-cloud-manager-for-aem.md) video series provides a deep dive into the Production Pipeline execution, including exploration of failing and successful deployments.*

>[!NOTE]
>
> Throughout these videos, the build, test, and deployment times have been sped up to reduce the time of the video. A complete pipeline execution typically takes 45 minutes or more (including the mandatory 30-minute performance testing), depending on the project size, number of AEM instances and UAT processes.

### Configuration

The [CI/CD Production Pipeline](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/using/pipelines/production-pipelines.html) configuration defines the trigger that initiates the pipeline, and parameters controlling the production deployment and performance test parameters.

>[!VIDEO](https://video.tv.adobe.com/v/26314?quality=12&learn=on)

### Pipeline Execution

The [CI/CD Production Pipeline](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/using/code-deployment.html) is used to build and deploy code through Stage to the Production environment, decreasing time to value.

>[!VIDEO](https://video.tv.adobe.com/v/26317?quality=12&learn=on)

## CI/CD Non-production Pipelines {#cicd-non-production-pipeline}

[CI/CD Non-production pipelines](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/using/pipelines/production-pipelines.html) are broken into two categories, Code Quality pipelines, and Deployment pipelines. Code Quality pipelines all code from a Git branch to build and be evaluated against Cloud Manager's code quality scan. Deployment pipelines support the automated deployment of code from the Git repository to any Non-production environment, meaning any provisioned AEM environment that is not Stage or Production.

>[!VIDEO](https://video.tv.adobe.com/v/26316?quality=12&learn=on)

## Activity {#activity}

Cloud Manager provides a consolidated view into a Program's activity, listing all CI/CD Pipeline executions, both production and non-production, allowing visibility into the past and present activity, and any activity's details can be reviewed.

Cloud Manager also integrates at a per-user level with [Adobe Experience Cloud Notifications](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/using/notifications.html), providing an omnipresent view into events and actions of interest.

>[!VIDEO](https://video.tv.adobe.com/v/26319?quality=12&learn=on)
