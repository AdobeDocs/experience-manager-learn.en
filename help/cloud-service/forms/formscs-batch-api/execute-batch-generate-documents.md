---
title: Execute the batch configuration
description: Start the document generation process by executing the batch
type: Documentation
role: Developer
level: Beginner, Intermediate
version: Experience Manager as a Cloud Service
feature: Output Service
topic: Development
jira: KT-9674
badgeVersions: label="AEM Forms as a Cloud Service" before-title="false"
exl-id: 17f91f81-96d8-49d6-b1e3-53d8899695ae
duration: 219
TQID: https://experienceleague.adobe.com/gockTWognINySBJOwinojEcHEJ0NrpBoDRnKgozaFXc
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
# Execute Batch Configuration

To run the batch make a POST request to following API

``` xml
<baseURL>/confi/<configName>/execution
```

This API expects an empty json object as a parameter in the request body.
This API returns a unique URL in the response header identified by **location** key.
A GET request to this unique URL will tell you the status of the batch execution

The following video demonstrates the triggering of the batch configuration

>[!VIDEO](https://video.tv.adobe.com/v/340242?quality=12&learn=on)
