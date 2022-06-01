---
title: Advanced networking
description: Learn about AEM as a Cloud Service's advanced networking options.
version: Cloud Service
feature: Security
topic: Development, Integrations, Security
role: Architect, Developer
level: Intermediate
kt: 9354
thumbnail: KT-9354.jpeg
exl-id: d1c1a3cf-989a-4693-9e0f-c1b545643e41
---
# Advanced networking

AEM as a Cloud Service provides advanced networking features that allows for precise management of connections to and from AEM as a Cloud Service programs. 

|                                                   | [Production Programs](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/programs/introduction-production-programs.html) | [Sandbox Programs](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/programs/introduction-sandbox-programs.html) |
|---------------------------------------------------|:-----------------------:|:---------------------:|
| Supports advanced networking                      | &#10004;                | &#10008;             |


AEM's advanced networking is comprised of three options for managing connectivity with external services. A Cloud Manager program, and its AEM as a Cloud Service environments, can only use a single type of advanced networking configuration at a time, so ensure that the most appropriate type is selected.

|                                   | HTTP/HTTPS on standard ports | HTTP/HTTPS on non-standard ports | Non-HTTP/HTTPS connections | Dedicated egress IP | "No-proxy hosts" list | Connect to VPN-protected services | Limit AEM Publish traffic by IP |
|-----------------------------------|:----------------------------:|:--------------------------------:|:--------------------------:|:-------------------:|:-------------------------------------:|:-------------------------------------:|:----:|
| __No advanced networking__                                            | &#10004; | &#10008; | &#10008; | &#10008; | &#10008; | &#10008; | &#10008; |
| [__Flexible port egress__](./flexible-port-egress.md)                 | &#10004; | &#10004; | &#10004; | &#10008; | &#10008; | &#10008; | &#10008; |
| [__Dedicated egress IP address__](./dedicated-egress-ip-address.md)   | &#10004; | &#10004; | &#10004; | &#10004; | &#10004; | &#10008; | &#10008; |
| [__Virtual Private Network__](./vpn.md)                               | &#10004; | &#10004; | &#10004; | &#10004; | &#10004; | &#10004; | &#10004; |


For more details on the considerations involved when selecting the appropriate advanced networking type, see [advanced networking documentation](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/configuring-advanced-networking.html).

## Advanced networking tutorials

Once the most appropriate advanced networking option based on your organization's need has been identified, click into the corresponding tutorial below to for step-by-step instructions and code samples.

<table>
  <tr>
   <td>
      <a  href="./flexible-port-egress.md"><img alt="Flexible port egress" src="./assets/flexible-port-egress.png"/></a>
      <div><strong><a href="./flexible-port-egress.md">Flexible port egress</a></strong></div>
      <p>
          Allow outbound AEM as a Cloud Service traffic on non-standard ports.
      </p>
    </td>   
   <td>
      <a  href="./dedicated-egress-ip-address.md"><img alt="FleDedicated egress IP address" src="./assets/dedicated-egress-ip-address.png"/></a>
      <div><strong><a href="./dedicated-egress-ip-address.md">Dedicated egress IP address</a></strong></div>
      <p>
        Originate outbound AEM as a Cloud Service traffic from a dedicated IP.
      </p>
    </td>   
   <td>
      <a  href="./vpn.md"><img alt="Virtual Private Network (VPN)" src="./assets/vpn.png"/></a>
      <div><strong><a href="./vpn.md">Virtual Private Network (VPN)</a></strong></div>
      <p>
        Secure traffic between a customer or vendor infrastructure and AEM as a Cloud Service.
      </p>
    </td>   
  </tr>
</table>

## Code examples

This collection provides examples of the configuration and code required to leverage advanced networking features for specific use cases.

Ensure the the appropriate [advanced networking configuration](#advanced-networking) has been set up prior to following these tutorials.

<table><tr>
   <td>
      <a  href="./examples/email-service.md"><img alt="Virtual Private Network (VPN)" src="./assets/code-examples__email.png"/></a>
      <div><strong><a href="./examples/email-service.md">E-mail service</a></strong></div>
      <p>
        OSGi configuration example using AEM's to connect to external e-mail services.
      </p>
    </td>  
    <td>
        <a  href="./examples/http-dedicated-egress-ip-vpn.md"><img alt="HTTP/HTTPS" src="./assets/code-examples__http.png"/></a>
        <div><strong><a href="./examples/http-dedicated-egress-ip-vpn.md">HTTP/HTTPS</a></strong></div>
        <p>
            Java™ code example making HTTP/HTTPS connection from AEM as a Cloud Service to an external service using HTTP/HTTPS protocol.
        </p>
    </td>
    <td>
      <a  href="./examples/sql-datasourcepool.md"><img alt="SQL connection using JDBC DataSourcePool" src="./assets//code-examples__sql-osgi.png"/></a>
      <div><strong><a href="./examples/sql-datasourcepool.md">SQL connection using JDBC DataSourcePool</a></strong></div>
      <p>
            Java™ code example connecting to external SQL databases by configuring AEM's JDBC datasource pool.
      </p>
    </td>   
    </tr><tr>
    <td>
      <a  href="./examples/sql-java-apis.md"><img alt="SQL connection using Java APIs" src="./assets/code-examples__sql-java-api.png"/></a>
      <div><strong><a href="./examples/sql-java-apis.md">SQL connection using Java™ APIs</a></strong></div>
      <p>
            Java™ code example connecting to external SQL databases using Java™'s SQL APIs.
      </p>
    </td>   
    <td>
      <a  href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/ip-allow-lists/apply-allow-list.html"><img alt="Applying an IP allow list" src="./assets/code_examples__vpn-allow-list.png"/></a>
      <div><strong><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/ip-allow-lists/apply-allow-list.html">Applying an IP allowlist</a></strong></div>
      <p>
            Configure an IP allowlist such that only VPN traffic can access AEM.
      </p>
    </td>
   <td>
      <a  href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/configuring-advanced-networking.html#restrict-vpn-to-ingress-connections"><img alt="Path-based VPN access restrictions to AEM Publish" src="./assets/code_examples__vpn-path-allow-list.png"/></a>
      <div><strong><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/configuring-advanced-networking.html#restrict-vpn-to-ingress-connections">Path-based VPN access restrictions to AEM Publish</a></strong></div>
      <p>
            Require VPN access for specific paths on AEM Publish.
      </p>
    </td>
</tr>
</table>
