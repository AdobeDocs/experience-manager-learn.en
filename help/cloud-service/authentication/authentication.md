---
title: Authentication in AEM as a Cloud Service
description: Learn about authentication in AEM as a Cloud Service's.
version: Experience Manager as a Cloud Service
feature: Security
topic: Development, Integrations, Security
role: Developer
level: Intermediate
jira: KT-10436
thumbnail: KT-10436.png
last-substantial-update: 2022-10-14T00:00:00.000Z
exl-id: 4dba6c09-2949-4153-a9bc-d660a740f8f7
duration: 28
TQID: https://experienceleague.adobe.com/sMhfnt2IVKldWexct6smvKf--S8H0I-1PgPEjfqwGvI
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: ae478996-b206-4712-9b0c-dc78a2644453
    internal-label: Integrations
  - id: eb3ad9f8-54a2-45f3-abb1-d3976415a718
    internal-label: Personalization
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
topic_v2:
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
    internal-label: Security
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
    internal-label: Personalization
---
# AEM as a Cloud Service authentication

AEM as a Cloud Service supports multiple of authentication options and varies by service type. 

|                       | AEM Author | AEM Publish |
|-----------------------|:----------:|:-----------:|
| [Adobe IMS](../accessing/overview.md)<br>*(AEM Preview does not support Adobe IMS)*|  &#10004;  | &#10004;    |
| [OpenID Connect (OIDC)](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/security/open-id-connect-support-for-aem-as-a-cloud-service-on-publish-tier) | &#10008;  | &#10004;    |
| [SAML 2.0 via Adobe IMS](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/security/ims-support.html#how-to-set-up) |  &#10004;  | &#10004;    |
| [SAML 2.0](./saml-2-0.md) | &#10008;  | &#10004;    |
| [Single-sign On (SSO)](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/authoring/personalization/user-and-group-sync-for-publish-tier.html#integration-with-an-idp)  | &#10008;  | &#10004;    |
| [OAuth](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/authoring/personalization/user-and-group-sync-for-publish-tier.html#integration-with-an-idp)                 | &#10008;  | &#10004;    |
| [Token authentication](../../headless-tutorial/authentication/overview.md) |  &#10004;  | &#10004;    |
| Basic authentication | &#10008;  | &#10008;    |

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
