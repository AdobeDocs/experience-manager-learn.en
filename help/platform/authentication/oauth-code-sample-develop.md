---
title: Developing OAuth Scopes in AEM
seo-title: Developing OAuth Scopes in AEM
description: Adobe Experience Manager's extensible OAuth Scopes allow for access control for resources from a client application that is authorized by an end user. The diagram below illustrates the request flow in the context of AEM.
seo-description: Adobe Experience Manager's extensible OAuth Scopes allow for access control for resources from a client application that is authorized by an end user. The diagram below illustrates the request flow in the context of AEM.
uuid: 64b9c3c9-b8e0-46d7-a510-601b69719910
products: SG_EXPERIENCEMANAGER/6.3
topic-tags: developing
products: SG_EXPERIENCEMANAGER/6.4
topic-tags: Security
discoiquuid: 61232735-3423-4cb5-ba97-46d019cb9332
targetaudience: target-audience advanced
index: y
internal: n
snippet: y
---

# Developing OAuth Scopes in AEM{#developing-oauth-scopes-in-aem}

Adobe Experience Manager's extensible OAuth Scopes allow for access control for resources from a client application that is authorized by an end user. The diagram below illustrates the request flow in the context of AEM.

 [ ![](assets/aem-oauth-scopes-request-flow.png)

Click to download

](oauth-code-sample-develop/_jcr_content/main-pars/image.img.png/Screens%20-%20Example%20Solution%20Arch.png) AEM's provides 3 scopes OOTB

* Profile
* Offline access
* Replicate

AEM's extensible OAuth scopes allow other custom scopes to be defined. For example, a custom scope can be developed and deployed to AEM that allows a mobile app authorized via OAuth to be restricted to reading, but not writing assets.

OAuth is the preferred method of authorizing a client application since it uses an access token instead of requiring an AEM user's credentials to be provided to that application.

## View the code {#view-the-code}

[ ](https://github.com/Adobe-Consulting-Services/acs-aem-samples/blob/master/bundle/src/main/java/com/adobe/acs/samples/authentication/oauth/impl/SampleScopeWithPrivileges.java) 

## Supporting materials {#supporting-materials}

* [Download diagram in hi-res](oauth-code-sample-develop/_jcr_content/main-pars/image.img.png/Screens%20-%20Example%20Solution%20Arch.png)

