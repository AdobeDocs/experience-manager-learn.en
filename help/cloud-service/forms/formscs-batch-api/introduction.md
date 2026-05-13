---
title: Document generation using batch API in AEM Forms CS
description: Configure and trigger batch operations to generate documents.
type: Documentation
role: Developer
level: Beginner, Intermediate
version: Experience Manager as a Cloud Service
feature: Output Service
topic: Development
exl-id: 165e2884-4399-4970-81ff-1f2f8b041a10
badgeVersions: label="AEM Forms as a Cloud Service" before-title="false"
duration: 26
TQID: https://experienceleague.adobe.com/iDonTzutH3f7Zp61oyZWlq5bWqnPpEzb64a2kTxHS7g
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: a01bfd36-4ab8-4bf8-9dc0-5b45b890552e
    internal-label: APIs
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
---
# Introduction

A batch request is where tens, hundreds or thousands of similar documents are generated at one time. Example: A finance company may generate credit card statements to send to all of their customers.
Batch APIs (Asynchronous APIs) are suitable for scheduled high throughput multiple document generation use cases. These APIs generate documents in batches. For example, phone bills, credit card statements, and benefits statements generated every month.

To use AEM Forms CS batch operation API, the following configurations are needed

1. Configure Azure storage account
1. Create Azure storage backed cloud configuration
1. Create Batch data store configuration
1. Execute the Batch API

It is recommended you get familiar with the [API documentation](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/batch-api.yaml?lang=en) before proceeding to use this tutorial.
