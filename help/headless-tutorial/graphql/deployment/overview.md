


# AEM Headless deployments

AEM Headless client deployments take many forms; AEM-hosted SPA, external SPA or web site, mobile app, or even server-to-server process. 

Depending on the client and how it is deployed, AEM Headless deployments have different considerations. 

## AEM service architecture

Prior to exploring deployment considerations, it's imperative to understand AEM's logical architecture, and the separation and roles of AEM as a Cloud Service's service tiers. AEM as a Cloud Service is comprised of two logical services:

+ __AEM Author__ is the service where teams create, collaborate and publish Content Fragments (and other assets)
+ __AEM Publish__ is the service that where published Content Fragments (and other assets) are replicated for general consumption

AEM Headless clients operating in a production capacity typically interact with AEM Publish, which contains the approved,published content. Client interacting with AEM Author needs to take special consideration as AEM Author is secure by default, requiring authorization for all requests, as well as may contain incomplete, or un-approved content.

## Headless client deployments

+ [Single-page app](./spa.md)
+ [Web component/JS](./web-component.md)
+ [Mobile app](./mobile.md)
+ [Server to server](./server-to-server.md)

