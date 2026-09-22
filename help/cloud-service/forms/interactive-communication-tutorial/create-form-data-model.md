---
title: Create Form Data Model for IC Document
description: Learn to create a Form Data Model in AEM Forms to dynamically retrieve data for Interactive Communication Document.
version: Experience Manager as a Cloud Service
feature: Interactive Communication
role: Developer
level: Intermediate
doc-type: Feature Video
duration: 170
last-substantial-update: 2026-02-20T00:00:00.000Z
jira: KT-20353
exl-id: 661afb90-4a6f-4974-b4cc-02b1ed12342f
TQID: 'https://experienceleague.adobe.com/N9heS2a09w1kM8Fhggc3UMniE7DqHJhgY0fZwTlS028'
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: a01bfd36-4ab8-4bf8-9dc0-5b45b890552e
    internal-label: APIs
---
# Create Form Data Model for IC Document

Create a Forms Data Model to integrate external data sources with Interactive Communication in Adobe AEM. This process involves setting up a RESTful service, uploading a Swagger file, and configuring service endpoints to dynamically retrieve and bind data. Learn how to securely connect to external services and test the model to ensure successful data retrieval.

A mock API server was implemented that simulates the Orders service for development and testing purposes. It exposes an endpoint to fetch orders for a given user (e.g., by user ID), returning predefined or dynamically generated order data in the same schema as the production API.

The swagger file used in creation of the form data model can be [downloaded from here](assets/UsersAndOrders.json)

>[!VIDEO](https://video.tv.adobe.com/v/3480005/?learn=on&enablevpops)

## Next Steps

[Create Template](./create-template.md)
