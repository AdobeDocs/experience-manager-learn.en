---
title: Deploy the sample
description: Get use case running on your local AEM Forms instance
feature: Adaptive Forms
type: Tutorial
version: 6.4,6.5
jira: KT-6602
thumbnail: 6602.jpg
topic: Development
role: Developer
level: Intermediate
exl-id: cdfae631-86d7-438f-9baf-afd621802723
duration: 186
---
# Deploy the sample

To get this use case working on your system, please follow the following instructions:

>[!NOTE]
>It is assumed that you are running AEM Forms on port 4502.


## Create database

This sample uses MySQL database to store the adaptive form data. You will need to create the [database schema by importing the schema file](assets/data-base-schema.sql) into MySQL workbench. 

## Create datasource

You need to create a Apache Sling Connection Pooled DataSource called **StoreAndRetrieveAfData** pointing to the  database schema created in the earlier step. The code in the OSGi bundle uses this datasource name.

## Create Form Data Model

Form Data Model needs to be created based on this datasource called **StoreAndRetrieveAfData**. This form data model is used to fetch the mobile phone number associated with the application id. The form data model can be [downloaded from here.](assets/2-Factor-Authentication-DataSource-and-FDM.zip)

## Create developer account with nexmo

Create a developer account with [Nexmo](https://dashboard.nexmo.com/) for sending and verifying OTP codes. Make a note of the API Key and API Secret Key. The data source and form data model have already been created for you against this service and are included with the assets mentioned in the previous step.

## Deploy the following OSGi bundles

Deploy the bundle which has the [code to store and fetch data from database](assets/SaveAndResume.core-1.0.0-SNAPSHOT.jar)
Download and unzip the [developingwithserviceuser.zip](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/developingwithserviceuser.zip). 
Deploy the DevelopingWithServiceUser.jar file using the Felix web console.

## Deploy the client library

The sample uses 2 client libraries. Import these [client libraries](assets/store-af-with-attachments-client-lib.zip) into AEM.

## Import the custom adaptive form template

The sample forms used in this demo are based on a custom template. Import the [custom template into AEM](assets/custom-template-with-page-component.zip)

## Import the sample adaptive forms

The 2 forms that make up this sample need to be imported into AEM. The sample forms can be [downloaded from here](assets/sample-forms.zip)

Open the [MyAccountForm](http://localhost:4502/editor.html/content/forms/af/myaccountform.html) in edit mode. Specify the Vonage API Key and API Secret values  in the appropriate fields in the adaptive form.

## Test the solution

Preview the [StoreAFWithAttachments](http://localhost:4502/content/dam/formsanddocuments/storeafwithattachments/jcr:content?wcmmode=disabled)
Enter your mobile number including the country code ,fill in your user details and add some attachments. Click the "Save And Exit" button to save the adaptive form and its attachments


## Demonstration of the use case

>[!VIDEO](https://video.tv.adobe.com/v/327122?quality=12&learn=on)
