---
title: HTTP/HTTPS connections on non-standard ports for dedicated egress IP address and VPN
description: Learn how to make HTTP/HTTPS requests from AEM as a Cloud Service to external web services running on non-standard ports for Dedicated Egress IP address and VPN
version: Cloud Service
feature: Security
topic: Development, Security
role: Architect, Developer
level: Intermediate
kt: 9354
thumbnail: KT-9354.jpeg
exl-id: a565bc3a-675f-4d5e-b83b-c14ad70a800b
---
# HTTP/HTTPS connections on non-standard ports for dedicated egress IP address and VPN

HTTP/HTTPS connections on non-standard ports (not 80/443) must be proxied out of AEM as a Cloud Service, however they do not need any special `portForwards` rules, and can use AEM's advanced networking's `AEM_HTTP_PROXY_HOST`, `AEM_HTTP_PROXY_PORT`, `AEM_HTTPS_PROXY_HOST`, and `AEM_HTTPS_PROXY_PORT`.

## Advanced networking support

The following code example is supported by the following advanced networking options.

Ensure the the [appropriate](../advanced-networking.md#advanced-networking) advanced networking configuration has been set up prior to following this tutorial.

| No advanced networking | [Flexible port egress](../flexible-port-egress.md) | [Dedicated egress IP address](../dedicated-egress-ip-address.md) | [Virtual Private Network](../vpn.md) |
|:-----:|:-----:|:------:|:---------:|
| &#10008; | &#10008; | &#10004; | &#10004; |

>[!CAUTION]
>
> This code example is only for [Dedicated Egress IP address](../dedicated-egress-ip-address.md) and [VPN](../vpn.md). A similar, but different code example is available for [HTTP/HTTPS connections on non-standard ports for Flexible Port Egress](./http-on-non-standard-ports-flexible-port-egress.md).

## Code example

This Java™ code example is of an OSGi service that can run in AEM as a Cloud Service that makes an HTTP connection to an external web server on 8080. Connections to HTTPS web servers use the `AEM_HTTPS_PROXY_HOST` and `AEM_HTTPS_PROXY_PORT` instead of  `AEM_HTTP_PROXY_HOST` and `AEM_HTTP_PROXY_PORT`.

>[!NOTE]
> It is recommended the [Java™ 11 HTTP APIs](https://docs.oracle.com/en/java/javase/11/docs/api/java.net.http/java/net/http/package-summary.html) are used to make HTTP/HTTPS calls from AEM.

+ `core/src/com/adobe/aem/wknd/examples/connections/impl/HttpExternalServiceImpl.java`

```java
package com.adobe.aem.wknd.examples.core.connections.impl;

import com.adobe.aem.wknd.examples.core.connections.ExternalService;
import org.osgi.service.component.annotations.Component;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import java.io.IOException;
import java.net.InetSocketAddress;
import java.net.ProxySelector;
import java.net.URI;
import java.net.http.HttpClient;
import java.net.http.HttpRequest;
import java.net.http.HttpResponse;
import java.time.Duration;

@Component
public class HttpExternalServiceImpl implements ExternalService {
    private static final Logger log = LoggerFactory.getLogger(HttpExternalServiceImpl.class);

    @Override
    public boolean isAccessible() {
        HttpClient client;

        // If the URL is http, use System.getenv("AEM_HTTP_PROXY_HOST") and System.getenv("AEM_HTTP_PROXY_PORT")
        // Else if the URL is https, us System.getenv("AEM_HTTPS_PROXY_HOST") and System.getenv("AEM_HTTPS_PROXY_PORT")

        if (System.getenv("AEM_HTTP_PROXY_HOST") != null) {
            // Create a ProxySelector that maps to AEM's provided AEM_HTTP_PROXY_HOST and AEM_HTTP_PROXY_PORT
            ProxySelector proxySelector = ProxySelector.of(
                    new InetSocketAddress(System.getenv("AEM_HTTP_PROXY_HOST"),
                            Integer.parseInt(System.getenv("AEM_HTTP_PROXY_PORT"))));
            // Create an HttpClient and provide the proxy selector that will use AEM's native HTTP proxy configuration
            client = HttpClient.newBuilder().proxy(proxySelector).build();
            log.debug("Using HTTPClient with AEM_HTTP_PROXY");
        } else {
            client = HttpClient.newBuilder().build();
            // If no proxy is set up (such as local dev)
            log.debug("Using HTTPClient without AEM_HTTP_PROXY");
        }

        // Prepare the full URI to request, note this will have the
        // - Scheme (http/https)
        // - External host name
        // - External port
        // The external service URI, including the scheme/host/port, is defined in code, rather than in Cloud Manager portForwards rules.
        URI uri = URI.create("http://api.example.com:8080/test.json");

        // Prepare the HttpRequest
        HttpRequest request = HttpRequest.newBuilder().uri(uri).timeout(Duration.ofSeconds(2)).build();

        // Send the HttpRequest using the configured HttpClient
        HttpResponse<String> response = null;
        try {
            // Request the URL
            response = client.send(request, HttpResponse.BodyHandlers.ofString());

            log.debug("HTTP response body: {} ", response.body());

            // Our simple example returns true is response is successful! (200 status code)
            return response.statusCode() == 200;
        } catch (IOException e) {
            return false;
        } catch (InterruptedException e) {
            return false;
        }
    }
}
```
