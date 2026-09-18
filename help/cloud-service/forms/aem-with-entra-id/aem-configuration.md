---
title: Secure AEM Forms Portal with Microsoft Entra ID
description: his use case demonstrates how Microsoft Entra External ID can serve as the customer identity provider for an AEM Forms banking portal.
solution: Experience Manager, Experience Manager Forms
type: Documentation
role: Developer
level: Beginner, Intermediate
version: Experience Manager as a Cloud Service
feature: Adaptive Forms
topic: Integrations, Development
jira: KT-22633
badgeIntegration: label="Integration" type="positive"
badgeVersions: label="AEM Forms as a Cloud Service" before-title="false"
---

## AEM Configuration

AEM can be configured for SAML 2.0 authentication by following Adobe's **SAML 2.0 Authentication for AEM as a Cloud Service** documentation:

[Configure SAML 2.0 Authentication for AEM as a Cloud Service](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/authentication/saml-2-0)

The Adobe documentation provides the general steps for configuring SAML authentication in AEM, including the SAML Authentication Handler, trust store, Dispatcher, CORS, and Referrer Filter configuration.

For this use case, the SAML configuration was adapted to use **Microsoft Entra External ID** as the identity provider. The following additional configuration was applied:

- The Microsoft Entra SAML signing certificate was imported into the **AEM Global Trust Store** and made available to the Publish environment.
- A **SAML Authentication Handler** was configured on AEM Publish with the Entra IdP URL, IdP identifier, certificate alias, service provider entity ID, and the Banking Application content paths that require authentication.
- The **Dispatcher** was configured to allow SAML `POST` requests to the `/saml_login` endpoint.
- The **Referrer Filter** and **CORS configuration** were updated to allow requests from the Microsoft Entra External ID login domain.
- An AEM group named **`entra-users`** was created and the appropriate permissions/CUG configuration was applied to the protected content.
- The SAML handler was configured to automatically create authenticated users and add them to the `entra-users` group.
- A custom [**SAML post-sync hook**](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/authentication/saml-2-0-login-hook) was implemented to run after successful authentication and user synchronization. The code for the [SAML post-sync hook can be downloaded from here.](assets/EntraSamlHook.zip).
- The post-sync hook extracts the **Entra Object ID, email address, first name, and last name** from the SAML assertion.
- The extracted customer profile is sent directly from AEM to **Adobe Experience Platform (AEP)** using the AEP Streaming Ingestion endpoint.

### com.adobe.granite.auth.saml.SamlAuthenticationHandler~entra.cfg.json

The following is my entra.cfg.json file for your reference

```
{
  "path": [ "/content/bankingapplication"],
  
  "idpCertAlias": "$[env:ENTRA_SAML_IDP_CERT_ALIAS;default=certAlias___1789123117072]",

  "idpIdentifier": "$[env:ENTRA_SAML_IDP_ID;default=https://bea27b92-5e14-4413-b807-fe4b295454a5.ciamlogin.com/bea27b92-5e14-4413-b807-fe4b295454a5/]",

  "idpUrl": "$[env:ENTRA_SAML_IDP_URL;default=https://aemformsportal.ciamlogin.com/bea27b92-5e14-4413-b807-fe4b295454a5/saml2]",

  "serviceProviderEntityId": "$[env:ENTRA_SAML_AEM_ID;default=https://publish-p133654-e1305513.adobeaemcloud.com]",

   "defaultRedirectUrl": "/content/bankingapplication/us/formsportal.html",

  "useEncryption": false,
  "userIDAttribute": "",

  

  "createUser": true,

  "userIntermediatePath": "entraformsportal/idp",

  "synchronizeAttributes": [
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname=profile/givenName",
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname=profile/familyName",
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress=profile/email",
    "objectId=profile/entraObjectId"
  ],

  "addGroupMemberships": true,

  "defaultGroups": [
    "entra-users"
  ]
}
```