---
title: Store Adaptive Form data in Azure Storage
description: Create and configure Adaptive Form to store data in Azure Storage
feature: Adaptive Forms
type: Documentation
role: Developer
level: Beginner
version: Cloud Service
topic: Integrations
thumbnail: 335423.jpg
exl-id: 0b543c6b-9cfd-4fac-b8d0-33153c036f4b
duration: 64
---
# Putting it all together

We now have all the required configurations/integrations required for the use case. The last step is to create an adaptive form based on the form data model backed by Azure Storage.

Create and adaptive form and make sure it is based on the correct adaptive form template. This will ensure our custom code associated with the template will get executed every time an adaptive form is rendered.

## Sample Adaptive Form

In the form we have added 2 hidden fields

* Blob ID - This field is populated with a GUID when the field is initialized. The value of this field is used as blobid to uniquely identify blob storage of the form data.This blobid is used to identify the form data.
* Blob ID Returned - This field is populated with the result of the service call to store data in Azure Storage. This value is going to be the same as Blob ID from the previous step.

The form has the following business rules

* Save Form button is displayed when the user enters e-mail address. On the click of Save Form button the form data is stored in Azure Storage using the invoke service operation of the form data model.
* The BlobID returned by the invoke service is stored in the Blob ID field. When this value changes an e-mail is sent to the applicant using SendGrid. The e-mail will contain the link to open the partially completed form identified by the Blob ID.
* A confirmation text is shown to the user when the data is successfully stored in Azure Storage

### Next Steps

[Deploy the sample assets](./deploy-sample-assets.md)
