---
title: Understanding Authentication support in AEM
seo-title: Understanding Authentication support in AEM
description: A consolidated view into the authentication (and occasionally authorization) mechanisms supported by AEM. 
seo-description: A consolidated view into the authentication (and occasionally authorization) mechanisms supported by AEM. 
uuid: 3adb0904-000b-423f-9d2e-13f1f0c56347
products: SG_EXPERIENCEMANAGER/6.2
products: SG_EXPERIENCEMANAGER/6.3
topic-tags: Foundation
discoiquuid: 71d6216c-1b94-418a-a753-787bab0b0a16
targetaudience: target-audience new
---

# Understanding Authentication Support in AEM{#understanding-authentication-support-in-aem}

A consolidated view into the authentication (and occasionally authorization) mechanisms supported by AEM. 

*The following table describes how users can authenticate into AEM.*

<!--I removed the border value. I remove the colspan and border values ad added two blank td values. spans aren't allowed. bob -->

<table> 
 <tbody>
  <tr>
   <td>Authentication</td> 
   <td>AEM 6.2</td> 
   <td>AEM 6.3</td> 
  </tr>
  <tr>
   <td><strong>AEM as the canonical identity provider</strong></td> 
   <td></td> 
   <td></td> 
  </tr>
  <tr>
   <td>Basic authentication</td> 
   <td>✔</td> 
   <td>✔</td> 
  </tr>
  <tr>
   <td>Forms-based</td> 
   <td>✔</td> 
   <td>✔</td> 
  </tr>
  <tr>
   <td>Token-based (w/ <a href="https://docs.adobe.com/docs/en/aem/6-3/administer/security/encapsulated-token.html" target="_blank">encapsulated token</a>)</td> 
   <td>✔</td> 
   <td>✔</td> 
  </tr>
  <tr>
   <td colspan="3"><strong>Non-AEM system as the canonical identity provider</strong></td> 
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/docs/en/aem/6-3/administer/security/ldap-config.html" target="_blank">LDAP</a></td> 
   <td>✔</td> 
   <td>✔</td> 
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/docs/en/aem/6-3/deploy/configuring/single-sign-on.html" target="_blank">SSO</a></td> 
   <td>✔</td> 
   <td>✔</td> 
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/docs/en/aem/6-3/administer/security/saml-2-0-authenticationhandler.html" target="_blank">SAML 2.0</a></td> 
   <td>✔</td> 
   <td>✔</td> 
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/ddc/en/gems/oauth-server-functionality-in-aem---embrace-federation-and-unlea.html" target="_blank">OAuth 1.0a &amp; 2.0</a></td> 
   <td>✔</td> 
   <td>✔</td> 
  </tr>
  <tr>
   <td><a href="http://sling.apache.org/documentation/the-sling-engine/authentication/authentication-authenticationhandler/openid-authenticationhandler.html" target="_blank">OpenID</a></td> 
   <td>⁕</td> 
   <td>⁕</td> 
  </tr>
 </tbody>
</table>

⁕ *Provided via community projects, but not directly supported by Adobe.*
