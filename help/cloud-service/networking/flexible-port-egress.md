---
title: Flexible port egress
description: Learn how to set up and use flexible port egress to support external connections from AEM as a Cloud Service to external services.
version: Cloud Service
feature: Security
topic: Development, Security
role: Architect, Developer
level: Intermediate
kt: 9350
thumbnail: KT-9350.jpeg
exl-id: 5c1ff98f-d1f6-42ac-a5d5-676a54ef683c
---
# Flexible port egress

Learn how to set up and use flexible port egress to support external connections from AEM as a Cloud Service to external services.

## What is Flexible port egress?

Flexible port egress allows for custom, specific port forwarding rules to be attached to AEM as a Cloud Service, allowing connections from AEM to external services to be made.

A Cloud Manager Program can only have a __single__ network infrastructure type. Ensure that dedicated egress IP address is the most [appropriate type of network infrastructure](./advanced-networking.md)  for your AEM as a Cloud Service before executing the following commands.

>[!MORELIKETHIS]
>
> Read the AEM as a Cloud Service [advanced network configuration documentation](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/security/configuring-advanced-networking.html#flexible-port-egress) for more details on flexible port egress.

## Prerequisites

The following are required when setting up flexible port egress:

+ Adobe Developer Console project with Cloud Manager API enabled and [Cloud Manager Business Owner permissions](https://developer.adobe.com/experience-cloud/cloud-manager/guides/getting-started/permissions/)
+ Access to [Cloud Manager API's authentication credentials](https://developer.adobe.com/experience-cloud/cloud-manager/guides/getting-started/authentication/)
  + Organization ID (aka IMS Org ID)
  + Client ID (aka API Key)
  + Access Token (aka Bearer Token)
+ The Cloud Manager Program ID
+ The Cloud Manager Environment IDs

For more details watch the following walkthrough for how to setup, configure, and obtain Cloud Manger API credentials, and how to use them to make a Cloud Manager API call.

>[!VIDEO](https://video.tv.adobe.com/v/342235/?quality=12&learn=on)

This tutorial uses `curl` to make the Cloud Manager API configurations. The provided `curl` commands assume a Linux/macOS syntax. If using the Windows command prompt, replace the `\` line-break character with `^`.

## Enable flexible port egress per program

Start by enabling the flexible port egress on AEM as a Cloud Service.

1. First, determine the region in which the Advanced Networking will be set up by using the Cloud Manager API [listRegions](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/) operation. The `region name` is required to make subsequent Cloud Manager API calls. Typically, the region the Production environment resides in is used.

    __listRegions HTTP request__

    ```shell
    $ curl -X GET https://cloudmanager.adobe.io/api/program/{programId}/regions \
        -H 'x-gw-ims-org-id: <ORGANIZATION_ID>' \
        -H 'x-api-key: <CLIENT_ID>' \
        -H 'Authorization: Bearer <ACCESS_TOKEN>' \
        -H 'Content-Type: application/json' 
    ```

1. Enable flexible port egress for a Cloud Manager Program using the Cloud Manager API [createNetworkInfrastructure](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/) operation. Use the appropriate `region` code obtained from the Cloud Manager API `listRegions` operation.

    __createNetworkInfrastructure HTTP request__

    ```shell
    $ curl -X POST https://cloudmanager.adobe.io/api/program/{programId}/networkInfrastructures \
        -H 'x-gw-ims-org-id: <ORGANIZATION_ID>' \
        -H 'x-api-key: <CLIENT_ID>' \ 
        -H 'Authorization: Bearer <ACCESS_TOKEN>' \
        -H 'Content-Type: application/json' \
        -d '{ "kind": "flexiblePortEgress", "region": "va7" }'
    ```

    Wait 15 minutes for the Cloud Manager Program to provision the network infrastructure.

1. Check that the environment has finished __flexible port egress__ configuration using the Cloud Manager API [getNetworkInfrastructure](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/getNetworkInfrastructure) operation, using the `id` returned from the  createNetworkInfrastructure HTTP request in the previous step.

     __getNetworkInfrastructure HTTP request__

    ```shell
    $ curl -X GET https://cloudmanager.adobe.io/api/program/{programId}/networkInfrastructure/{networkInfrastructureId} \
        -H 'x-gw-ims-org-id: <ORGANIZATION_ID>' \
        -H 'x-api-key: <CLIENT_ID>' \ 
        -H 'Authorization: Bearer <ACCESS_TOKEN>' \
        -H 'Content-Type: application/json'
    ```

    Verify that the HTTP response contains a __status__ of __ready__. If not yet ready recheck the status every few minutes.

## Configure flexible port egress proxies per environment

1. Enable and configure the __flexible port egress__ configuration on each AEM as a Cloud Service environment using the Cloud Manager API [enableEnvironmentAdvancedNetworkingConfiguration](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/) operation. 

    __enableEnvironmentAdvancedNetworkingConfiguration HTTP request__

    ```shell
    $ curl -X PUT https://cloudmanager.adobe.io/api/program/{programId}/environment/{environmentId}/advancedNetworking \
        -H 'x-gw-ims-org-id: <ORGANIZATION_ID>' \
        -H 'x-api-key: <CLIENT_ID>' \ 
        -H 'Authorization: Bearer <ACCESS_TOKEN>' \
        -H 'Content-Type: application/json' \
        -d @./flexible-port-egress.json
    ```

    Define the JSON parameters in a `flexible-port-egress.json` and provided to curl via `... -d @./flexible-port-egress.json`.

    [Download the example flexible-port-egress.json](./assets/flexible-port-egress.json). This file only an example. Configure your file as required based on the optional/required fields documented at [enableEnvironmentAdvancedNetworkingConfiguration](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/). 

    ```json
    {
        "portForwards": [
            {
                "name": "mysql.example.com",
                "portDest": 3306,
                "portOrig": 30001
            },
            {
                "name": "smtp.sendgrid.com",
                "portDest": 465,
                "portOrig": 30002
            }
        ]
    }
    ```

    For each `portForwards` mapping, the advanced networking defines the following forwarding rule:

    | Proxy host  | Proxy port |  | External host | External port | 
    |---------------------------------|----------|----------------|------------------|----------|
    | `AEM_PROXY_HOST` | `portForwards.portOrig` | &rarr; | `portForwards.name` | `portForwards.portDest` |

    If your AEM deployment __only__ requires HTTP/HTTPS connections (port 80/443) to external service, leave the `portForwards` array empty, as these rules are only required for non-HTTP/HTTPS requests.

1. For each environment, validate the egress rules are in effect using the Cloud Manager API [getEnvironmentAdvancedNetworkingConfiguration](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/) operation.

    __getEnvironmentAdvancedNetworkingConfiguration HTTP request__

    ```shell
    $ curl -X GET https://cloudmanager.adobe.io/api/program/{programId}/environment/{environmentId}/advancedNetworking \
        -H 'x-gw-ims-org-id: <ORGANIZATION_ID>' \
        -H 'Authorization: Bearer <ACCESS_TOKEN>' \
        -H 'x-api-key: <CLIENT_ID>' \ 
        -H 'Content-Type: application/json'
    ```

1. Flexible port egress configurations can be updated using the Cloud Manager API [enableEnvironmentAdvancedNetworkingConfiguration](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/) operation. Remember `enableEnvironmentAdvancedNetworkingConfiguration` is a `PUT` operation, so all rules must be provided with every invocation of this operation.

1. Now you can use the flexible port egress configuration in your custom AEM code and configuration.


## Connecting to external services over flexible port egress

With the flexible port egress proxy enabled, AEM code and configuration can use them to make calls to external services. There are two flavors of external calls that AEM treats differently:

1. HTTP/HTTPS calls to external services on non-standard ports
    + Includes HTTP/HTTPS calls made to services running on ports other than the standard 80 or 443 ports.
1. non-HTTP/HTTPS calls to external services
    + Includes any non-HTTP calls, such as connections with Mail servers, SQL databases, or services that run on other non-HTTP/HTTPS protocols.

HTTP/HTTPS requests from AEM on standard ports (80/443) are allowed by default and need no extra configuration or considerations.


### HTTP/HTTPS on non-standard ports

When creating HTTP/HTTPS connections to non-standard ports (not-80/443) from AEM, the connections must be made through special host and ports, provided via placeholders.

AEM provides two sets of special Java™ system variables that map to AEM's HTTP/HTTPS proxies.

| Variable name | Use | Java™ code | OSGi configuration | 
| - |  - | - | - |
| `AEM_PROXY_HOST` | Proxy host for both HTTP/HTTPS connections | `System.getenv().getOrDefault("AEM_PROXY_HOST", "proxy.tunnel")` | `$[env:AEM_PROXY_HOST;default=proxy.tunnel]` |
| `AEM_HTTP_PROXY_PORT` | Proxy port for HTTPS connections (set fallback to `3128`) | `System.getenv().getOrDefault("AEM_HTTP_PROXY_PORT", 3128)` | `$[env:AEM_HTTP_PROXY_PORT;default=3128]` |
| `AEM_HTTPS_PROXY_PORT` | Proxy port for HTTPS connections (set fallback to `3128`) | `System.getenv().getOrDefault("AEM_HTTPS_PROXY_PORT", 3128)` | `$[env:AEM_HTTPS_PROXY_PORT;default=3128]` |

When making HTTP/HTTPS calls to external services on non-standard ports, no corresponding `portForwards` must be defined using the Cloud Manager API `enableEnvironmentAdvancedNetworkingConfiguration` operation, as the port forwarding "rules" are defined "in code".

>[!TIP]
>
> See AEM as a Cloud Service's flexible port egress documentation for [the full set of routing rules](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/security/configuring-advanced-networking.html#flexible-port-egress-traffic-routing).

#### Code examples

<table>
<tr>
<td>
    <a  href="./examples/http-on-non-standard-ports-flexible-port-egress.md"><img alt="HTTP/HTTPS on non-standard ports" src="./assets/code-examples__http.png"/></a>
    <div><strong><a href="./examples/http-on-non-standard-ports-flexible-port-egress.md">HTTP/HTTPS on non-standard ports</a></strong></div>
    <p>
        Java™ code example making HTTP/HTTPS connection from AEM as a Cloud Service to an external service on non-standard HTTP/HTTPS ports.
    </p>
</td>   
<td></td>   
<td></td>   
</tr>
</table>

### Non-HTTP/HTTPS connections to external services

When creating non-HTTP/HTTPS connections (ex. SQL, SMTP, and so on) from AEM, the connection must be made through a special host name provided by AEM.

| Variable name | Use | Java™ code | OSGi configuration | 
| - |  - | - | - |
| `AEM_PROXY_HOST` | Proxy host for non-HTTP/HTTPS connections | `System.getenv().getOrDefault("AEM_PROXY_HOST", "proxy.tunnel")` | `$[env:AEM_PROXY_HOST;default=proxy.tunnel]` |


Connections to external services are then called through the `AEM_PROXY_HOST` and the mapped port (`portForwards.portOrig`), which AEM then routes to the mapped external hostname (`portForwards.name`) and port (`portForwards.portDest`).

| Proxy host  | Proxy port |  | External host | External port | 
|---------------------------------|----------|----------------|------------------|----------|
| `AEM_PROXY_HOST` | `portForwards.portOrig` | &rarr; | `portForwards.name` | `portForwards.portDest` |

#### Code examples

<table><tr>
   <td>
      <a  href="./examples/sql-datasourcepool.md"><img alt="SQL connection using JDBC DataSourcePool" src="./assets/code-examples__sql-osgi.png"/></a>
      <div><strong><a href="./examples/sql-datasourcepool.md">SQL connection using JDBC DataSourcePool</a></strong></div>
      <p>
            Java™ code example connecting to external SQL databases by configuring AEM's JDBC datasource pool.
      </p>
    </td>   
   <td>
      <a  href="./examples/sql-java-apis.md"><img alt="SQL connection using Java APIs" src="./assets/code-examples__sql-java-api.png"/></a>
      <div><strong><a href="./examples/sql-java-apis.md">SQL connection using Java™ APIs</a></strong></div>
      <p>
            Java™ code example connecting to external SQL databases using Java™'s SQL APIs.
      </p>
    </td>   
   <td>
      <a  href="./examples/email-service.md"><img alt="Virtual Private Network (VPN)" src="./assets/code-examples__email.png"/></a>
      <div><strong><a href="./examples/email-service.md">E-mail service</a></strong></div>
      <p>
        OSGi configuration example using AEM's to connect to external e-mail services.
      </p>
    </td>   
</tr></table>
