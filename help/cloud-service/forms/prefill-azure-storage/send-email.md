---
title: Send e-mail using SendGrid
description: Trigger an e-mail with a link to the saved form
feature: Adaptive Forms
type: Documentation
role: Developer
level: Beginner
version: Experience Manager as a Cloud Service
topic: Integrations
jira: KT-8474
duration: 25
---
# Send e-mail

After the form's data is saved in Azure Blob Storage, an e-mail with a link to the saved form is sent to the user. This e-mail is sent using SendGrid REST API.

The swagger file,form data model and the cloud services configuration needed to send e-mails are provided to you as part of the article assets.

You will have to create a SendGrid account,dynamic template that can ingest data captured in the adaptive form.


The following is the snippet of html code used in the dynamic template. The value of blobID parameter is passed using the form data model invoke service.

```html
You can  <a href='https://forms.enablementadobe.com/content/dam/formsanddocuments/azureportalstorage/creditcardapplication/jcr:content?wcmmode=disabled&ampguid={{blobID}}'>access your application here</a> and complete it.
```


