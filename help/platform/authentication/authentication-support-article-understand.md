---
title: Understanding Authentication support in AEM
seo-title: Understanding Authentication support in AEM
description: A consolidated view into the authentication (and occasionally authorization) mechanisms supported by AEM. 
seo-description: A consolidated view into the authentication (and occasionally authorization) mechanisms supported by AEM. 
uuid: 3adb0904-000b-423f-9d2e-13f1f0c56347
products: SG_EXPERIENCEMANAGER/6.2
products: SG_EXPERIENCEMANAGER/6.3
products: SG_EXPERIENCEMANAGER/6.4
products: SG_EXPERIENCEMANAGER/6.5
topic-tags: platform
discoiquuid: 71d6216c-1b94-418a-a753-787bab0b0a16
targetaudience: target-audience new
---

# Understanding Authentication Support in AEM{#understanding-authentication-support-in-aem}

A consolidated view into the authentication (and occasionally authorization) mechanisms supported by AEM. 

*The following table describes how users can authenticate into AEM.*

<table border="1" cellpadding="1" cellspacing="0" width="100%"> 
 <tbody>
  <tr>
   <td>Authentication</td> 
   <td style="text-align: center;">AEM 6.2</td> 
   <td style="text-align: center;">AEM 6.3</td> 
  </tr>
  <tr>
   <td colspan="3" style="text-align: center;"><strong>AEM as the canonical identity provider</strong></td> 
  </tr>
  <tr>
   <td>Basic authentication</td> 
   <td style="text-align: center;">✔<br /> </td> 
   <td style="text-align: center;">✔<br /> </td> 
  </tr>
  <tr>
   <td>Forms-based</td> 
   <td style="text-align: center;">✔<br /> </td> 
   <td style="text-align: center;">✔<br /> </td> 
  </tr>
  <tr>
   <td>Token-based (w/ <a href="https://docs.adobe.com/docs/en/aem/6-3/administer/security/encapsulated-token.html" target="_blank">encapsulated token</a>)</td> 
   <td style="text-align: center;">✔<br /> </td> 
   <td style="text-align: center;">✔<br /> </td> 
  </tr>
  <tr>
   <td colspan="3" style="text-align: center;"><strong>Non-AEM system as the canonical identity provider</strong></td> 
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/docs/en/aem/6-3/administer/security/ldap-config.html" target="_blank">LDAP</a></td> 
   <td style="text-align: center;">✔<br /> </td> 
   <td style="text-align: center;">✔<br /> </td> 
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/docs/en/aem/6-3/deploy/configuring/single-sign-on.html" target="_blank">SSO</a></td> 
   <td style="text-align: center;">✔<br /> </td> 
   <td style="text-align: center;">✔<br /> </td> 
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/docs/en/aem/6-3/administer/security/saml-2-0-authenticationhandler.html" target="_blank">SAML 2.0</a></td> 
   <td style="text-align: center;">✔<br /> </td> 
   <td style="text-align: center;">✔<br /> </td> 
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/ddc/en/gems/oauth-server-functionality-in-aem---embrace-federation-and-unlea.html" target="_blank">OAuth 1.0a &amp; 2.0</a></td> 
   <td style="text-align: center;">✔<br /> </td> 
   <td style="text-align: center;">✔<br /> </td> 
  </tr>
  <tr>
   <td><a href="http://sling.apache.org/documentation/the-sling-engine/authentication/authentication-authenticationhandler/openid-authenticationhandler.html" target="_blank">OpenID</a></td> 
   <td style="text-align: center;">⁕<br /> </td> 
   <td style="text-align: center;">⁕<br /> </td> 
  </tr>
 </tbody>
</table>

⁕ *Provided via community projects, but not directly supported by Adobe.*
