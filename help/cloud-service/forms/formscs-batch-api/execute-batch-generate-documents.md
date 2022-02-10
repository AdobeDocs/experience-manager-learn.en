---
title: Execute the batch configuration
description: Start the document generation process by executing the batch
type: Documentation
role: Developer
level: Beginner, Intermediate
version: Cloud Service
feature: Output Service
topic: Development
kt: 9674
exl-id: 17f91f81-96d8-49d6-b1e3-53d8899695ae
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

>[!VIDEO](https://video.tv.adobe.com/v/340242/?quality=12&learn=on)
