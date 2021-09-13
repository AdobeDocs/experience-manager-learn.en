---
title: Getting Started with AEM Forms and Adobe Campaign Standard
description: Integrate AEM Forms with Adobe Campaign Standard using AEM Forms Form Data Model to fetch ACS campaign profile information etc.
feature: Adaptive Forms, Form Data Model
version: 6.3,6.4,6.5
topic: Development
role: Developer
level: Experienced
exl-id: e028837b-13d8-4058-ac25-ed095f49524c
---
# Getting Started with AEM Forms and Adobe Campaign Standard {#getting-started-with-aem-forms-and-adobe-campaign-standard}

 ![formsandcampaign](assets/helpx-cards-forms.png)

This tutorial will list the various use cases for integrating AEM Forms with Adobe Campaign Standard(ACS).

ACS has a rich set of API's exposed which allows ACS to be interfaced with the technology of our choice. In this tutorial, we will concentrate on interfacing AEM Forms with ACS.

To integrate AEM Forms with ACS you will need to follow the following steps:

* [Set up API acess on your ACS instance.](https://docs.campaign.adobe.com/doc/standard/en/api/ACS_API.html#setting-up-api-access)
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
