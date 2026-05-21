---
title: Prefill adaptive form with data from sharepoint list
description: Learn how to prefill adaptive form using form data model backed by share point list
feature: Adaptive Forms
type: Documentation
role: Developer
level: Beginner
version: Experience Manager as a Cloud Service
topic: Integrations
jira: KT-14795
badgeVersions: label="AEM Forms as a Cloud Service" before-title="false"
duration: 46
exl-id: 9abe9f9d-8fb3-4e01-a830-1dad1c27274d
TQID: https://experienceleague.adobe.com/V5WlwAGZpkgbn4QC-rFIOCx7X22gna3MmJVbsBtDc9A
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: ae478996-b206-4712-9b0c-dc78a2644453
    internal-label: Integrations
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
---
# Prefill adaptive form with share point list data

In the previous version of AEM Form(6.5), custom code had to be written to prefill form data model backed adaptive form using request attribute. In AEM Forms as cloud service, the need to write custom code is not longer required.

This article explains the steps required to prefill/pre-populate adaptive form with data fetched from SharePoint list using the form data model prefill service. 

This article assumes you have [successfully configured adaptive form to submit data to SharePoint list.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/configure-submit-actions-core-components.html?lang=en#connect-af-sharepoint-list)

The following is the data in the SharePoint list
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
