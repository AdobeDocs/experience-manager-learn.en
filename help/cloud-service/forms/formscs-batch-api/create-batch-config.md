---
title: Configure batch data configuration
description: Configure batch data configuration
type: Documentation
role: Developer
level: Beginner, Intermediate
version: Experience Manager as a Cloud Service
feature: Output Service
topic: Development
jira: KT-9673
badgeVersions: label="AEM Forms as a Cloud Service" before-title="false"
exl-id: db25e5a2-e1a8-40ad-af97-35604d515450
duration: 233
TQID: https://experienceleague.adobe.com/m16v6a8ffAfF8VH3agtllhc31gwiukqLt-ONbwrP7UU
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
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
---
# Create batch configuration

To use a batch API, create a batch configuration and execute a run based on that configuration. The following video shows a demonstration of creating batch configuration using the API

>[!NOTE]
>Please make sure the AEM user belongs to `forms-users` group to make API calls.


>[!VIDEO](https://video.tv.adobe.com/v/340241?quality=12&learn=on)

## Create Batch Configuration

The following is the POST endpoint for creating Batch config

``` xml
<baseURL>/config
```

The following is the minimum configuration that needs to be specified when creating batch configuration. This needs to be passed as JSON object in the body of the HTTP request

```
{
    "configName": "monthlystatements",
    "dataSourceConfigUri": "/conf/batchapi/settings/forms/usc/batch/batchapitutorial",
    "outputTypes": [
        "PDF"
    ],
    "template": "crx:///content/dam/formsanddocuments/formtemplates/custom_fonts.xdp"

}

```

## Verify Batch configuration

To verify the successful creation of batch configuration, you can make a GET request call to the following endpoint


``` xml
<baseURL>/config/monthlystatements
```

You only need to pass an empty JSON object in the body of the HTTP request
