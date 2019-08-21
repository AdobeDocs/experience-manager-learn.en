---
title: Certifying Document in AEM Forms
seo-title: Certifying Document in AEM Forms
description: null
seo-description: null
uuid: ecb1f9b6-bbb3-43a3-a0e0-4c04411acc9f
contentOwner: gbedekar
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: document_services
discoiquuid: 9fd78c7f-ffa6-457e-b866-cd27d671732c
index: y
internal: n
snippet: y
---

# Certifying Document in AEM Forms{#certifying-document-in-aem-forms}

A Certified Document provides PDF document and forms recipients with added assurances of its authenticity and integrity.

To certify a document, you can use Acrobat DC on the desktop or AEM Forms Document Services as part of an automated process on a server.

This tutorial explains the steps needed to automate the certification process using AEM Forms Document Services.

## Adding certificate to trust store {#adding-certificate-to-trust-store}

Please follow the steps mentioned below to add the certificate to keystore in AEM

* [Login to AEM](/libs/granite/security/content/useradmin) as admin user
* Search for admin user
* Double click the admin user to open the user settings window
* Click on Keystore tab
* Click Create Keystore
* Set the keystore access password. For this tutorial we have set the password to "password"
* Expand the "Add Private Key from KeyStore file"
* Provide the following properties as specified here

    * New Alias: certifypdf
    * Select KeyStore File: upload the gbedekar.p12 file
    * Keystore file password: password
    * private key alias:gbedekar
    * private key password:password
    * click submit

* Click Save and Close to save your changes

## Deploying OSGI Bundle {#deploying-osgi-bundle}

You can write your own OSGi bundle and use the AEM Forms Client SDK to certify the bundle. The steps to write your own OSGi bundle are as follows

* [Creating your first OSGi bundle](https://helpx.adobe.com/experience-manager/using/maven_arch13.html)
* [Use Document Service API](https://helpx.adobe.com/experience-manager/6-4/forms/using/aem-document-services-programmatically.html)

Or you can use the sample bundle included as part of this tutorial assets. The assets are available at the bottom of this page.

## Testing the sample using Postman {#testing-the-sample-using-postman}

Once you deploy the assets related to this tutorial, you are ready to make POST calls to the endpoint exposed by this tutorial. The easiest way is to use Postman chrome extension for testing REST API.

The endpoint is http://localhost:4502/content/AemFormsSamples/certifypdf

The REST endpoint takes 2 parameters

* pdfFile - This is the document that you want to certify
* saveLocation - This is the save location on the server where the certified pdf will be stored. Please make sure the directory in which you are storing exists. The sample code does not create the directory structure

If you are running the sample on author instance, please provide the authentication parameters to AEM server. Typically these are admin/admin.

Import this zip file using package manager

[Get File](assets/certifydocumentassets.zip)

This zip file contains a sample certificate and Postman request. Unzip this file and extract the content on to your hard drive

[Get File](assets/certificateandpostman.zip)
