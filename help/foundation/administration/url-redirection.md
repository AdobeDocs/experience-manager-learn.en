---
title: URL redirects
description: Learn about the various options to perform URL redirection in AEM.
version: Experience Manager 6.4, Experience Manager 6.5, Experience Manager as a Cloud Service
topic: Development, Administration
feature: Operations, Dispatcher
role: Developer, Architect
level: Intermediate
jira: KT-11466
last-substantial-update: 2024-10-22
index: y
doc-type: Article
exl-id: 8e64f251-e5fd-4add-880e-9d54f8e501a6
duration: 164
---
# URL redirects

URL redirection is a common aspect as part of website operation. Architects and administrators are challenged to find the best solution on how and where to manage the URL redirects that provide flexibility and fast redirect deployment time. 

Make sure you are familiar with the [AEM (6.x) aka AEM Classic](https://experienceleague.adobe.com/en/docs/experience-manager-learn/dispatcher-tutorial/chapter-2) and [AEM as a Cloud Service](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/overview/architecture) infrastructure. The key differences are:

1. AEM as a Cloud Service has [built-in CDN](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn), however, customers can provide a CDN (BYOCDN) in front of AEM-managed CDN.
1. AEM 6.x whether on-premise or Adobe Managed Services (AMS) does not include an AEM-managed CDN, and customers must bring their own.

The other AEM services (AEM Author/Publish, and Dispatcher) are otherwise conceptually similar between AEM 6.x and AEM as a Cloud Service.

AEM's URL redirect solutions are as follows:

|                                                   | Managed & deployed as AEM project code | Ability to change by marketing/content team  | AEM as Cloud Service compatible | Where redirection execution happens |
|---------------------------------------------------|:-----------------------:|:---------------------:|:---------------------:| :---------------------:|
| [At Edge via AEM-managed CDN](#at-edge-via-aem-managed-cdn)                                   | &#10004;                | &#10008;             | &#10004;             | Edge/CDN (Built-in) |
| [At Edge via bring your own CDN (BYOCDN)](#at-edge-via-bring-your-own-cdn)                                   | &#10008;                | &#10008;             | &#10004;             | Edge/CDN (BYOCDN) |
| [Apache `mod_rewrite` rules as Dispatcher config ](#apache-mod_rewrite-module)  | &#10004;                | &#10008;             | &#10004;             | Dispatcher |
| [ACS Commons - Redirect Map Manager](#redirect-map-manager)                | &#10008;                | &#10004;             | &#10004;             | Dispatcher |
| [ACS Commons - Redirect Manager](#redirect-manager)                    | &#10008;                | &#10004;             | &#10004;              | AEM / Dispatcher |
| [The `Redirect` page property](#the-redirect-page-property)                    | &#10008;                | &#10004;             | &#10004;              | AEM |


## Solution options

The following are solution options in the order of being closer to the website visitor's browser.

### At Edge via AEM-managed CDN {#at-edge-via-aem-managed-cdn}

This option is only available for AEM as a Cloud Service customers. 

The [AEM-managed CDN](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn) provides a redirection solution at the Edge level thus reducing round trips to the origin. The [Server-side Redirects](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn-configuring-traffic#server-side-redirectors) feature allows you to configure the redirect rules in the AEM project code and deploy using the [Config Pipeline](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/security/traffic-filter-and-waf-rules/how-to-setup#deploy-rules-through-cloud-manager). The CDN configuration file (`cdn.yaml`) size should not exceed 100KB.

Managing redirects at Edge or CDN level has performance advantages.

### At Edge via bring your own CDN

Some CDN services provide redirection solutions at the Edge level, thus reducing round trips to the origin. See [Akamai Edge Redirector](https://techdocs.akamai.com/cloudlets/docs/what-edge-redirector), [AWS CloudFront Functions](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/cloudfront-functions.html). Please consult with your CDN service provider for Edge level redirection capability.

Managing redirects at Edge or CDN level has performance advantages, however they are not managed as part of AEM but rather discrete projects. A well defined process to manage and deploy redirect rules is crucial to avoid problems.


### Apache `mod_rewrite` module

A common solution uses [Apache Module mod_rewrite](https://httpd.apache.org/docs/current/mod/mod_rewrite.html). The [AEM Project Archetype](https://github.com/adobe/aem-project-archetype) provides a Dispatcher project structure for both [AEM 6.x](https://github.com/adobe/aem-project-archetype/tree/develop/src/main/archetype/dispatcher.ams#file-structure) and [AEM as a Cloud Service](https://github.com/adobe/aem-project-archetype/tree/develop/src/main/archetype/dispatcher.cloud#file-structure) project. The default (immutable) and custom rewrite rules are defined in the `conf.d/rewrites` folder and the rewrite engine is turned ON for `virtualhosts` that listens on port `80` via `conf.d/dispatcher_vhost.conf` file. An example implementation is available in the [AEM WKND Sites Project](https://github.com/adobe/aem-guides-wknd/tree/main/dispatcher/src/conf.d/rewrites).

In AEM as a Cloud Service, these redirect rules are managed as part of AEM code and deployed via the Cloud Manager [Web Tier config pipeline](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/cicd-pipelines/introduction-ci-cd-pipelines) or [Full-stack pipeline](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/cicd-pipelines/introduction-ci-cd-pipelines). Thus, your AEM project-specific process is at play to manage, deploy, and trace the redirect rules.

Most CDN services do cache the HTTP 301 and 302 redirects depending on their `Cache-Control` or `Expires` headers. It helps to avoid the round trip after the initial redirect originating at Apache/Dispatcher.


### ACS AEM Commons

There are two features available within [ACS AEM Commons](https://adobe-consulting-services.github.io/acs-aem-commons/) to manage URL redirects. Please note, ACS AEM Commons is a community-operated, open-source project and not supported by Adobe.

#### Redirect Map Manager

[Redirect Map Manager](https://adobe-consulting-services.github.io/acs-aem-commons/features/redirect-map-manager/index.html) helps AEM administrators to easily maintain and publish [Apache RewriteMap](https://httpd.apache.org/docs/2.4/rewrite/rewritemap.html) files without directly accessing the Apache Web server or requiring an Apache Web server restart. This feature allows permissions users to create, update, and delete redirect rules from a console in AEM, without the help of the development team or an AEM deployment. Redirect Map Manager is both **AEM as a Cloud Service** (see [Pipeline-free URL Redirects](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/content-delivery/pipeline-free-url-redirects) strategy and related [tutorial](https://experienceleague.adobe.com/en/docs/experience-manager-learn/foundation/administration/implementing-pipeline-free-url-redirects#acs-commons---redirect-map-manager)) and **AEM 6.x** compatible.

#### Redirect Manager

[Redirect Manager](https://adobe-consulting-services.github.io/acs-aem-commons/features/redirect-manager/index.html) allows the users in AEM to easily maintain and publish redirects from AEM. The implementation is based on Java&trade; servlet filter, thus typical JVM resource consumption. This feature also eliminates the dependency on the AEM development team and the AEM deployments. Redirect Manager is both **AEM as a Cloud Service** and **AEM 6.x** compatible. While the initial redirected request must hit the AEM Publish service to generate the 301/302 (most) CDNs' cache 301/302 by default, allowing subsequent requests to be redirected at the edge/CDN.

[Redirect Manager](https://adobe-consulting-services.github.io/acs-aem-commons/features/redirect-manager/index.html) also supports [Pipeline-free URL Redirects](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/content-delivery/pipeline-free-url-redirects) strategy for **AEM as a Cloud Service** by [compiling redirects into a text file](https://adobe-consulting-services.github.io/acs-aem-commons/features/redirect-manager/subpages/rewritemap.html) for [Apache RewriteMap](https://httpd.apache.org/docs/2.4/rewrite/rewritemap.html), so it allows for updating redirects used in Apache Web server without directly accessing it or requiring its restart. Refer to the [tutorial](https://experienceleague.adobe.com/en/docs/experience-manager-learn/foundation/administration/implementing-pipeline-free-url-redirects#acs-commons---redirect-manager) for more details. In this scenario the initial redirect request hits Apache Web server, and not AEM Publish service.

### The `Redirect` page property

The out-of-the-box (OOTB) `Redirect` page property from the [Advanced tab](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/authoring/sites-console/page-properties.html) allows content authors to define the redirect location for the current page. This solution is best for per-page redirect scenarios and does not have a central location to view and manage the page redirects.

## Which solution is right for implementation

Below are a few criteria to determine the right solution. Also, your organization's IT and Marketing process should help to pick the right solution.

1. Enabling the marketing team or super users to manage redirect rules without the AEM development team and the AEM deployments.
1. The Process to manage, verify, track, and revert the changes or risk mitigation.
1. Availability of _Subject Matter Expertise_ for **At Edge via CDN Service** solution.
