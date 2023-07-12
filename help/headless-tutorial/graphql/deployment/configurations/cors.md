---
title: CORS configuration for AEM GraphQL
description: Learn how to configure Cross-origin resource sharing (CORS) for use with AEM GraphQL.
version: Cloud Service
feature: GraphQL API
topic: Headless, Content Management
role: Developer, Architect
level: Intermediate
kt: 10830
thumbnail: KT-10830.jpg
exl-id: 394792e4-59c8-43c1-914e-a92cdfde2f8a
---
# Cross-origin resource sharing (CORS) 

Adobe Experience Manager as a Cloud Service's Cross-Origin Resource Sharing (CORS) facilitates non-AEM web properties to make browser-based client-side calls to AEM's GraphQL APIs.

The following article describes how to configure _single-origin_ access to a specific set of AEM Headless endpoints via CORS. Single-origin means only single non-AEM domain accesses AEM, for example, https://app.example.com connecting to https://www.example.com. Multi-origin access may not work using this approach due to caching concerns.

>[!TIP]
>
> The following configurations are examples. Ensure you adjust them to align to the requirements of your project.

## CORS requirement

CORS is required for browser-based connections to AEM GraphQL APIs, when the client connecting to AEM is NOT served from the same origin (also known as host or domain) as AEM.

| Client type                               | [Single-page app (SPA)](../spa.md) | [Web Component/JS](../web-component.md) | [Mobile](../mobile.md)    | [Server-to-server](../server-to-server.md) |
|----------------------------:|:---------------------:|:-------------:|:---------:|:----------------:|
| Requires CORS configuration | &#10004;              | &#10004;      | &#10008;  | &#10008;         |

## OSGi configuration

The AEM CORS OSGi configuration factory defines the allow criteria for accepting CORS HTTP requests.

| Client connects to                   | AEM Author | AEM Publish   | AEM Preview   |
|-------------------------------------:|:----------:|:-------------:|:-------------:|
| Requires CORS OSGi configuration     | &#10004;   | &#10004;      | &#10004;      | 


The example below defines an OSGi configuration for AEM Publish (`../config.publish/..`), but can be added to [any supported run mode folder](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/configuring-osgi.html#runmode-resolution).

The key configuration properties are:

+ `alloworigin` and/or `alloworiginregexp` specifies the origins the client connecting to AEM web runs on.
+ `allowedpaths` specifies the URL path patterns allowed from the specified origins. 
    + To support AEM GraphQL persisted queries, add the following pattern: `/graphql/execute.json.*`
    + To support Experience Fragments, add the following pattern: `/content/experience-fragments/.*`
+ `supportedmethods` specifies the allowed HTTP methods for the CORS requests. Add `GET`, to support AEM GraphQL persisted queries (and Experience Fragments).

[Learn more about the CORS OSGi configuration.](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html)

This example configuration supports use of AEM GraphQL persisted queries. To use client-defined GraphQL queries, add a GraphQL endpoint URL in `allowedpaths` and `POST` to `supportedmethods`. 

+ `/ui.config/src/main/content/jcr_root/apps/wknd-examples/osgiconfig/config.publish/com.adobe.granite.cors.impl.CORSPolicyImpl~graphql.cfg.json`

```json
{
  "alloworigin":[
    "https://spa.external.com/"
  ],
  "alloworiginregexp":[
  ],
  "allowedpaths": [
    "/graphql/execute.json.*",
    "/content/experience-fragments/.*"
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
    "HEAD",
  ],
  "maxage:Integer": 1800,
  "supportscredentials": false,
  "exposedheaders":[ "" ]
}
```

### Authorized AEM GraphQL API requests

When accessing AEM GraphQL APIs that require authorization (typically AEM Author or protected content on AEM Publish) ensure the CORS OSGi configuration has the additional values:

+ `supportedheaders` also lists `"Authorization"`
+ `supportscredentials` is set to `true`

Authorized requests to AEM GraphQL APIs that require CORS configuration are unusual, as they typically occur in the context of [server-to-server apps](../server-to-server.md) and thus, do not require CORS configuration. Browser-based apps that require CORS configurations, such as [single-page apps](../spa.md) or [Web Components](../web-component.md), typically do use authorization as it is difficult to secure the credentials . 

For example, these two settings are set as follows in a `CORSPolicyImpl` OSGi factory configuration:

+ `/ui.config/src/main/content/jcr_root/apps/wknd-examples/osgiconfig/config/com.adobe.granite.cors.impl.CORSPolicyImpl~graphql.cfg.json`

```json
{ 
  ...
  "supportedheaders": [
    "Origin",
    "Accept",
    "X-Requested-With",
    "Content-Type",
    "Access-Control-Request-Method",
    "Access-Control-Request-Headers",
    "Authorization"
  ],
  ...
  "supportscredentials": true,
  ...
}
```

#### Example OSGi configuration

+ [An example of the OSGi configuration can be found in the WKND project.](https://github.com/adobe/aem-guides-wknd/blob/main/ui.config/src/main/content/jcr_root/apps/wknd/osgiconfig/config.publish/com.adobe.granite.cors.impl.CORSPolicyImpl~wknd-graphql.cfg.json)

## Dispatcher configuration

AEM Publish (and Preview) service's Dispatcher must be configured to support CORS.

| Client connects to                   | AEM Author | AEM Publish   | AEM Preview   |
|-------------------------------------:|:----------:|:-------------:|:-------------:|
|Requires Dispatcher CORS configuration| &#10008;   | &#10004;      | &#10004;      | 

### Allow CORS headers on HTTP requests

Update the `clientheaders.any` file to allow the HTTP request headers `Origin`,  `Access-Control-Request-Method`, and `Access-Control-Request-Headers` to be passed through to AEM, allowing the HTTP request to be processed by the [AEM CORS configuration](#osgi-configuration).

`dispatcher/src/conf.dispatcher.d/clientheaders/clientheaders.any`

```
# Allowing CORS headers to be passed through to the publish tier to support headless and SPA Editor use cases.
# https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS#the_http_request_headers

"Origin"
"Access-Control-Request-Method"
"Access-Control-Request-Headers"

$include "./default_clientheaders.any"
```

#### Example Dispatcher configuration

+ [An example of the Dispatcher _client headers_ configuration can be found in the WKND project.](https://github.com/adobe/aem-guides-wknd/blob/main/dispatcher/src/conf.dispatcher.d/clientheaders/clientheaders.any#L10-L12)


### Deliver CORS HTTP response headers

Configure Dispatcher farm to cache **CORS HTTP response headers** to ensure they are included when AEM GraphQL persisted queries are served from Dispatcher cache by adding the `Access-Control-...` headers to the cache headers list.

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

#### Example Dispatcher configuration

+ [An example of the Dispatcher _CORS HTTP response headers_ configuration can be found in the WKND project.](https://github.com/adobe/aem-guides-wknd/blob/main/dispatcher/src/conf.dispatcher.d/available_farms/wknd.farm#L109-L114)
