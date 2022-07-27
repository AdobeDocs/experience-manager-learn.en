---
title: AEM Headless mobile deployments
description:
version: Cloud Service
feature: GraphQL API
topic: Headless, Content Management
role: Developer, Architect
level: Intermediate
kt: 
thumbnail: KT-.jpg
mini-toc-levels: 2
---

# AEM Headless mobile deployments

AEM Headless mobile deployments are native mobile apps for iOS, Android, etc. that consume and interact with content in AEM in a headless manner.

Mobile deployments require minimal configuration, as HTTP connections to AEM Headless APIs are not initiated in the context of a browser.

## Deployment configurations

| Mobile app connects to | AEM Author | AEM Publish | AEM Preview |
|-----------------------:|:----------:|:-----------:|:-----------:|
| [Dispatcher filters](./dispatcher-fitlers.md)     | &#10008;   | &#10004;    | &#10004;    |
| [CORS configuration](./cors.md)     | &#10008;   | &#10008;    | &#10008;    |  
| Image URL hostname     | &#10004;   | &#10004;    | &#10004;    |  

## Example mobile apps

Adobe provides example iOS and Android mobile apps.


