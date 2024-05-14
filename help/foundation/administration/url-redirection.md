---
title: URL redirects
description: Learn about the various options to perform URL redirection in AEM.
version: 6.4, 6.5, Cloud Service
topic: Development, Administration
feature: Operations, Dispatcher
role: Developer, Architect
level: Intermediate
jira: KT-11466
last-substantial-update: 2022-10-14
index: y
doc-type: Article
exl-id: 8e64f251-e5fd-4add-880e-9d54f8e501a6
duration: 164
---
# URL redirects

URL redirection is a common aspect as part of website operation. Architects and administrators are challenged to find the best solution on how and where to manage the URL redirects that provide flexibility and fast redirect deployment time. 

Make sure you are familiar with the [AEM (6.x) aka AEM Classic](https://experienceleague.adobe.com/docs/experience-manager-learn/dispatcher-tutorial/chapter-2.html#the-%E2%80%9Clegacy%E2%80%9D-setup) and [AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/architecture.html#runtime-architecture) infrastructure. The key differences are:

1. AEM as a Cloud Service has [built-in CDN](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn.html), however, customers can provide a CDN (BYOCDN) in front of AEM-managed CDN.
1. AEM 6.x whether on-premise or Adobe Managed Services (AMS) does not include an AEM-managed CDN, and customers must bring their own.

The other AEM services (AEM Author/Publish, and Dispatcher) are otherwise conceptually similar between AEM 6.x and AEM as a Cloud Service.

AEM's URL redirect solutions are as follows:

|                                                   | Managed & deployed as AEM project code | Ability to change by marketing/content team  | AEM as Cloud Service compatible | Where redirection execution happens |
|---------------------------------------------------|:-----------------------:|:---------------------:|:---------------------:| :---------------------:|
| [At Edge via bring your own CDN](#at-edge-via-bring-your-own-cdn)                                   | &#10008;                | &#10008;             | &#10004;             | Edge/CDN |
| [Apache `mod_rewrite` rules as Dispatcher config ](#apache-mod_rewrite-module)  | &#10004;                | &#10008;             | &#10004;             | Dispatcher |
| [ACS Commons - Redirect Map Manager](#redirect-map-manager)                | &#10008;                | &#10004;             | &#10008;             |Dispatcher |
| [ACS Commons - Redirect Manager](#redirect-manager)                    | &#10008;                | &#10004;             | &#10004;              |AEM |
| [The `Redirect` page property](#the-redirect-page-property)                    | &#10008;                | &#10004;             | &#10004;              |AEM |


## Solution options

The following are solution options in the order of being closer to the website visitor's browser.

### At Edge via bring your own CDN

Some CDN services provide redirection solutions at the Edge level thus reducing round trips to the origin. See [Akamai Edge Redirector](https://techdocs.akamai.com/cloudlets/docs/what-edge-redirector), [AWS CloudFront Functions](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/cloudfront-functions.html). Please consult with your CDN service provider for Edge level redirection capability.

Managing redirects at Edge or CDN level has performance advantages, however they are not managed as part of AEM but rather discrete projects. A well-thought process to manage and deploy redirect rules is crucial to avoid problems.


### Apache `mod_rewrite` module

A common solution uses [Apache Module mod_rewrite](https://httpd.apache.org/docs/current/mod/mod_rewrite.html). The [AEM Project Archetype](https://github.com/adobe/aem-project-archetype) provides a Dispatcher project structure for both [AEM 6.x](https://github.com/adobe/aem-project-archetype/tree/develop/src/main/archetype/dispatcher.ams#file-structure) and [AEM as a Cloud Service](https://github.com/adobe/aem-project-archetype/tree/develop/src/main/archetype/dispatcher.cloud#file-structure) project. The default (immutable) and custom rewrite rules are defined in the `conf.d/rewrites` folder and the rewrite engine is turned ON for `virtualhosts` that listens on port `80` via `conf.d/dispatcher_vhost.conf` file. An example implementation is available in the [AEM WKND Sites Project](https://github.com/adobe/aem-guides-wknd/tree/main/dispatcher/src/conf.d/rewrites).

In AEM as a Cloud Service, these redirect rules are managed as part of AEM code and deployed via Cloud Manager [Web Tier config pipeline](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/cicd-pipelines/introduction-ci-cd-pipelines.html#web-tier-config-pipelines) or [Full-stack pipeline](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/cicd-pipelines/introduction-ci-cd-pipelines.html#full-stack-pipeline). Thus your AEM project-specific process is at play to manage, deploy, and trace the redirect rules.

Most CDN services do cache the HTTP 301 and 302 redirects depending on their `Cache-Control` or `Expires` headers. This helps to avoid the round trip after the initial redirect originating at Apache/Dispatcher.


### ACS AEM Commons

There are two features available within [ACS AEM Commons](https://adobe-consulting-services.github.io/acs-aem-commons/) to manage URL redirects. Please note, ACS AEM Commons is a community-operated, open-source project and not supported by Adobe.

#### Redirect Map Manager

[Redirect Map Manager](https://adobe-consulting-services.github.io/acs-aem-commons/features/redirect-map-manager/index.html) allows AEM 6.x administrators to easily maintain and publish [Apache RewriteMap](https://httpd.apache.org/docs/2.4/rewrite/rewritemap.html) files without directly accessing Apache Web server or requiring an Apache web server restart. This feature allows permissions users  to create, update, and delete redirect rules from a console in AEM, without the help of the development team or an AEM deployment. Redirect Map Manager is **NOT AEM as a Cloud Service compatible**.  

#### Redirect Manager

[Redirect Manager](https://adobe-consulting-services.github.io/acs-aem-commons/features/redirect-manager/index.html) allows the users in AEM to easily maintain and publish redirects from AEM. The implementation is based on Java&trade; servlet filter, thus typical JVM resource consumption. This feature also eliminates the dependency on the AEM development team and the AEM deployments. Redirect Manager is both **AEM as a Cloud Service** and **AEM 6.x** compatible. While the initial redirected request must hit AEM Publish service to generate the 301/302 (most) CDNs' cache 301/302 by default, allowing subsequent requests to be redirected at the edge/CDN.

### The `Redirect` page property

The out-of-the-box (OOTB) `Redirect` page property from the [Advanced tab](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/authoring/fundamentals/page-properties.html#advanced) allows content authors to define the redirect location for the current page. This solution is best for per-page redirect scenarios and does not have a central location to view and manage the page redirects.

## Which solution is right for implementation

Below are a few criteria to determine the right solution. Also, your organization's IT and Marketing process should help to pick the right solution.

1. Enabling the marketing team or super users to manage redirect rules without the AEM development team and the AEM deployments.
1. The Process to manage, verify, track, and revert the changes or risk mitigation.
1. Availability of _Subject Matter Expertise_ for **At Edge via CDN Service** solution.
