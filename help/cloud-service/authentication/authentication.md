---
title: Authentication in AEM as a Cloud Service
description: Learn about authentication in AEM as a Cloud Service's.
version: Cloud Service
feature: Security
topic: Development, Integrations, Security
role: Architect, Developer
level: Intermediate
kt: 10436
thumbnail: KT-10436.jpeg
exl-id: 4dba6c09-2949-4153-a9bc-d660a740f8f7
---
# AEM as a Cloud Service authentication

AEM as a Cloud Service supports multiple of authentication options and varies by service type. 

|                       | AEM Author | AEM Publish | 
|-----------------------|:----------:|:-----------:|
| [Adobe IMS](../accessing/overview.md) |  &#10004;  | &#10008;    |
| [SAML 2.0](./saml-2-0.md) |  &#10008;  | &#10004;    |
| [Token authentication](../../headless-tutorial/authentication/overview.md) |  &#10004;  | &#10004;    |

## Authentication options

Click into the corresponding link below to for details on how to set up and use the authentication approach.

<table>
  <tr>
   <td>
      <a  href="../accessing/overview.md"><img alt="Adobe IMS" src="./assets/card--adobe-ims.png"/></a>
      <div><strong><a href="../accessing/overview.md">Adobe IMS</a></strong></div>
      <p>
          Manage AEM Author access using Adobe IMS via the Adobe Admin Console.
      </p>
    </td>   
   <td>
      <a  href="./saml-2-0.md"><img alt="SAML 2.0" src="./assets/card--saml-2-0.png"/></a>
      <div><strong><a href="./saml-2-0.md">SAML 2.0</a></strong></div>
      <p>
        Authenticate your web site's user to an IDP using AEM Publish service's SAML 2.0 integration.
      </p>
    </td>   
   <td>
      <a  href="../../headless-tutorial/authentication/overview.md"><img alt="Token" src="./assets/card--token.png"/></a>
      <div><strong><a href="../../headless-tutorial/authentication/overview.md">Token authentication</a></strong></div>
      <p>
        Allow applications and middleware to authenticate to AEM using an API service token.
      </p>
    </td>   
  </tr>
</table>
