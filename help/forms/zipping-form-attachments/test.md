---
title: Test the solution
description: Test the solution by adding attachments to the form and trigger the workflow to send the email.
sub-product: forms
feature: Workflow
topics: adaptive forms
audience: developer
doc-type: article
activity: develop
version: 6.5
topic: Development
role: Developer
level: Beginner
kt: kt-8049
---

# Test the solution


* Configure [Day CQ Mail Service](https://experienceleague.adobe.com/docs/experience-manager-65/administering/operations/notification.html?lang=en#configuring-the-mail-service) to send e-mails from AEM Forms server
* Deploy the [formattachments](assets/formattachments.formattachments.core-1.0-SNAPSHOT.jar) bundle using [felix web console](http://localhost:4502/system/console/bundles)
* Deploy the [SendFormAttachmentsViaEmail workflow.](assets/zipped-form-attachments-model.zip) This workflow uses send email component to send the zipped_attachments.zip file which is saved under the payload folder by the custom process step. Configure the senders and recipients email address according to your needs.
* Import the [sample form](assets/zip-form-attachments-form.zip) from [Forms And Document UI](http://localhost:4502/aem/forms.html/content/dam/formsanddocuments)
* [Preview the form](http://localhost:4502/content/dam/formsanddocuments/zippformattachments/jcr:content?wcmmode=disabled) and add a couple of attachments and submit the form.
* The workflow should get triggered and an email notification with the zip file should be sent.

