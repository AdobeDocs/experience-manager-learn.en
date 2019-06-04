---
title: AEM Forms with Marketo(Part 1)
seo-title: AEM Forms with Marketo(Part 1)
description: Tutorial to integrate AEM Forms with Marketo using AEM Forms Form Data Model.
seo-description: Tutorial to integrate AEM Forms with Marketo using AEM Forms Form Data Model.
---

# AEM Forms With Marketo

Marketo, part of Adobe provides Marketing Automation software focused on account-based marketing, including email, mobile, social, digital ads, web management, and analytics.

Using the Form Data Model of AEM Forms we can now integrate AEM Form with Marketo seamlessly.

[Learn more about the Form Data Model](https://helpx.adobe.com/experience-manager/6-5/forms/using/data-integration.html)

Marketo exposes a REST API which allows for remote execution of many of the system’s capabilities. From creating programs to bulk lead import, there are many options which allow fine-grained control of a Marketo instance. Using the Form Data Model it is quite simple to integrate AEM Forms with Marketo.

This tutorial will walk you through the steps involved in integrating AEM Forms with Marketo using Form Data Model. On completing the tutorial you will have an OSGi bundle that will do the custom authentication against Marketo. You will also have configured data source using the provided swagger file.

To get started it is highly recommended that you are familiar with the following topics listed in the Prerequisite section.

## Prerequisite

 1. [AEM server  with AEM Forms Add on package installed](/help/forms/adaptive-forms/installing-aem-form-on-windows-tutorial-use.md)
 1. Local AEM  Development Environment
 1. Familiar with Form Data Model
 1. Basic knowledge of Swagger Files
 1. Creating Adaptive Forms

**Client Secret ID and Client Secret Key**

The first step in the integration of Marketo with AEM Forms is to obtain the API credentials that are needed to make the REST calls using API. You will need the following

1. client_id
1. client_secret
1. identity_endpoint
1. authentication URL.

[Please follow the official Marketo documentation to get the above-mentioned properties.](https://developers.marketo.com/rest-api/) Alternatively, you can also contact the administrator of your Marketo instance.

**Before you begin**

[Download and unzip the assets related to this article.](assets/aemformsandmarketo.zip) The zip file contains the following:

1. BlankTemplatePackage.zip - This is the Adaptive Form template. Import this using the package manager.
1. marketo.json - This is the swagger file that will be used to configure the data source.
1. MarketoAndForms.MarketoAndForms.core-1.0-SNAPSHOT.jar - This is the bundle that does the custom authentication. Feel free to use this if you are unable to complete the tutorial or your bundle is not working as expected.
