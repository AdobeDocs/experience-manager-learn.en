---
title: HTTP/HTTPS connections for dedicated egress IP address and VPN
description: Learn how to make HTTP/HTTPS requests from AEM as a Cloud Service to external web services running for Dedicated Egress IP address and VPN
version: Experience Manager as a Cloud Service
feature: Security
topic: Development, Security
role: Developer
level: Intermediate
jira: KT-9354
thumbnail: KT-9354.jpeg
exl-id: a565bc3a-675f-4d5e-b83b-c14ad70a800b
duration: 70
TQID: https://experienceleague.adobe.com/J-DUQFg54PnezD6aTor7rvMviLwbhrt-AKYM30vqIhE
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
topic_v2:
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
    internal-label: Security
---
# HTTP/HTTPS connections for dedicated egress IP address and VPN

HTTP/HTTPS connections are automatically proxied out of AEM as a Cloud Service with dedicated egress IP address or VPN, and they do not need any special `portForwards` rules.

## Advanced networking support

The following code example is supported by the following advanced networking options.

Ensure the the [dedicated egress IP address or VPN](../advanced-networking.md#advanced-networking) advanced networking configuration has been set up prior to following this tutorial.

| No advanced networking | [Flexible port egress](../flexible-port-egress.md) | [Dedicated egress IP address](../dedicated-egress-ip-address.md) | [Virtual Private Network](../vpn.md) |
|:-----:|:-----:|:------:|:---------:|
| &#10008; | &#10008; | &#10004; | &#10004; |

>[!CAUTION]
>
> This code example is only for [Dedicated Egress IP address](../dedicated-egress-ip-address.md) and [VPN](../vpn.md). A similar, but different code example is available for [HTTP/HTTPS connections on non-standard ports for Flexible Port Egress](./http-on-non-standard-ports-flexible-port-egress.md).

## Code example

This Java™ code example is of an OSGi service that can run in AEM as a Cloud Service that makes an HTTP connection to an external web server on 8080. The HTTPS (or HTTP) connections are automatically proxied out of AEM as a Cloud Service, and do not require special development.

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
import java.net.URI;
import java.net.http.HttpClient;
import java.net.http.HttpRequest;
import java.net.http.HttpResponse;
import java.time.Duration;

@Component
public class HttpExternalServiceImpl implements ExternalService {
    private static final Logger log = LoggerFactory.getLogger(HttpExternalServiceImpl.class);

    // client with connection pool reused for all requests
    private HttpClient client = HttpClient.newBuilder().build();

    @Override
    public boolean isAccessible() {

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
