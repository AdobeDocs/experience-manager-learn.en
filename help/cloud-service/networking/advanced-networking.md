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
---

# Advanced networking

AEM as a Cloud Service provides three options for managing connectivity with external services. A Cloud Manager program, and its AEM as a Cloud Service environments, can only use a single type of advanced networking configuration at a time, so ensure that the most appropriate type is selected.

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
