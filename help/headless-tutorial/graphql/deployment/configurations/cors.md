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
last-substantial-update: 2023-08-08
---
# Cross-origin resource sharing (CORS) 

Adobe Experience Manager as a Cloud Service's Cross-Origin Resource Sharing (CORS) facilitates non-AEM web properties to make browser-based client-side calls to AEM's GraphQL APIs, and other AEM Headless resources.

>[!TIP]
>
> The following configurations are examples. Ensure you adjust them to align to the requirements of your project.

## CORS requirement

CORS is required for browser-based connections to AEM GraphQL APIs, when the client connecting to AEM is NOT served from the same origin (also known as host or domain) as AEM.

| Client type                               | [Single-page app (SPA)](../spa.md) | [Web Component/JS](../web-component.md) | [Mobile](../mobile.md)    | [Server-to-server](../server-to-server.md) |
|----------------------------:|:---------------------:|:-------------:|:---------:|:----------------:|
| Requires CORS configuration | &#10004;              | &#10004;      | &#10008;  | &#10008;         |

## AEM Author

Enabling CORS on AEM Author service is different from AEM Publish and AEM Preview services. AEM Author service requires an OSGi configuration to be added to the AEM Author service's run mode folder, and does not use a Dispatcher configuration.

### OSGi configuration

The AEM CORS OSGi configuration factory defines the allow criteria for accepting CORS HTTP requests.

| Client connects to                   | AEM Author | AEM Publish   | AEM Preview   |
|-------------------------------------:|:----------:|:-------------:|:-------------:|
| Requires CORS OSGi configuration     | &#10004;   | &#10008;      | &#10008;      | 


The example below defines an OSGi configuration for AEM Author (`../config.author/..`) so it is only active on AEM Author service.

The key configuration properties are:

+ `alloworigin` and/or `alloworiginregexp` specifies the origins the client connecting to AEM web runs on.
+ `allowedpaths` specifies the URL path patterns allowed from the specified origins. 
    + To support AEM GraphQL persisted queries, add the following pattern: `/graphql/execute.json.*`
    + To support Experience Fragments, add the following pattern: `/content/experience-fragments/.*`
+ `supportedmethods` specifies the allowed HTTP methods for the CORS requests. To support AEM GraphQL persisted queries (and Experience Fragments), add `GET` .
+ `supportedheaders` includes `"Authorization"` as requests to AEM Author should be authorized.
+ `supportscredentials` is set to `true` as request to AEM Author should be authorized.
  
[Learn more about the CORS OSGi configuration.](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html)

The following example supports use of AEM GraphQL persisted queries on AEM Author. To use client-defined GraphQL queries, add a GraphQL endpoint URL in `allowedpaths` and `POST` to `supportedmethods`. 

+ `/ui.config/src/main/content/jcr_root/apps/wknd-examples/osgiconfig/config.author/com.adobe.granite.cors.impl.CORSPolicyImpl~graphql.cfg.json`

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
    "Access-Control-Request-Headers",
    "Authorization"
  ],
  "supportedmethods":[
    "GET",
    "HEAD",
    "POST"
  ],
  "maxage:Integer": 1800,
  "supportscredentials": true,
  "exposedheaders":[ "" ]
}
```

#### Example OSGi configuration

+ [An example of the OSGi configuration can be found in the WKND project.](https://github.com/adobe/aem-guides-wknd/blob/main/ui.config/src/main/content/jcr_root/apps/wknd/osgiconfig/config.author/com.adobe.granite.cors.impl.CORSPolicyImpl~wknd-graphql.cfg.json)

## AEM Publish

Enabling CORS on AEM Publish (and Preview) services are different from the AEM Author service. AEM Publish service requires an AEM Dispatcher configuration to be added to the AEM Publish's Dispatcher configuration. AEM Publish does not use an [OSGi configuration](#osgi-configuration).

When configuring CORS on AEM Publish, ensure:

  + The `Origin` HTTP request header cannot be sent to AEM Publish service, by removing the `Origin` header (if previously added) from the AEM Dispatcher project's `clientheaders.any` file. Any `Access-Control-` headers should be removed from the `clientheaders.any` file and Dispatcher manages them, not AEM Publish service.
  + If you have any [CORS OSGi configurations](#osgi-configuration) enabled on your AEM Publish service, you have to remove them and migrate their configurations to the [Dispatcher vhost configuration](#set-cors-headers-in-vhost) outlined below.
  
### Dispatcher configuration

AEM Publish (and Preview) service's Dispatcher must be configured to support CORS.

| Client connects to                   | AEM Author | AEM Publish   | AEM Preview   |
|-------------------------------------:|:----------:|:-------------:|:-------------:|
|Requires Dispatcher CORS configuration| &#10008;   | &#10004;      | &#10004;      | 

#### Set Dispatcher environment variable

1. Open the global.vars file for AEM Dispatcher configuration, typically at `dispatcher/src/conf.d/variables/global.vars`.
2. Add the following to the file:

    ```
    # Enable CORS handling in the dispatcher
    #
    # By default, CORS is handled by the AEM publish server.
    # If you uncomment and define the ENABLE_CORS variable, then CORS will be handled in the dispatcher.
    # See the default.vhost file for a suggested dispatcher configuration. Note that:
    #   a. You will need to adapt the regex from default.vhost to match your CORS domains
    #   b. Remove the "Origin" header (if it exists) from the clientheaders.any file
    #   c. If you have any CORS domains configured in your AEM publish server origin, you have to move those to the dispatcher
    #       (i.e. accordingly update regex in default.vhost to match those domains)
    #
    Define ENABLE_CORS
    ```

#### Set CORS headers in vhost

1. Open the vhost configuration file for the AEM Publish service, in your Dispatcher configuration project, typically at `dispatcher/src/conf.d/available_vhosts/<example>.vhost`
2. Copy the contents of the `<IfDefine ENABLE_CORS>...</IfDefine>` block below, into your enabled vhost configuration file.

    ```{line-numbers="true"}
    <VirtualHost *:80>
      ...
      <IfModule mod_headers.c>
        ...
        <IfDefine ENABLE_CORS>
          ################## Start of CORS configuration ##################

          SetEnvIfExpr "req_novary('Origin') == ''" CORSType=none CORSProcessing=false
          SetEnvIfExpr "req_novary('Origin') != ''" CORSType=cors CORSProcessing=true CORSTrusted=false

          SetEnvIfExpr "req_novary('Access-Control-Request-Method') == '' && %{REQUEST_METHOD} == 'OPTIONS' && req_novary('Origin') != ''" CORSType=invalidpreflight CORSProcessing=false
          SetEnvIfExpr "req_novary('Access-Control-Request-Method') != '' && %{REQUEST_METHOD} == 'OPTIONS' && req_novary('Origin') != ''" CORSType=preflight CORSProcessing=true CORSTrusted=false
          SetEnvIfExpr "req_novary('Origin') -strcmatch '%{REQUEST_SCHEME}://%{HTTP_HOST}*'" CORSType=samedomain CORSProcessing=false

          # For requests that require CORS processing, check if the Origin can be trusted
          SetEnvIfExpr "%{HTTP_HOST} =~ /(.*)/ " ParsedHost=$1

          ################## Adapt regex to match CORS origin(s) for your environment
          SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://.*\.your-domain\.tld(:\d+)?$)#" CORSTrusted=true

          # Extract the Origin header
          SetEnvIfNoCase ^Origin$ ^(.*)$ CORSTrustedOrigin=$1

          # Flush If already set
          Header unset Access-Control-Allow-Origin
          Header unset Access-Control-Allow-Credentials

          # Trusted
          Header always set Access-Control-Allow-Credentials "true" "expr=reqenv('CORSTrusted') == 'true'"
          Header always set Access-Control-Allow-Origin "%{CORSTrustedOrigin}e" "expr=reqenv('CORSTrusted') == 'true'"
          Header always set Access-Control-Allow-Methods "GET" "expr=reqenv('CORSTrusted') == 'true'"
          Header always set Access-Control-Max-Age 1800 "expr=reqenv('CORSTrusted') == 'true'"
          Header always set Access-Control-Allow-Headers "Origin, Accept, X-Requested-With, Content-Type, Access-Control-Request-Method, Access-Control-Request-Headers" "expr=reqenv('CORSTrusted') == 'true'"

          # Non-CORS or Not Trusted
          Header unset Access-Control-Allow-Credentials "expr=reqenv('CORSProcessing') == 'false' || reqenv('CORSTrusted') == 'false'"
          Header unset Access-Control-Allow-Origin "expr=reqenv('CORSProcessing') == 'false' || reqenv('CORSTrusted') == 'false'"
          Header unset Access-Control-Allow-Methods "expr=reqenv('CORSProcessing') == 'false' || reqenv('CORSTrusted') == 'false'"
          Header unset Access-Control-Max-Age "expr=reqenv('CORSProcessing') == 'false' || reqenv('CORSTrusted') == 'false'"

          # Always vary on origin, even if its not there.
          Header merge Vary Origin

          # CORS - send 204 for CORS requests which are not trusted
          RewriteCond expr "reqenv('CORSProcessing') == 'true' && reqenv('CORSTrusted') == 'false'"
          RewriteRule "^(.*)" - [R=204,L]

          # Remove Origin before sending to AEM Publish
          RequestHeader unset Origin

          ################## End of CORS configuration ##################
        </IfDefine>
        ...
      </IfModule>
      ...
    </VirtualHost>
    ```

3. Match the desired Origins accessing your AEM Publish service by updating the regular expression in the line below. If multiple origins are required, duplicate this line and update for each origin/origin pattern.
      
    ```
    SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://.*.your-domain.tld(:\d+)?$)#" CORSTrusted=true
    ``` 

   + For example, to enable CORS access from origins:
  
     + Any subdomain on `https://example.com` 
     + Any port on `http://localhost` 
      
      Replace the line with the following two lines:

       ```
       SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://.*\.example\.com$)#" CORSTrusted=true
       SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(http://localhost(:\d+)?$)#" CORSTrusted=true
       ``` 

#### Example Dispatcher configuration

+ [An example of the Dispatcher configuration can be found in the WKND project.](https://github.com/adobe/aem-guides-wknd/blob/main/dispatcher/src/conf.d/available_vhosts/wknd.vhost)
