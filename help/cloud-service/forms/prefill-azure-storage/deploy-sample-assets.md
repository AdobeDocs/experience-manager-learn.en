---
title: Deploy the sample assets
description: Deploy the sample assets on your local cloud ready system.
feature: Adaptive Forms
type: Documentation
role: Developer
level: Beginner
version: Cloud Service
topic: Integrations
kt: 13717
exl-id: ae8104fa-7af2-49c2-9e6b-704152d49149
---
# Deploy the sample assets

To get this use case working on your system, please deploy the following assets on your local cloud ready system.

*   Please make sure you have created all the required configurations/accounts listed in the[introduction document](./introduction.md)

*   [Install the custom adaptive form template and the associated page component](./assets/azure-portal-template-page-component.zip)

*   [Install the SendGrid Form Data Model](./assets/send-grid-form-data-model.zip). You will have to provide your API key and SendGrid verified from address for this form data model to work. Test the form data model in the form data model editor

*   [Install the Azure backed Form Data Model](./assets/azure-storage-fdm.zip). You will have to provide your Azure Storage account credentials for the form data model to work. Test the form data model in the form data model editor.

*   [Import the sample adaptive form](./assets/credit-applications-af.zip)
*   [Import the client library](./assets/client-lib.zip)
*   [Preview the form](http://localhost:4502/content/dam/formsanddocuments/azureportalstorage/creditapplications/jcr:content?wcmmode=disabled). Enter a valid e-mail and click on the save button. The form data should get stored in the Azure Storage and an e-mail with an link to the saved form will be sent to the e-mail address specified.
