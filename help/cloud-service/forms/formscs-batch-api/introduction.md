---
title: Document generation using batch API in AEM Forms CS
description: Configure and trigger batch operations to generate documents.
type: Documentation
role: Developer
level: Beginner, Intermediate
version: Cloud Service
feature: Output Service
topic: Development
exl-id: 165e2884-4399-4970-81ff-1f2f8b041a10
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
