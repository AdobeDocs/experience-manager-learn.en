---
title: Understand Reasons to Upgrade
seo-title: Understand Reasons to Upgrade AEM
description: A high-level breakdown of key features for customers considering upgrading to the latest version of Adobe Experience Manager.
seo-description: A high-level breakdown of key features for customers considering upgrading to the latest version of Adobe Experience Manager.
uuid: fc08e630-e9ab-4d32-811d-14e6c437cde3
products: SG_EXPERIENCEMANAGER/6.4
discoiquuid: 78610491-568f-4f4b-bbae-1d6acbf81591
index: y
internal: n
snippet: y
---

# Understanding Reasons to Upgrade

A high-level breakdown of key features for customers considering upgrading to the latest version of Adobe Experience Manager.

## Key Features for Upgrading to AEM 6.5

* [Adobe Experience Manager 6.5 Release Notes](https://helpx.adobe.com/experience-manager/6-5/release-notes.html)

### Foundation improvements {#foundation-improvements}

Adobe Experience Manager 6.5 continues to enhance the system's stability, performance and supportability via: 

* **Java 11** support (while maintaining Java 8 support).

### Website creation and management {#website-creation-and-management}

AEM Sites introduces a number of features designed to accelerate the creation and build-out of websites:

* **SPA Editor** support allows SPA (single-page applications) to be completely authored in AEM, supporting a rich, Marketer-friendly authoring experience.
* **JavaScript SDK's**, a SPA Project Start Kit and supporting build tools, allow front-end developers to develop SPA Editor-compatible single page-applications independently of AEM.
* **Core Components** adds a multitude of new components, a **Component Library** as well as a variety of enhancements to existing Core Components.
* Further **Translations** enhancements streamline translation of AEM Sites.

### Fluid experiences {#fluid-experiences}

AEM continues to embrace Fluid Experiences with new and improved tooling that facilitates the use of content outside of AEM.

* **Content Fragments** suppport Version Comparison/Diff and Annotations.
* **AEM's Assets HTTP API** supports exposing **Content Fragments** directly in the DAM as **JSON**.
**Experience Fragments** support **Fulltext Search** and **AEM Dispatcher Cache Invalidation** for referencing **Pages**.

### Asset management {#asset-management}

AEM Assets continues building on its rich set of Asset management capabilities to improve using, managing and understanding the DAM. AEM 6.5 continues to improve the integration between Adobe Creative Cloud and creative workflows.

* **Adobe Asset Link** connects creatives directly to AEM Assets from Adobe Creative Cloud tools.
* **Adobe Stock** integration allows direct access to Adobe Stock imagery directly from the AEM Assets experience, creating a seamless content discovery experience.
* **AEM Desktop App** releases version 2.0 and re-envisioning itself while improving performance and stability.
* **Connected Assets** supports discrete AEM Sites instances to seamlessly access and use assets from a different AEM Assets instance.
* Updated video support in **Dynamic Media**, including **360 Video** and **Custom Video Thumbnails**.

### Content intelligence {#content-intelligence}

AEM continues to build its integration with smart technologies, leveraging machine learning and artificial intelligence to improve all experiences.

* **Adobe Asset Link** adds **Visual Similarity Search**, allowing for similar images to be easily discovered and used within **Adobe Creative Cloud tools**.

### Integrations {#integrations}

AEM grows its ability to integrate with other Adobe services:

* **Experience Fragments** deepens their integration with **Adobe Target** by supporting **Export as JSON** to Adobe Target and the ability to **delete Experience Fragment-based offers** from **Adobe Target**.

### AMS Cloud Manager {#ams-cloud-manager}

[Cloud Manager](https://adobe.ly/2HODmsv), an exclusive to Adobe Managed Services (AMS) customers, offers the following features:

* Cloud Manager supports extends AEM deployment support from AEM Sites to **AEM Assets**, including **automated performance testing of asset processing**.
* **Auto-scaling** of the AEM Publish tier at pre-defined thresholds, ensure an optimal end-user experience.
* **Non-production pipelines** allow development teams to leverage Cloud Manager to continuously check code-quality and deploy to lower environments (Development and QA).
* **CI/CD Pipeline APIs** allow customers to programmatically engage with Cloud Manager, deepening integration possibilities with on-premise development infrastructure.


## Foundation Features {#foundation-matrix}

Below is a matrix of key foundation features offered by AEM. Some of these features were introduced in earlier versions incremental enhancements added in each release.

* [AEM Foundation release notes](https://helpx.adobe.com/experience-manager/6-5/release-notes/wcm-platform.html)

***X denotes that significant enhancements to the feature in this version.***

***X<sup>+</sup> denotes the feature is available via a Service Pack or Feature Pack.***

<table>
<tbody><tr><td>Foundation Feature</td>
<td>5.6.x</td>
<td>6.0</td>
<td>6.1</td>
<td>6.2</td>
<td>6.3</td>
<td>6.4</td>
<td>6.5</td>
</tr><tr><td><strong>Java 11 Support<br>
 </strong>AEM supports Java 11 (as well as Java 8).<br>
</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>X</td>
</tr><tr><td><a href="https://jackrabbit.apache.org/oak/docs/index.html" target="_blank">Oak Content Repository</a><strong><br>
Provides far greater performance and scalability then predecessor Jackrabbit 2.</td>
<td>&nbsp;</td>
<td>X</td>
<td>X</td>
<td>X</td>
<td>X</td>
<td>X</td>
<td>X<sup>+</sup></td>
</tr><tr><td><strong><a href="https://helpx.adobe.com/experience-manager/6-5/sites/deploying/using/indexing-via-the-oak-run-jar.html">oak-run.jar Index Support</a></strong><br>
 </strong>Improved re/indexing, statistics collection, and consistency checking of Oak indexes.</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>X</td>
<td>X<sup>+</sup></td>
</tr><tr><td><strong><a href="https://helpx.adobe.com/experience-manager/6-5/sites/deploying/using/queries-and-indexing.html" target="_blank">Custom Search Indexes</a></strong><br>
Ability to add custom index definitions to optimize query performance and search relevancy.</td>
<td>&nbsp;</td>
<td>X</td>
<td>X</td>
<td>X</td>
<td>X</td>
<td>X</td>
<td>X<sup>+</sup></td>
</tr><tr><td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/deploying/using/revision-cleanup.html" target="_blank">Online Revision Cleanup</a></strong><br>
Perform repository maintenance without server downtime.</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>X</td>
<td>X<sup>+</sup></td>
<td>X</td>
</tr><tr><td><strong><a href="https://helpx.adobe.com/experience-manager/6-5/sites/deploying/using/storage-elements-in-aem-6.html" target="_blank">TarMK or MongoMK repository storage</a></strong><br>
Options to use simple, performant file-based storage of TarMK (next-generation version of TarPM)<br>
or scale horizontally with a MongoDB backed repository with MongoMK.</td>
<td>&nbsp;</td>
<td>X</td>
<td>X</td>
<td>X</td>
<td>X</td>
<td>X</td>
<td>X</td>
</tr><tr><td><strong><a href="https://helpx.adobe.com/experience-manager/6-5/sites/deploying/using/aem-with-mongodb.html" target="_blank">MongoMK performance and stability</a><br>
 </strong>Continued enhancements have been made to MongoMK since it's introduction with AEM 6.0.</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>X</td>
<td>X</td>
<td>X</td>
<td>X</td>
<td>X</td>
</tr><tr><td><strong><a href="https://helpx.adobe.com/experience-manager/6-5/sites/deploying/using/data-store-config.html#AmazonS3DataStore">Amazon S3 DataStore</a></strong><br>
Leverage expandable cloud storage solution to store binary assets.</td>
<td>X</td>
<td>X<sup>+</sup></td>
<td>X</td>
<td>X</td>
<td>X</td>
<td>X</td>
<td>X</td>
</tr><tr><td><strong>Touch UI Feature Parity</strong><br>
Continued enhancements to authoring UI for speed with increased productivity and feature parity with Classic UI.</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>X</td>
<td>X</td>
<td>X</td>
<td>X</td>
</tr><tr><td><strong>Omnisearch</strong><br>
Quickly search and navigate AEM.</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>X</td>
<td>X</td>
<td>X</td>
<td>X</td>
</tr><tr><td><strong><a href="https://helpx.adobe.com/experience-manager/6-5/sites/administering/using/operations-dashboard.html" target="_blank">Operations Dashboard</a><br>
 </strong>Perform maintenance, monitor server health and analyze performance from within AEM.</td>
<td></td>
<td>X</td>
<td>X</td>
<td>X</td>
<td>X</td>
<td>X<sup>+</sup></td>
<td>X</td>
</tr><tr><td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/deploying/using/upgrade.html" target="_blank" >Upgrade Improvements</a><br>
Upgrade improvements allow easier and quicker in-place upgrades of AEM.&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>X</td>
<td>X</td>
</tr><tr><td><strong><a href="https://helpx.adobe.com/experience-manager/htl/using/overview.html" target="_blank">HTL Template Language</a><br>
 </strong>A modern templating engine that separates presentation from logic. Significantly reduces component development time. Incremental features added with each release.</td>
<td>&nbsp;</td>
<td>X</td>
<td>X</td>
<td>X</td>
<td>X</td>
<td>X</td>
<td>X</td>
</tr><tr><td><strong><a href="https://sling.apache.org/documentation/bundles/models.html" target="_blank">Sling Models</a><br>
 </strong>A flexible framework for modeling JCR resources into business objects and logic. Incremental features added with each release.<br>
</td>
<td>&nbsp;</td>
<td>X</td>
<td>X</td>
<td>X</td>
<td>X</td>
<td>X<sup>+</sup></td>
<td>X</td>
</tr><tr><td><strong><a href="https://adobe.ly/2HODmsv" target="_blank">Cloud Manager</a></strong><br>
Exclusive to Adobe Managed Services (AMS) customers, Cloud Manager accelerates development and deployment via a state of the art CI/CD pipeline.</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>X</td>
<td>X<sup>+</sup></td>
</tr></tbody></table>

## Security Features {#security-matrix}

Below is a matrix of key security features offered by AEM. Some of these features were introduced in earlier versions incremental enhancements added in each release.

* [Security release notes](https://helpx.adobe.com/experience-manager/6-5/release-notes/wcm-platform.html#Security)

***X denotes that significant enhancements to the feature in this version.***

***X<sup>+</sup> denotes the feature is available via a Service Pack or Feature Pack.***

<table>
<tbody><tr><td><strong>Security Feature<br>
 </strong>&nbsp;</td>
<td>5.6.x<br>
</td>
<td>6.0</td>
<td>6.1</td>
<td>6.2</td>
<td>6.3</td>
<td>6.4</td>
<td>6.5</td>
</tr><tr><td><strong><a href="https://helpx.adobe.com/experience-manager/6-5/sites/administering/using/security-service-users.html" target="_blank">Service Users</a></strong><br>
Compartmentalizes permissions avoid unnecessary use of Admin privileges.</td>
<td></td>
<td>X</td>
<td>X</td>
<td>X</td>
<td>X</td>
<td>X</td>
<td>X</td>
</tr><tr><td><strong><a href="https://helpx.adobe.com/experience-manager/6-5/sites/administering/using/saml-2-0-authenticationhandler.html" target="_blank">Key Store Management</a></strong><br>
Global trust store, certificates, and keys all managed within the repository.</td>
<td></td>
<td>X</td>
<td>X</td>
<td>X</td>
<td>X</td>
<td>X</td>
<td>X</td>
</tr><tr><td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/csrf-protection.html" target="_blank"><strong>CSRF</strong>&nbsp;<strong>protection</strong></a><br>
Cross-Site Request Forgery protection out of the box.</td>
<td></td>
<td></td>
<td>X</td>
<td>X</td>
<td>X</td>
<td>X</td>
<td>X</td>
</tr><tr><td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/administering/using/saml-2-0-authenticationhandler.html" target="_blank"><strong>CORS</strong>&nbsp;<strong>support</strong></a><br>
Cross-Origin Resource Sharing support for greater application flexibility.</td>
<td></td>
<td></td>
<td></td>
<td></td>
<td>X</td>
<td>X</td>
<td>X</td>
</tr><tr><td><strong><a href="https://docs.adobe.com/docs/en/aem/6-5/administer/security/saml-2-0-authenticationhandler.html" target="_blank">Improved SAML authentication support</a><br>
 </strong>Improved SAML redirect, optimized group info, and key encryption issues resolved.<br>
</td>
<td></td>
<td></td>
<td>X</td>
<td>X</td>
<td>X</td>
<td>X</td>
<td>X</td>
</tr><tr><td><strong><a href="https://helpx.adobe.com/experience-manager/6-5/sites/administering/using/ldap-config.html" target="_blank">LDAP as an OSGi Configuration</a><br>
 </strong>Simplifies management and updates of LDAP authentication.</td>
<td></td>
<td>X</td>
<td>X</td>
<td>X</td>
<td>X</td>
<td>X</td>
<td>X</td>
</tr><tr><td><strong>OSGi Encryption support for plain-text passwords<br>
 </strong>Passwords and other sensitive values can be saved in encrypted form and automatically decrypted.</td>
<td></td>
<td></td>
<td></td>
<td></td>
<td>X</td>
<td>X</td>
<td>X</td>
</tr><tr><td><strong><a href="https://helpx.adobe.com/experience-manager/6-5/sites/administering/using/user-group-ac-admin.html" target="_blank">CUG enhancements</a><br>
 </strong>Closed-User Group implementation has been re-written to address performance and scalability issues.</td>
<td></td>
<td></td>
<td></td>
<td></td>
<td>X</td>
<td>X<sup>+</sup></td>
<td>X</td>
</tr><tr><td><strong><a href="https://helpx.adobe.com/experience-manager/kt/platform-repository/using/ssl-wizard-technical-video-use.html" target="_blank">SSL Wizard</a></strong><br>
UI to simplify setup and management of SSL.</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>X</td>
<td>X</td>
<td>X</td>
</tr><tr><td><strong><a href="https://helpx.adobe.com/experience-manager/6-5/sites/administering/using/encapsulated-token.html" target="_blank">Encapsulated Token Support</a></strong><br>
No longer necessary for "sticky" sessions to support horizontal authentication across publish instances.</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>X</td>
<td>X</td>
<td>X</td>
<td>X</td>
<td>X</td>
</tr><tr><td><strong><a href="https://helpx.adobe.com/experience-manager/6-5/sites/administering/using/ims-config-and-admin-console.html" target="_blank">Adobe IMS Authentication Support</a><br>
 </strong>Exclusive to Adobe Managed Services (AMS), centrally manage access to AEM Author instances via Adobe IMS (Identity Management System).</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>X</td>
<td>X</td>
</tr></tbody></table>

## Sites Features {#sites-matrix}

Below is a matrix of key Sites features offered by AEM. Some of these features were introduced in earlier versions incremental enhancements added in each release.

* [AEM Sites release notes](https://helpx.adobe.com/experience-manager/6-5/release-notes/sites.html)

***X denotes that significant enhancements to the feature in this version.***

***X<sup>+</sup> denotes the feature is available via a Service Pack or Feature Pack.***

<table>
<tbody><tr><td><strong>Sites Feature<br>
 </strong>&nbsp;</td>
<td>5.6.x<br>
</td>
<td>6.0</td>
<td>6.1</td>
<td>6.2</td>
<td>6.3</td>
<td>6.4</td>
<td>6.5</td>
</tr><tr><td><strong><a href="http://helpx.adobe.com/experience-manager/kt/sites/using/page-editor-feature-video-use.html" target="_blank">Touch Optimized Page Authoring</a></strong><br>
Allows editors to leverage tablets and computers with touch screens.</td>
<td></td>
<td>X</td>
<td>X<sup>+</sup></td>
<td>X</td>
<td>X</td>
<td>X</td>
<td>X</td>
</tr><tr><td><strong><a href="http://helpx.adobe.com/experience-manager/6-5/sites/authoring/using/responsive-layout.html" target="_blank">Responsive Site Authoring</a></strong><br>
The layout&nbsp;mode allows editors to resize components based on device widths for responsive sites.</td>
<td></td>
<td></td>
<td>X<sup>&nbsp;</sup><br>
</td>
<td>X<sup>&nbsp;</sup><br>
</td>
<td>X<sup>+</sup></td>
<td>X</td>
<td>X</td>
</tr><tr><td><strong><a href="http://helpx.adobe.com/experience-manager/kt/sites/using/template-editor-feature-video-use.html" target="_blank">Editable Templates</a></strong><br>
Allow specialized authors to create and edit page templates.</td>
<td></td>
<td></td>
<td></td>
<td>X</td>
<td>X<sup>+</sup></td>
<td>X</td>
<td>X</td>
</tr><tr><td><strong><a href="http://helpx.adobe.com/experience-manager/core-components/user-guide.html" target="_blank">Core Components</a></strong><br>
Accelerate site development. Available on GitHub for frequent release schedule and flexibility.</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>X</td>
<td>X<sup>+</sup></td>
<td>X<sup>+</sup></td>
</tr><tr><td><strong><a href="http://helpx.adobe.com/experience-manager/6-5/sites/developing/using/spa-overview.html" target="_blank">SPA Editor</a><br>
 </strong>Create authorable, enaging web experiences using Single-Page Application (SPA) frameworks built on React or Angular.</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>X<sup>+</sup></td>
<td>X<sup>+</sup></td>
<td>X<sup>+</sup></td>
</tr><tr><td><strong><a href="http://helpx.adobe.com/experience-manager/6-5/release-notes/style-system-fp.html" target="_blank">Style System<br>
</a> </strong>Increase AEM component re-use by defining their visual appearance using the in-context style system.&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>X<sup>FP</sup></td>
<td>X</td>
<td>X</td>
</tr><tr><td><strong><a href="http://helpx.adobe.com/experience-manager/6-5/sites/administering/using/msm.html" target="_blank">Multi-Site Manager (MSM)</a><br>
 </strong>Manage multiple websites that share common content (i.e multi-lingual, multiple brands).</td>
<td>X</td>
<td>X</td>
<td>X</td>
<td>X<sup>+</sup></td>
<td>X</td>
<td>X</td>
<td>X</td>
</tr><tr><td><strong><a href="http://helpx.adobe.com/experience-manager/6-5/sites/administering/using/translation.html" target="_blank">Content Translation</a></strong><br>
Plug and play framework integrates with industry leading 3rd party translation services.</td>
<td></td>
<td></td>
<td>X</td>
<td>X<sup>+</sup></td>
<td>X</td>
<td>X<sup>+</sup></td>
<td>X<sup>+</sup></td>
</tr><tr><td><strong><a href="http://helpx.adobe.com/experience-manager/6-5/sites/developing/using/contexthub.html" target="_blank">ContextHub</a><br>
 </strong>Next generation client context framework for personalization of content.</td>
<td></td>
<td>X</td>
<td>X<sup>+</sup></td>
<td>X</td>
<td>X</td>
<td>X</td>
<td>X</td>
</tr><tr><td><strong><a href="http://helpx.adobe.com/experience-manager/6-5/sites/authoring/using/launches.html" target="_blank">Launches</a><br>
 </strong>Develop content for a future release without disrupting day-to-day authoring.</td>
<td>X</td>
<td>X</td>
<td>X</td>
<td>X<sup>+</sup></td>
<td>X<sub></sub></td>
<td>X<sub></sub></td>
<td>X</td>
</tr><tr><td><strong><a href="http://helpx.adobe.com/experience-manager/kt/sites/using/content-fragments-feature-video-understand.html" target="_blank">Content Fragments</a></strong><br>
Create and curate editorial content de-coupled from the presentation for easy reuse.</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>X</td>
<td>X<sup>+</sup></td>
<td>X<sup>+</sup></td>
<td>X<sup>+</sup></td>
</tr><tr><td><strong><a href="http://helpx.adobe.com/experience-manager/kt/sites/using/experience-fragments-feature-video-use.html" target="_blank">Experience Fragments</a></strong><br>
Create reusable experiences and variations optimized for desktop, mobile, and social channels.</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>X</td>
<td>X<sup>+</sup></td>
<td>X<sup>+</sup></td>
</tr><tr><td><strong><a href="http://helpx.adobe.com/experience-manager/6-5/release-notes/content-services-fragments-featurepack.html" target="_blank">Content Services</a><br>
 </strong>Export content from AEM as JSON for consumption across devices and applications.</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>X<sup>FP</sup></td>
<td>X</td>
<td>X</td>
</tr><tr><td><strong>Adobe Analytics Integration and Content Insights</strong><br>
Easy integration of Adobe Analytics and DTM. Display performance info within Author environment.</td>
<td>&nbsp;</td>
<td>X</td>
<td>X</td>
<td>X</td>
<td>X<sup>+</sup></td>
<td>X</td>
<td>X</td>
</tr><tr><td><strong><a href="http://helpx.adobe.com/experience-manager/6-5/sites/authoring/using/content-targeting-touch.html" target="_blank">Adobe Target Integration</a></strong><br>
Step-by-step wizard to create targeted experiences, create reusable offer libraries.</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>X</td>
<td>X<sup>+</sup></td>
<td>X</td>
<td>X</td>
<td>X</td>
</tr><tr><td><strong><a href="http://helpx.adobe.com/experience-manager/6-5/sites/administering/using/campaign.html" target="_blank">Adobe Campaign Integration</a></strong><br>
Easy integration with next-generation email campaign solution.</td>
<td>&nbsp;</td>
<td>X</td>
<td>X</td>
<td>X</td>
<td>X</td>
<td>X</td>
<td>X</td>
</tr><tr><td><strong><a href="http://helpx.adobe.com/experience-manager/using/aem_launch_adobeio_integration.html" target="_blank">Adobe Launch Integration</a></strong><br>
Integrate with Adobe's next-generation tag management cloud service.</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>X</td>
<td>X</td>
</tr><tr><td><strong><a href="http://helpx.adobe.com/experience-manager/6-5/sites/deploying/using/aem-screens-introduction.html" target="_blank">Screens</a></strong><br>
Manage experiences for digital signage and kiosks.</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>X</td>
<td>X</td>
<td>X<sup>+</sup></td>
<td>X<sup>+</sup></td>
</tr><tr><td><strong><a href="http://helpx.adobe.com/experience-manager/6-5/sites/administering/using/ecommerce.html" target="_blank">eCommerce</a></strong><br>
Deliver branded, personalized shopping experiences across web, mobile, and social touchpoints<br>
</td>
<td>X</td>
<td>X</td>
<td>X</td>
<td>X</td>
<td>X</td>
<td>X<sup>+</sup></td>
<td>X<sup>+</sup></td>
</tr><tr><td><strong><a href="http://helpx.adobe.com/experience-manager/6-5/communities/using/overview.html" target="_blank">Communities</a></strong><br>
Forums, threaded comments, event calendars, and many other features allow deep engagement with site visitors.</td>
<td>X</td>
<td>X</td>
<td>X<sup>+</sup></td>
<td>X</td>
<td>X</td>
<td>X</td>
<td>X<sup>+</sup></td>
</tr></tbody></table>

## Assets Features {#assets-matrix}

Below is a matrix of key Assets features offered by AEM. Some of these features were introduced in earlier versions incremental enhancements added in each release.

* [AEM Assets release notes](https://helpx.adobe.com/experience-manager/6-5/release-notes/assets.html)

***X denotes that significant enhancements to the feature in this version.***

***X<sup>+</sup> denotes the feature is available via a Service Pack or Feature Pack.***

<table>
<tbody><tr><td>Assets Feature</td>
<td>5.6.x</td>
<td>6.0</td>
<td>6.1</td>
<td>6.2</td>
<td>6.3</td>
<td>6.4</td>
<td>6.5</td>
</tr><tr><td><strong><a href="https://helpx.adobe.com/experience-manager/6-5/assets/using/managing-assets-touch-ui.html" target="_blank">Touch Optimized UI</a></strong><br>
Manage assets on a desktop computer or on touch-enabled devices.&nbsp;</td>
<td>&nbsp;</td>
<td>X</td>
<td>X<sup>+</sup></td>
<td>X</td>
<td>X</td>
<td>X<sup>+</sup></td>
<td>X<sup>+</sup></td>
</tr><tr><td><strong><a href="https://helpx.adobe.com/experience-manager/6-5/assets/using/metadata.html" target="_blank">Advanced Metadata Management</a><br>
 </strong>Metadata Templates, Metadata Schema Editor and Bulk Metadata Editing.</td>
<td>&nbsp;</td>
<td>X</td>
<td>X</td>
<td>X<sup>+</sup></td>
<td>X</td>
<td>X<sup>+</sup></td>
<td>X<sup>+</sup></td>
</tr><tr><td><strong><a href="https://helpx.adobe.com/experience-manager/6-5/sites/authoring/using/task-content.html" target="_blank">Task</a> and <a href="https://helpx.adobe.com/experience-manager/6-5/sites/authoring/using/projects-with-workflows.html" target="_blank">Workflow</a> Management</strong><br>
Pre-built workflows and tasks for review and approval of digital assets leveraging AEM Projects.</td>
<td>&nbsp;</td>
<td>X</td>
<td>X</td>
<td>X</td>
<td>X<sup>+</sup></td>
<td>X</td>
<td>X</td>
</tr><tr><td><strong>Scalability and Performance</strong><br>
Enhanced support for ingestion, upload and storage at scale.</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>X</td>
<td>X</td>
<td>X<sup>+</sup></td>
</tr><tr><td><strong><a href="https://helpx.adobe.com/experience-manager/6-5/assets/using/mac-api-assets.html" target="_blank">Assets HTTP API</a><br>
 </strong>Programmatically interact with assets via HTTP and JSON.</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>X</td>
<td>X</td>
<td>X</td>
<td>X</td>
<td>X<sup>+</sup></td>
</tr><tr><td><strong><a href="https://helpx.adobe.com/experience-manager/6-5/assets/using/link-sharing.html" target="_blank">Link Share</a></strong><br>
Simple ad-hoc sharing of digital assets without a need to log in.</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>X</td>
<td>X</td>
<td>X</td>
<td>X</td>
</tr><tr><td><strong><a href="https://helpx.adobe.com/experience-manager/brand-portal/using/brand-portal.html" target="_blank">Brand Portal</a></strong><br>
Cloud service SAAS solution for seamless sharing and distribution of digital assets.</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>X</td>
<td>X</td>
<td>X</td>
<td>X<sup>+</sup></td>
</tr><tr><td><strong><a href="https://helpx.adobe.com/experience-manager/6-5/assets/using/use-assets-across-connected-assets-instances.html" target="_blank">Connected Assets</a></strong><br>
AEM Sites instances can seamlessly access and use assets from a different AEM Assets instance.</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>X</td>
</tr><tr><td><strong><a href="https://helpx.adobe.com/experience-manager/6-5/assets/using/touch-ui-asset-insights.html" target="_blank">Asset Insights</a></strong><br>
Leverage Adobe Analytics to capture customer interaction of digital assets and view in AEM.</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>X</td>
<td>X<sup>+</sup></td>
<td>X</td>
<td>X</td>
</tr><tr><td><strong><a href="https://helpx.adobe.com/experience-manager/6-5/assets/using/multilingual-assets.html" target="_blank">Multilingual Assets</a></strong><br>
Translation support of asset metadata automatically with language roots.</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>X</td>
<td>X</td>
<td>X</td>
<td>X</td>
</tr><tr><td><strong><a href="https://helpx.adobe.com/experience-manager/6-5/assets/using/enhanced-smart-tags.html" target="_blank">Smart Tags and Moderation</a></strong><br>
Leverage Adobe Sensei to tag images automatically with useful metadata.</td>
<td>&nbsp;</td>
<td></td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>X</td>
<td>X<sup>+</sup></td>
<td>X</td>
</tr><tr><td><strong><a href="https://helpx.adobe.com/experience-manager/kt/assets/using/smart-translation-search-feature-video-use.html" target="_blank">Smart Translation Search</a></strong><br>
Automatically translate search terms when searching for AEM Assets.</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>X</td>
<td>X</td>
</tr><tr><td><strong><a href="https://helpx.adobe.com/experience-manager/6-5/assets/using/indesign.html" target="_blank">Adobe InDesign Server Integration</a></strong><br>
Generate product catalogs. Create brochures, flyers and print ads based on InDesign templates.</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>X&nbsp;</td>
<td>X</td>
<td>X<sup>+</sup></td>
<td>X</td>
<td>X</td>
</tr><tr><td><strong><a href="https://helpx.adobe.com/experience-manager/desktop-app/aem-desktop-app.html" target="_blank">AEM Desktop App</a></strong><br>
Sync assets to the local desktop for editing with Creative Suite products.<br>
</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>X</td>
<td>X</td>
<td>X<sup>+</sup></td>
<td>X</td>
<td>X<sup>+</sup></td>
</tr><tr><td><strong><a href="https://helpx.adobe.com/experience-manager/6-5/assets/using/imaging-transcoding-library.html" target="_blank">Adobe Imaging Library</a></strong><br>
Photoshop and Acrobat PDF libraries used for high-quality file manipulation.</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>X</td>
<td>X</td>
<td>X</td>
</tr><tr><td><strong><a href="https://www.adobe.com/creativecloud/business/enterprise/adobe-asset-link.html" target="_blank">Adobe Asset Link</a><br>
 </strong>Access AEM Assets directly from Adobe Create Cloud applications.</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>X</td>
<td>X<sup>+</sup></td>
</tr><tr><td><strong><a href="https://helpx.adobe.com/experience-manager/6-5/assets/using/aem-assets-adobe-stock.html" target="_blank">Adobe Stock Integration</a><br>
 </strong>Seamlessly access and use Adobe Stock imagery directly from AEM.</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td valign="middle">X<sup>FP</sup></td>
<td>X</td>
</tr></tbody></table>

### AEM Assets Dynamic Media {#dynamic-media}

***X denotes that significant enhancements to the feature in this version.***

***X<sup>+</sup> denotes the feature is available via a Service Pack or Feature Pack.***

<table>
<tbody><tr><td>Dynamic Media Feature</td>
<td>5.6.x</td>
<td>6.0</td>
<td>6.1</td>
<td>6.2</td>
<td>6.3<br>
+ FP<br>
</td>
<td>6.4</td>
<td>6.5</td>
</tr><tr><td><strong><a href="https://helpx.adobe.com/experience-manager/6-5/assets/using/managing-assets.html" target="_blank">Imaging</a></strong><br>
Dynamically deliver images at different sizes and formats, including Smart Crop.</td>
<td>&nbsp;</td>
<td>X</td>
<td>X</td>
<td>X</td>
<td>&nbsp;X<sup>+</sup></td>
<td>X<sup>+</sup></td>
<td>X</td>
</tr><tr><td><strong><a href="https://helpx.adobe.com/experience-manager/6-5/assets/using/video-profiles.html" target="_blank">Video</a></strong><br>
Advanced video encoding and adaptive video streaming</td>
<td>&nbsp;</td>
<td>X</td>
<td>X</td>
<td>X</td>
<td>&nbsp;X<sup>+</sup><br>
</td>
<td>X<sup>+</sup></td>
<td>X<sup>+</sup></td>
</tr><tr><td><strong><a href="https://helpx.adobe.com/experience-manager/6-5/assets/using/interactive-images.html" target="_blank">Interactive Media</a></strong><br>
Create interactive banners, videos with clickable content to showcase key offers.<a href="https://helpx.adobe.com/experience-manager/6-5/assets/using/managing-viewer-presets.html" target="_blank"></a></td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>X</td>
<td>X</td>
<td>X<sup>+</sup></td>
<td>X</td>
</tr><tr><td><strong>Sets (<a href="https://helpx.adobe.com/experience-manager/6-5/assets/using/image-sets.html" target="_blank">Image</a>, <a href="https://helpx.adobe.com/experience-manager/6-5/assets/using/spin-sets.html" target="_blank">Spin</a>, <a href="https://helpx.adobe.com/experience-manager/6-5/assets/using/mixed-media-sets.html" target="_blank">Mixed Media</a>)</strong><br>
Allow users to zoom, pan, rotate and simulate a 360-degree viewing experience.</td>
<td>&nbsp;</td>
<td>X</td>
<td>X</td>
<td>X</td>
<td>&nbsp;X<sup>+</sup></td>
<td>X</td>
<td>X</td>
</tr><tr><td><strong><a href="https://docs.adobe.com/docs/en/aem/6-5/administer/content/dynamic-media/viewer-presets.html" target="_blank">Viewers</a></strong><br>
Custom branded rich media players and presets with support for different screens/devices.</td>
<td>&nbsp;</td>
<td>X</td>
<td>X</td>
<td>X<sup>+</sup></td>
<td>X</td>
<td>X<sup>+</sup></td>
<td>X</td>
</tr><tr><td><strong><a href="https://helpx.adobe.com/experience-manager/6-5/assets/using/delivering-dynamic-media-assets.html" target="_blank">Delivery</a></strong><br>
Flexible options for linking or embedding of Dynamic Media content and delivery over HTTP/2 protocol.</td>
<td>&nbsp;</td>
<td>X</td>
<td>X</td>
<td>X<sup>+</sup></td>
<td>&nbsp;X<sup>+</sup></td>
<td>X</td>
<td>X</td>
</tr><tr><td><strong>Upgrade from Scene7 to Dynamic Media</strong><br>
Ability to migrate master assets and continue using existing S7 URLs.</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>X</td>
<td>X</td>
<td>X</td>
</tr></tbody></table>

## Forms Features {#forms-matrix}

Below is a matrix of key AEM Forms Add-on features offered by AEM. Some of these features were introduced in earlier versions incremental enhancements added in each release.

* [AEM Forms release notes](https://helpx.adobe.com/experience-manager/6-5/release-notes/forms.html)

***X denotes that significant enhancements to the feature in this version.***

***X<sup>+</sup> denotes the feature is available via a Service Pack or Feature Pack.***

<table>
<tbody><tr><td>Forms Feature</td>
<td>5.6.x</td>
<td>6.0</td>
<td>6.1</td>
<td>6.2</td>
<td>6.3</td>
<td>6.4</td>
<td>6.5</td>
</tr><tr><td><strong><a href="https://helpx.adobe.com/experience-manager/6-4/forms/using/introduction-forms-authoring.html" target="_blank">Adaptive Forms Editor</a></strong><br>
Create engaging, responsive, and adaptive forms based on device and browser settings.</td>
<td>&nbsp;</td>
<td>X</td>
<td>X<sup>+</sup></td>
<td>X<sup>+</sup></td>
<td>X<sup>+</sup></td>
<td>X<sup>+</sup></td>
<td>X</td>
</tr><tr><td><strong><a href="https://helpx.adobe.com/experience-manager/6-4/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.html" target="_blank">Document of Record</a><br>
 </strong>Create a document to ensure long-term storage of a data capture experience or print ready version.</td>
<td>&nbsp;</td>
<td>X</td>
<td>X</td>
<td>X<sup>+</sup></td>
<td>X<sup>+</sup></td>
<td>X</td>
<td>X</td>
</tr><tr><td><strong><a href="https://helpx.adobe.com/experience-manager/6-4/forms/using/themes.html" target="_blank">Theme Editor</a></strong><br>
Create reusable themes to style components and panels of a form.</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>X</td>
<td>X</td>
<td>X<sup>+</sup></td>
<td>X</td>
</tr><tr><td><strong><a href="https://helpx.adobe.com/experience-manager/6-4/forms/using/template-editor.html" target="_blank">Template Editor</a></strong><br>
Standardize and implement best practices for adaptive forms.</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>X</td>
<td>X</td>
<td>X<sup>+</sup></td>
<td>X</td>
</tr><tr><td><strong><a href="https://helpx.adobe.com/aem-forms/6-5/whats-new.html#EnhancedintegrationwithAdobeSign" target="_blank">Adobe Sign Integration</a></strong><br>
Allow deployment of Adobe Sign integrated forms based signing scenarios.</td>
<td>&nbsp;</td>
<td><sup>&nbsp;</sup></td>
<td>&nbsp;</td>
<td>X</td>
<td>X<sup>+</sup></td>
<td>X</td>
<td>X<sup>+</sup></td>
</tr><tr><td><strong><a href="https://helpx.adobe.com/experience-manager/6-4/forms/using/cm-overview.html" target="_blank">Correspondence Management</a></strong><br>
With AEM Forms, you can create, manage, and deliver personalized and interactive customer correspondences.<br>
</td>
<td>&nbsp;</td>
<td>X</td>
<td>X</td>
<td>X</td>
<td>X<sup>+</sup></td>
<td>X</td>
<td>X</td>
</tr><tr><td><strong><a href="https://helpx.adobe.com/aem-forms/6-5/whats-new.html#AEMFormsdataintegration" target="_blank">Third-Party Data Integration</a></strong><br>
Using Data Integration, data is fetched from disparate data sources based on user inputs in a form. On form submission, the captured data is written back to the data sources.<br>
</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>X</td>
<td>X<sup>+</sup></td>
<td>X<sup>+</sup></td>
</tr><tr><td><strong><a href="https://helpx.adobe.com/aem-forms/6-5/whats-new.html#FormscentricAEMWorkflowsforAEMFormsonOSGi" target="_blank">Workflow (on OSGi) for Forms Processing</a><br>
 </strong>Simplified deployment of forms approval processes.</td>
<td>&nbsp;</td>
<td><sup>&nbsp;</sup></td>
<td><sup>&nbsp;</sup></td>
<td>&nbsp;</td>
<td>X</td>
<td>X<sup>+</sup></td>
<td>X<sup>+</sup></td>
</tr><tr><td><a href="https://helpx.adobe.com/experience-manager/6-4/forms/user-guide.html?topic=/experience-manager/6-4/forms/morehelp/integrations.ug.js" target="_blank"><strong>Integration with Marketing Cloud</strong></a><br>
Integration with Adobe Analytics and Adobe Target to enhance and measure customer experiences.</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>X</td>
<td>X</td>
<td>X</td>
<td>X</td>
<td>X</td>
</tr><tr><td><strong><a href="https://helpx.adobe.com/experience-manager/6-4/forms/using/introduction-managing-forms.html" target="_blank">Form Manager</a><br>
 </strong>Single location to manage all form/document/correspondence such as enabling analytics, translation, A/B testing, reviews, and publishing.<br>
</td>
<td>&nbsp;</td>
<td>X</td>
<td>X</td>
<td>X</td>
<td>X<sup>+</sup></td>
<td>X</td>
<td>X</td>
</tr><tr><td><strong><a href="https://helpx.adobe.com/experience-manager/6-4/forms/using/aem-forms-app.html" target="_blank">AEM Forms App</a><br>
 </strong>Allow for online/offline forms processing within an app on iOS, Android, or Windows.</td>
<td>&nbsp;</td>
<td>X</td>
<td>X</td>
<td>X<sup>+</sup></td>
<td>X<sup>+</sup></td>
<td>X</td>
<td>X</td>
</tr><tr><td><strong><a href="https://helpx.adobe.com/aem-forms/6-5/adaptive-document.html" target="_blank">Interactive Communications</a><br>
 </strong>Create rich communications such as targeted statements with interactive elements such as charts (formerly known as Adaptive Documents).</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>X</td>
<td>X</td>
<td>X<sup>+</sup></td>
<td>X<sup>+</sup></td>
<td>X<sup>+</sup></td>
</tr><tr><td><strong><a href="https://helpx.adobe.com/pdf/aem-forms/6-5/WorkbenchHelp.pdf" target="_blank">Workflow (J2EE) for Forms Processing</a><br>
 </strong>Build complex forms/document-centric workflows utilizing an intuitive IDE.</td>
<td></td>
<td>X</td>
<td>X</td>
<td>X</td>
<td>X</td>
<td>X</td>
<td>X</td>
</tr><tr><td><strong><a href="https://helpx.adobe.com/aem-forms/6-5/whats-new.html#EnhancedDocumentSecurity" target="_blank">AEM Forms Document Security</a><br>
 </strong>Secure access and authorization of PDF and Office documents.<br>
</td>
<td>&nbsp;</td>
<td>X</td>
<td>X</td>
<td>X<sup>+</sup></td>
<td>X<sup>+</sup></td>
<td>X</td>
<td>X</td>
</tr><tr><td><strong><a href="https://helpx.adobe.com/aem-forms/6-5/whats-new.html#Simplifiedauthoringexperience" target="_blank">Testing Frameworks</a><br>
 </strong>Use the Calvin framework and Chrome plugin to support and debug adaptive forms.</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>X</td>
<td>X</td>
<td>X</td>
</tr></tbody></table>

## Communities Features {#communities}

Below is a matrix of key AEM Communities Add-on features offered by AEM. Some of these features were introduced in earlier versions incremental enhancements added in each release.

* [AEM Communities new feature summary](https://helpx.adobe.com/experience-manager/6-5/communities/using/whats-new-aem-communities.html#main-pars_text)

<table>
<tbody><tr><td>&nbsp;</td>
<td>Communities Feature</td>
<td>6.0</td>
<td>6.1</td>
<td>6.2</td>
<td>6.3</td>
<td>6.4</td>
<td>6.5</td>
</tr><tr><td rowspan="7">Communities Functions</td>
<td><a href="https://helpx.adobe.com/experience-manager/6-5/communities/using/forum.html" target="_blank"><strong>Forums</strong></a><br>
(Social Component Framework)<br>
Create new topics, or view, follow, search, and move existing topics.</td>
<td valign="top">X<sup>+</sup></td>
<td>X</td>
<td>X</td>
<td>X</td>
<td>X</td>
<td>X</td>
</tr><tr><td><p><a href="https://helpx.adobe.com/experience-manager/6-5/communities/using/working-with-qna.html" target="_blank"><strong>QnA</strong></a><br>
Ask, view, and answer questions.</p>
</td>
<td><sup>&nbsp;</sup></td>
<td>X<sup>+</sup></td>
<td>X</td>
<td>X</td>
<td>X</td>
<td>X</td>
</tr><tr><td><p><a href="https://helpx.adobe.com/experience-manager/6-5/communities/using/blog-feature.html" target="_blank"><strong>Blogs</strong></a><br>
Create blog articles and comments on the publish side.</p>
</td>
<td>&nbsp;</td>
<td>X<sup>+</sup></td>
<td>X</td>
<td>X</td>
<td>X</td>
<td>X</td>
</tr><tr><td><p><a href="https://helpx.adobe.com/experience-manager/6-5/communities/using/ideation-feature.html" target="_blank"><strong>Ideation</strong></a><br>
Create and share ideas with the community, or view, follow and comment on existing ideas.</p>
</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>X<sup>+</sup></td>
<td>X</td>
<td>X</td>
<td>X</td>
</tr><tr><td><p><a href="https://helpx.adobe.com/experience-manager/6-5/communities/using/calendar.html" target="_blank"><strong>Calendar</strong></a><br>
(Social Component Framework)<br>
Provide community events information to site visitors.</p>
</td>
<td>X<sup>+</sup></td>
<td>X<sup>+</sup></td>
<td>X</td>
<td>X</td>
<td>X</td>
<td>X</td>
</tr><tr><td><strong><a href="https://helpx.adobe.com/experience-manager/6-5/communities/using/file-library.html" target="_blank">File Library</a></strong><br>
Upload, manage and download files within the community site.</td>
<td>&nbsp;</td>
<td>X<sup>+</sup></td>
<td>X</td>
<td>X</td>
<td>X</td>
<td>X</td>
</tr><tr><td><strong><a href="https://helpx.adobe.com/experience-manager/6-5/communities/using/users.html#AboutCommunityGroups" target="_blank">User Groups</a><br>
 </strong>A set of users can belong to member groups, and can be collectively assigned roles. &nbsp;</td>
<td>X</td>
<td>X</td>
<td>X</td>
<td>X</td>
<td>X</td>
<td>X</td>
</tr><tr><td><strong>&nbsp;</strong></td>
<td><strong><a href="https://helpx.adobe.com/experience-manager/6-5/communities/using/resource.html" target="_blank">Assignment</a><br>
 </strong>Create and assign learning resources to community members.</td>
<td>&nbsp;</td>
<td>X<sup>+</sup></td>
<td>X</td>
<td>X</td>
<td>X</td>
<td>X</td>
</tr><tr><td rowspan="5">Enablement</td>
<td><a href="https://helpx.adobe.com/experience-manager/6-5/communities/using/catalog.html" target="_blank" >Catalog</a><strong> and </strong><a href="https://helpx.adobe.com/experience-manager/6-5/communities/using/resource.html" target="_blank" >Resource Management</a><br>
Access enablement resources from catalog.</td>
<td>&nbsp;</td>
<td>X<sup>+</sup></td>
<td>X</td>
<td>X</td>
<td>X</td>
<td>X</td>
</tr><tr><td><strong><a href="https://helpx.adobe.com/experience-manager/6-5/communities/using/resources.html#CreateaLearningPath" target="_blank">Learning Paths Management</a><br>
 </strong>Manage courses or groups of enablement resources.</td>
<td>&nbsp;</td>
<td>X<sup>+</sup></td>
<td>X</td>
<td>X</td>
<td>X</td>
<td>X</td>
</tr><tr><td><strong><a href="https://helpx.adobe.com/experience-manager/6-5/communities/using/reports.html#main-pars_text_1739724213" target="_blank">Enablement Reporting</a></strong><br>
Reporting on enablement resources and learning paths.</td>
<td>&nbsp;</td>
<td>X<sup>+</sup></td>
<td>X</td>
<td>X</td>
<td>X</td>
<td>X</td>
</tr><tr><td><strong><a href="https://helpx.adobe.com/experience-manager/6-5/communities/using/resources.html#main-pars_text_899882038" target="_blank">Engagement on Enablement</a><br>
 </strong>Add comments on enablement resources.</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>X<sup>+</sup></td>
<td>X</td>
<td>X</td>
<td>X</td>
</tr><tr><td><strong><a href="https://helpx.adobe.com/experience-manager/6-5/communities/using/analytics.html" target="_blank">Enablement Analytics</a></strong><br>
Video Analytics, Progress Reporting, and Assignment Reporting<strong><a href="https://helpx.adobe.com/experience-manager/6-5/communities/using/reports.html#main-pars_text_1739724213"></a></strong></td>
<td>&nbsp;</td>
<td>X<sup>+</sup></td>
<td>X</td>
<td>X</td>
<td>X</td>
<td>X</td>
</tr><tr><td rowspan="8">Commons</td>
<td><strong><a href="https://helpx.adobe.com/experience-manager/6-5/communities/using/comments.html" target="_blank">Comments</a> </strong>and attachments<br>
(social component framework)<br>
As a community member share opinion and knowledge about content on Communities site.</td>
<td>X<sup>+</sup></td>
<td>X</td>
<td>X<sup>+</sup></td>
<td>X</td>
<td>X<sup>+</sup></td>
<td>X</td>
</tr><tr><td><strong>Content fragment conversion<br>
 </strong>Convert UGC contributions to content fragments.</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>X<sup>+</sup></td>
<td>X</td>
<td>X</td>
<td>X</td>
</tr><tr><td><strong><a href="https://helpx.adobe.com/experience-manager/6-5/communities/using/reviews.html" target="_blank">Reviews</a></strong><br>
(social component framework)<br>
As a community member review a piece of content using a combination of comments and rating functions.</td>
<td>X<sup>+</sup></td>
<td>X<sup>+</sup></td>
<td>X</td>
<td>X</td>
<td>X</td>
<td>X</td>
</tr><tr><td><strong><a href="https://helpx.adobe.com/experience-manager/6-5/communities/using/rating.html" target="_blank">Ratings</a></strong><br>
(social component framework)<br>
As a community member rate a piece of content.</td>
<td>X<sup>+</sup></td>
<td>X</td>
<td>X</td>
<td>X</td>
<td>X</td>
<td>X</td>
</tr><tr><td><strong><a href="https://helpx.adobe.com/experience-manager/6-5/communities/using/voting.html" target="_blank">Votes</a></strong><br>
(social component framework)<br>
As a community member upvote or downvote a piece of content.</td>
<td>X<sup>+</sup></td>
<td>X</td>
<td>X</td>
<td>X</td>
<td>X</td>
<td>X</td>
</tr><tr><td><strong><a href="https://helpx.adobe.com/experience-manager/6-5/communities/using/tag-ugc.html" target="_blank">Tags</a><br>
 </strong>Attach tags (keywords or labels) with content to quickly locate content.</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>X<sup>+</sup></td>
<td>X</td>
<td>X</td>
</tr><tr><td><strong><a href="https://helpx.adobe.com/experience-manager/6-5/communities/using/search.html" target="_blank">Search</a><br>
 </strong>Predictive and suggestive searches.</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>X<sup>+</sup></td>
<td>X</td>
<td>X</td>
<td>X</td>
</tr><tr><td><strong><a href="https://helpx.adobe.com/experience-manager/6-5/communities/using/translate-ugc.html" target="_blank">Translation</a><br>
 </strong>Machine translation of user-generated content.</td>
<td>X<sup>+</sup></td>
<td>X</td>
<td>X<sup>+</sup></td>
<td>X</td>
<td>X</td>
<td>X</td>
</tr><tr><td rowspan="10">Administration</td>
<td><strong><a href="https://helpx.adobe.com/experience-manager/6-5/communities/using/create-site.html" target="_blank">Site Management</a></strong><br>
Creating sites with communities functions.</td>
<td>&nbsp;</td>
<td>X</td>
<td>X<sup>+</sup></td>
<td>X</td>
<td>X<sup>+</sup></td>
<td>X</td>
</tr><tr><td><strong><a href="https://helpx.adobe.com/experience-manager/6-5/communities/using/sites.html" target="_blank">Templates</a></strong><br>
<a href="https://helpx.adobe.com/experience-manager/6-5/communities/using/sites.html" target="_blank">Site</a> and <a href="https://helpx.adobe.com/experience-manager/6-5/communities/using/tools-groups.html" target="_blank">group</a> templates for wizard-based creation of fully functional Community sites.</td>
<td>&nbsp;</td>
<td>X<sup>+</sup></td>
<td>X</td>
<td>X</td>
<td>X</td>
<td>X</td>
</tr><tr><td><strong>Editable Templates<br>
 </strong>Empower community administrators to build out rich experiences using AEM Editable Templates.&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>X</td>
</tr><tr><td><strong><a href="https://helpx.adobe.com/experience-manager/6-5/communities/using/creating-groups.html" target="_blank">Groups or Sub-Communities</a></strong><br>
Dynamically create sub-communities within communities sites.<br>
</td>
<td>&nbsp;</td>
<td>X<sup>+</sup></td>
<td>X</td>
<td>X</td>
<td>X</td>
<td>X</td>
</tr><tr><td><strong><a href="https://helpx.adobe.com/experience-manager/6-5/communities/using/in-context.html" target="_blank">Moderation</a></strong><br>
Moderating user-generated content.<br>
</td>
<td>X</td>
<td>X</td>
<td>X</td>
<td>X</td>
<td>X</td>
<td>X</td>
</tr><tr><td><strong><a href="https://helpx.adobe.com/experience-manager/6-5/communities/using/moderation.html" target="_blank">Bulk moderation</a><br>
 </strong>Moderation console to bulk manage user generated content.</td>
<td>&nbsp;</td>
<td>X<sup>+</sup></td>
<td>X</td>
<td>X<br>
</td>
<td>X</td>
<td>X<sup>+</sup></td>
</tr><tr><td><strong><a href="https://helpx.adobe.com/experience-manager/6-5/communities/using/moderate-ugc.html#CommonModerationConcepts" target="_blank">Spam detection and Profanity filters</a><br>
 </strong>Automatic spam detection. <strong>&nbsp;</strong></td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>X<sup>+</sup></td>
<td>X</td>
<td>X</td>
</tr><tr><td><strong><a href="https://helpx.adobe.com/experience-manager/6-5/communities/using/members.html" target="_blank">Member Management</a></strong><br>
Manage user profiles and groups from member management area.</td>
<td>&nbsp;</td>
<td>X<sup>+</sup></td>
<td>X</td>
<td>X</td>
<td>X<sup>+</sup></td>
<td>X</td>
</tr><tr><td><strong><a href="https://helpx.adobe.com/experience-manager/6-5/communities/using/overview.html#main-pars_text_866731966" target="_blank">Responsive Design</a></strong><br>
AEM Communities sites are responsive.<br>
</td>
<td>&nbsp;</td>
<td>X</td>
<td>X</td>
<td>X</td>
<td>X</td>
<td>X</td>
</tr><tr><td><strong><a href="https://helpx.adobe.com/experience-manager/6-5/communities/using/analytics.html" target="_blank">Analytics</a></strong><br>
Integrate with Adobe Analytics for key insights into&nbsp;Communities sites usage.</td>
<td>X<sup>+</sup></td>
<td>X</td>
<td>X</td>
<td>X</td>
<td>X</td>
<td>X</td>
</tr><tr><td rowspan="4">Members</td>
<td><strong><a href="https://helpx.adobe.com/experience-manager/6-5/communities/using/advanced.html" target="_blank">Scoring and Badging</a><br>
 </strong>(Advanced scoring powered by Adobe Sensei)<br>
Identify community members as experts and reward them.</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>X</td>
<td>X</td>
<td>X</td>
<td>X</td>
</tr><tr><td><strong><a href="https://helpx.adobe.com/experience-manager/6-5/communities/using/activities.html" target="_blank">Activities</a> and <a href="https://helpx.adobe.com/experience-manager/6-5/communities/using/notifications.html" target="_blank">Notifications</a></strong><br>
View recent activities stream, and get notified about events of interest.</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
</tr><tr><td><strong><a href="https://helpx.adobe.com/experience-manager/6-5/communities/using/configure-messaging.html" target="_blank">Messages</a></strong><br>
Direct messaging to users and groups.</td>
<td>X</td>
<td>X</td>
<td>X</td>
<td>X</td>
<td>X</td>
<td>X<sup>+</sup></td>
</tr><tr><td><strong><a href="https://helpx.adobe.com/experience-manager/6-5/communities/using/social-login.html" target="_blank">Social Logins</a></strong><br>
Sign in with their Facebook or Twitter account.</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>X<sup>+</sup></td>
<td>X</td>
<td>X</td>
<td>X</td>
</tr><tr><td rowspan="5">Platform</td>
<td><a href="https://helpx.adobe.com/experience-manager/6-5/communities/using/working-with-srp.html" target="_blank"><strong>MSRP (Mongo Storage)</strong></a><br>
User-generated content (UGC) is persisted directly in a local MongoDB instance</td>
<td>&nbsp;</td>
<td>X<sup>+</sup></td>
<td>X</td>
<td>X</td>
<td>X</td>
<td>X</td>
</tr><tr><td><a href="https://helpx.adobe.com/experience-manager/6-5/communities/using/working-with-srp.html" target="_blank"><strong>DSRP (Database Storage)</strong></a><br>
User-generated content (UGC) is persisted directly in a local MySQL database instance.</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>X<sup>+</sup></td>
<td>X</td>
<td>X</td>
<td>X</td>
</tr><tr><td><a href="https://helpx.adobe.com/experience-manager/6-5/communities/using/working-with-srp.html" target="_blank"><strong>ASRP (Cloud Storage)</strong></a><br>
User-generated content (UGC)&nbsp;UGC is persisted remotely in a cloud service hosted and managed by Adobe.</td>
<td>X<sup>+</sup></td>
<td>X</td>
<td>X</td>
<td>X</td>
<td>X</td>
<td>X</td>
</tr><tr><td><a href="https://helpx.adobe.com/experience-manager/6-5/communities/using/working-with-srp.html" target="_blank"><strong>JSRP</strong></a><br>
Community content is stored in&nbsp;JCR&nbsp;and UGC is accessible from author (or publish) instance to which it was posted.</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>X<sup>+</sup></td>
<td>X</td>
<td>X</td>
<td>X</td>
</tr><tr><td><a href="https://helpx.adobe.com/experience-manager/6-5/communities/using/sync.html" target="_blank"><strong>User and Group Sync</strong></a><br>
Synchronize users and groups across publish instances when using a Publish farm topology.</td>
<td>X<sup>+</sup></td>
<td>X</td>
<td>X</td>
<td>X</td>
<td>X</td>
<td>X</td>
</tr></tbody></table>

***X denotes that significant enhancements to the feature in this version.***

***X<sup>+</sup> denotes the feature is available via a Service Pack or Feature Pack.***

AEM Communities adds [enhancements](https://helpx.adobe.com/experience-manager/6-5/communities/using/whats-new-aem-communities.html) through releases to enable organizations to engage and enable their users, by:

* **@mention** support in user-generated content.
* Accessibility improvements through **Keyboard Navigation** in **Enablement** components.
* Improved **Bulk Moderation** using **Custom Filters**.
* **Editable Templates** to empower community administrators to build rich  community experiences in AEM.
* Users can now send **direct messages in bulk** to all members of a group.
