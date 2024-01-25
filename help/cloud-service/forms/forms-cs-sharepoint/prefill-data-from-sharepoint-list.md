---
title: Prefill adaptive form with data from sharepoint list
description: Learn how to prefill adaptive form using form data model backed by share point list
feature: Adaptive Forms
type: Documentation
role: Developer
level: Beginner
version: Cloud Service
topic: Integrations
jira: KT-14795
duration: 60
---
# Prefill adaptive form with share point list data

In the previous version of AEM Form(6.5), custom code had to be written to prefill form data model backed adaptive form using request attribute. In AEM Forms as cloud service, the need to write custom code is not longer required.

This article explains the steps required to prefill/pre-populate adaptive form with data fetched from sharepoint list using the form data model prefill service. 

This article assumes you have [successfully configured adaptive form to submit data to sharepoint list.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/configure-submit-actions-core-components.html?lang=en#connect-af-sharepoint-list)

The following is the data in the sharepoint list
![sharepoint-list](assets/list-data.png) 

To prefill an adaptive form with the data associated with a particular guid the following steps need to be performed

## Configure the get service

* Create a get service for the top level object of the form data model using the guid attribute
![get-service](assets/mapping-request-attribute.png)

In this screenshot, the guid column is bound via a request attribute called `submissionid`.

The get service fully configured looks like this

![get-service](assets/fdm-request-attribute.png)

## Configure the adaptive form to use form data model prefill service

* Open an adaptive form based on the share point list form data model. Associate the Form Data Model Prefill service
![form-prefill-service](assets/form-prefill-service.png)

## Test the form

Preview the form by including the `submissionid` in the URL as shown below

```html
http://localhost:4502/content/dam/formsanddocuments/contactusform/jcr:content?wcmmode=disabled&submissionid=57e12249-751a-4a38-a81f-0a4422b24412
```




