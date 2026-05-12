---
title: Dispatcher filters for AEM GraphQL
description: Learn how to configure AEM Publish Dispatcher filters for use with AEM GraphQL.
version: Experience Manager as a Cloud Service
feature: GraphQL API
topic: Headless, Content Management
role: Developer
level: Intermediate
jira: KT-10829
thumbnail: kt-10829.jpg
exl-id: b76b7c46-5cbd-4039-8fd6-9f0f10a4a84f
duration: 48
TQID: https://experienceleague.adobe.com/RB55HK6lcamVX-n89dOI5d1ZI5nAX4c-PwdTsVhD9Yk
product_v2:
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
---
# Dispatcher filters 

Adobe Experience Manager as a Cloud Service uses AEM Publish Dispatcher filters to ensure only requests that should reach AEM do reach AEM. By default all requests are denied, and patterns for allowed URLs must be explicitly added.

| Client type                               | [Single-page app (SPA)](../spa.md) | [Web Component/JS](../web-component.md) | [Mobile](../mobile.md)    | [Server-to-server](../server-to-server.md) |
|------------------------------------------:|:---------------------:|:----------------:|:---------:|:----------------:|
| Requires Dispatcher filters configuration | &#10004;              | &#10004;         | &#10004;  | &#10004;         |

>[!TIP]
>
> The following configurations are examples. Ensure you adjust them to align to the requirements of your project.

## Dispatcher filter configuration

The AEM Publish Dispatcher filter configuration defines the URL patterns allowed to reach AEM, and must include the URL prefix for the AEM persisted query endpoint.

| Client connects to                        | AEM Author | AEM Publish   | AEM Preview   |
|------------------------------------------:|:----------:|:-------------:|:-------------:|
| Requires Dispatcher filters configuration | &#10008;   | &#10004;      | &#10004;      |

Add an `allow` rule with the URL pattern `/graphql/execute.json/*`, and ensure the file ID (for example `/0600`, is unique in the example farm file). 
This allows HTTP GET request to the persisted query endpoint, such as `HTTP GET /graphql/execute.json/wknd-shared/adventures-all` through to AEM Publish.

If using Experience Fragments in your AEM Headless experience, do the same for these paths.

+ `dispatcher/src/conf.dispatcher.d/filters/filters.any`

```
...
# Allow headless requests for Persisted Query endpoints
/0600 { /type "allow" /method '(POST|OPTIONS)' /url "/graphql/execute.json/*" }
# Allow headless requests for Experience Fragments
/0601 { /type "allow" /method '(GET|OPTIONS)' /url "/content/experience-fragments/*" }
...
```

### Example filters configuration

+ [An example of the Dispatcher filter can be found in the WKND project.](https://github.com/adobe/aem-guides-wknd/blob/main/dispatcher/src/conf.dispatcher.d/filters/filters.any#L28)
