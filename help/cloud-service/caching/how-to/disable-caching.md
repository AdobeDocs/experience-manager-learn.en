---
title: How to disable CDN caching
description: Learn how to disable the caching of HTTP responses in AEM as a Cloud Service's CDN.
version: Cloud Service
feature: Operations, CDN Cache
topic: Administration, Performance
role: Admin, Architect, Developer
level: Beginner
doc-type: Tutorial
last-substantial-update: 2023-11-30
jira: KT-14224
thumbnail: KT-14224.jpeg
exl-id: 22b1869e-5bb5-437d-9cb5-2d27f704c052
duration: 116
---
# How to disable CDN caching

Learn how to disable the caching of HTTP responses in AEM as a Cloud Service's CDN. The caching of responses is controlled by `Cache-Control`, `Surrogate-Control`, or `Expires` HTTP response cache headers.

These cache headers are typically set in AEM Dispatcher vhost configurations using `mod_headers`, but can also be set in custom Java&trade; code running in AEM Publish itself.

## Default caching behavior

Review the default caching behavior for AEM Publish and Author when an [AEM Project Archetype](./enable-caching.md#default-caching-behavior) based AEM project is deployed.

## Disable caching

Turning off caching can have a negative impact on the performance of your AEM as a Cloud Service instance, so exercise caution when turning off default caching behavior. 

However there are some scenarios where you may want to disable caching, such as:

- Developing a new feature and want to see the changes immediately.
- Content is secure (meant only for authenticated users) or dynamic (shopping cart, order details) and should not be cached.

To disable caching, you can update the cache headers in two ways.

1. **Dispatcher vhost configuration:** Only available for AEM Publish.
1. **Custom Java&trade; code:** Available for both AEM Publish and Author.

Let's review each of these options.

### Dispatcher vhost configuration

This option is the recommended approach for disabling caching however it is only available for AEM Publish. To update the cache headers, use the `mod_headers` module and `<LocationMatch>` directive in the Apache HTTP Server's vhost file. The general syntax is as follows:

```
<LocationMatch "$URL$ || $URL_REGEX$">
    # Removes the response header of this name, if it exists. If there are multiple headers of the same name, all will be removed.
    Header unset Cache-Control
    Header unset Expires

    # Instructs the CDN to not cache the response.
    Header set Cache-Control "private"
</LocationMatch>
```

#### Example

To disable the CDN caching of the **CSS content types** for some troubleshooting purposes, follow these steps. 

Note that, to bypass the existing CSS cache, a change in the CSS file is required to generate a new cache key for the CSS file. 

1. In your AEM project, locate the desired vhsot file from `dispatcher/src/conf.d/available_vhosts` directory.
1. Update the vhost (e.g `wknd.vhost`) file as follows:

    ```
    <LocationMatch "^/etc.clientlibs/.*\.(css)$">
        # Removes the response header of this name, if it exists. If there are multiple headers of the same name, all will be removed.
        Header unset Cache-Control
        Header unset Expires

        # Instructs the CDN to not cache the response.
        Header set Cache-Control "private"
    </LocationMatch>
    ```

    The vhost files in `dispatcher/src/conf.d/enabled_vhosts` directory are **symlinks** to the files in `dispatcher/src/conf.d/available_vhosts` directory, so make sure to create symlinks if not present.
1. Deploy the vhost changes to desired AEM as a Cloud Service environment using the [Cloud Manager - Web Tier Config Pipeline](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/cicd-pipelines/introduction-ci-cd-pipelines.html?#web-tier-config-pipelines) or [RDE Commands](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/developing/rde/how-to-use.html?lang=en#deploy-apache-or-dispatcher-configuration).

### Custom Java&trade; code

This option is available for both AEM Publish and Author. To update the cache headers, use the `SlingHttpServletResponse` object in custom Java&trade; code (Sling servlet, Sling servlet filter). The general syntax is as follows:

```java
response.setHeader("Cache-Control", "private");
```
