---
title: Repository modernization
description: Learn about repository modernization, mutable and immutable content, package structure and the repository modernizer CLI tool.
version: Experience Manager as a Cloud Service
feature: Developer Tools
topic: Migration, Upgrade
role: Developer
level: Experienced
jira: KT-8630
thumbnail: 336958.jpeg
exl-id: e9bd9035-1f2d-4a34-a581-9c1ec2c7bc04
duration: 1305
TQID: https://experienceleague.adobe.com/Ia3aTtzWbWZT-SiWRby-jC9bFP20uiqff-CdphqngTM
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: f2d27a5f-0d67-4d85-8a24-86a8d8a3574b
    internal-label: Developer tools
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
---
# Repository modernization

Learn about repository modernization, mutable and immutable content, package structure and the repository modernizer CLI tool.

>[!VIDEO](https://video.tv.adobe.com/v/336958?quality=12&learn=on)

## Repository Modernizer Tool

![Repository Modernizer](./assets/repository-modernizer.png)

As part of refactoring your code base, use the [Repository Modernizer tool](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/repo-modernizer.html) to restructure a 6.x code base to a more modern structure.

## Key activities

* Use the [Adobe I/O Repository Modernizer](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#command-aio-aem-migrationrepository-modernizer) tool to restructure a project to match the expected structure of an AEM as a Cloud Service project.
* Manually adjust and fix any build errors in the updated code base.
* Set up a [local development environment](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html) and deploy the updated code base. Iterate until the project is in a stable state.
* Deploy the updated code base to an AEM as a Cloud Service development environment and continue to validate.
