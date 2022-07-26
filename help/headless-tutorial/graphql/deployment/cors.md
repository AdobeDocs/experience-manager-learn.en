---
title: CORS configuration for AEM GraphQL
description: Learn how to configure Cross-origin resource sharing (CORS) for use with AEM GraphQL.
version: Cloud Service
feature: GraphQL API
topic: Headless, Content Management
role: Developer, Architect
level: Intermediate
kt: 10587
thumbnail: KT-10587.jpg
mini-toc-levels: 2
---

# Cross-origin resource sharing (CORS) 

Adobe Experience Manager as a Cloud Service's Cross-Origin Resource Sharing (CORS) facilitates non-AEM web properties to make browser-based client-side calls to AEM's GraphQL APIs.

>[!TIP]
>
> The following configurations are examples. Ensure you adjust them to align to the requirements of myour project.



## CORS requirement

CORS is required for browser-based connections to AEM GraphQL APIs, when the client connecting to AEM is NOT served from the same origin (also known as host or domain) as AEM.

| Client type                 | Single-page app (SPA) | Web component/JS | Mobile    | Server to server |
|----------------------------:|:---------------------:|:-------------:|:---------:|:----------------:|
| Requires CORS configuration | &#10004;              | &#10004;      | &#10008;  | &#10008;         |

## OSGi configuration

The AEM CORS OSGi configuration factory defines the allow criteria for accepting CORS HTTP requests.

| Client connects to                   | AEM Author | AEM Publish   | AEM Preview   |
|-------------------------------------:|:----------:|:-------------:|:-------------:|
|Requires CORS OSGi configuration      | &#10004;   | &#10004;      | &#10004;      | 


The example below defines an OSGi configuration for AEM Publish (`../config.publish/..`), but can be added to [any supported runmode folder](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/configuring-osgi.html#runmode-resolution).

The key configuration properties are:

+ `alloworigin` and/or `alloworiginregexp` specifies the origin(s) the client connecting to AEM web runs on.
+ `allowedpaths` specifies specifies the URL path pattern(s) allowed from the specified origins. To support AEM GraphQL persisted queries, use the following pattern: `"/graphql/execute.json.*"`
+ `supportedmethods` specifies the allowed HTTP methods for the CORS requests. Add `GET`, to support AEM GraphQL persisted queries.

[Learn more about the CORS OSGi configuration.](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html)


This example configuration supports use of AEM GraphQL persisted queries. To use client-defined GraphQL queries, add a GraphQL endpoint URL in `allowedpaths` and `POST` to `supportedmethods`. 

+ `/ui.config/src/main/content/jcr_root/apps/wknd-examples/osgiconfig/config.publish/com.adobe.granite.cors.impl.CORSPolicyImpl~graphql.cfg.json`

```json
{
  "alloworigin":[
    "https://spa.external.com/"
  ],
  "alloworiginregexp":[
    "http://localhost:.*"
  ],
  "allowedpaths": [
    "/graphql/execute.json.*"
  ],
  "supportedheaders": [
    "Origin",
    "Accept",
    "X-Requested-With",
    "Content-Type",
    "Access-Control-Request-Method",
    "Access-Control-Request-Headers"
  ],
  "supportedmethods":[
    "GET",
    "HEAD"
  ],
  "maxage:Integer": 1800,
  "supportscredentials": false,
  "exposedheaders":[ "" ]
}
```


## Dispatcher configuration

AEM Publish (and Preview) service's Dispatcher must be configured to support CORS.

| Client connects to                   | AEM Author | AEM Publish   | AEM Preview   |
|-------------------------------------:|:----------:|:-------------:|:-------------:|
|Requires Dispatcher CORS configuration| &#10008;   | &#10004;      | &#10004;      | 

### Allow CORS headers on HTTP requests

Update the `clientheaders.any` file to allow the HTTP request headers `Origin`,  `Access-Control-Request-Method` and `Access-Control-Request-Headers` to be passed through to AEM, allowing the HTTP request to be processed by the [AEM CORS configuration](#osgi-configuration).

`dispatcher/src/conf.dispatcher.d/clientheaders/clientheaders.any`

```
# Allowing CORS headers to be passed through to the publish tier to support headless and SPA Editor use cases.
# https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS#the_http_request_headers

"Origin"
"Access-Control-Request-Method"
"Access-Control-Request-Headers"

$include "./default_clientheaders.any"
```

### Deliver CORS HTTP response headers

Configure dispatcher farm to cache **CORS HTTP response headers** to ensure they are included when AEM GraphQL persisted queries are served from Dispatcher cache by adding the `Access-Control-...` headers to the cache headers list.

+ `dispatcher/src/conf.dispatcher.d/available_farms/wknd.farm`

```
/publishfarm {
    ...
    /cache {
        ...
        # CORS HTTP response headers
        # https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS#the_http_response_headers
        /headers {
            ...
            "Access-Control-Allow-Origin"
            "Access-Control-Expose-Headers"
            "Access-Control-Max-Age"
            "Access-Control-Allow-Credentials"
            "Access-Control-Allow-Methods"
            "Access-Control-Allow-Headers"
        }
    ...
    }
...
}
```
