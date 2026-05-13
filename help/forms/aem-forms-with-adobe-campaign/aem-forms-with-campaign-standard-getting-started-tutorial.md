---
title: Integrate AEM Forms and Adobe Campaign Standard
description: Integrate AEM Forms with Adobe Campaign Standard using AEM Forms Form Data Model to fetch ACS campaign profile information etc.
feature: Adaptive Forms, Form Data Model
version: Experience Manager 6.4, Experience Manager 6.5
topic: Integrations, Development
role: Developer
level: Experienced
exl-id: e028837b-13d8-4058-ac25-ed095f49524c
badgeIntegration: label="Integration" type="positive"
badgeVersions: label="AEM Forms 6.5" before-title="false"
last-substantial-update: 2020-03-20T00:00:00.000Z
duration: 44
TQID: https://experienceleague.adobe.com/U6dcxrb-mNA56aY09wZAo5PW0V97nJ4DR2Rl4woKmJI
product_v2:
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: a01bfd36-4ab8-4bf8-9dc0-5b45b890552e
    internal-label: APIs
  - id: a1df6763-63b5-45b4-8c8a-155a692a2b3e
    internal-label: Integrations
  - id: ae478996-b206-4712-9b0c-dc78a2644453
    internal-label: Integrations
  - id: f013e6ab-27b8-4645-b5a7-31ffa474d04f
    internal-label: APIs
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
---
# Integrate AEM Forms and Adobe Campaign Standard

 ![formsandcampaign](assets/helpx-cards-forms.png)

Learn how to integrate AEM Forms with Adobe Campaign Standard (ACS).

ACS has a rich set of API's exposed which allows ACS to be interfaced with the technology of our choice. In this tutorial, we will concentrate on interfacing AEM Forms with ACS.

To integrate AEM Forms with ACS you will need to follow the following steps:

* [Set up API access on your ACS instance.](https://experienceleague.adobe.com/docs/campaign-standard/using/working-with-apis/get-started-apis.html?lang=en)
* Create JSON Web Token.
* Exchange the JSON Web Token with Adobe Identity Management Service for an Access Token.
* Include this Access Token in Authorization HTTP Header, along with X-API-Key in every request to ACS instance.

To get started please follow the following instructions

* [Download and unzip the assets related to this tutorial.](assets/aem-forms-and-acs-bundles.zip)
* Deploy the bundles using [Felix web console](http://localhost:4502/system/console/bundles)
* Provide the appropriate settings for Adobe Campaign in Felix OSGI Configuration.
* [Create a service user as mentioned in this article](/help/forms/adaptive-forms/service-user-tutorial-develop.md). Make sure to deploy the OSGi bundle associated with the article.
* Store the ACS private key in etc/key/campaign/private.key. You will have to create a folder called campaign under etc/key.
* [Provide read access to the campaign folder to the service user "data".](http://localhost:4502/useradmin)

## Next Steps

[Generate JWT and Access Token](partone.md)
