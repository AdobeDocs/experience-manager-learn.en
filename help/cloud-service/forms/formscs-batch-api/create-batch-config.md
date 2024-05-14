---
title: Configure batch data configuration
description: Configure batch data configuration
type: Documentation
role: Developer
level: Beginner, Intermediate
version: Cloud Service
feature: Output Service
topic: Development
jira: KT-9673
exl-id: db25e5a2-e1a8-40ad-af97-35604d515450
duration: 233
---
# Create batch configuration

To use a batch API, create a batch configuration and execute a run based on that configuration. The following video shows a demonstration of creating batch configuration using the API

>[!NOTE]
>Please make sure the AEM user belongs to ```forms-users``` group to make API calls.


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
