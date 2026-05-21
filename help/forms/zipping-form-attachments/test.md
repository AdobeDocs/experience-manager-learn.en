---
title: Test the solution - Steps needed to test the two approaches
description: Test the solution by adding attachments to the form and trigger the workflow to send the email.
feature: Adaptive Forms
version: Experience Manager 6.5
topic: Development
role: Developer
level: Beginner
kt: kt-8049
exl-id: ce9b9203-b44c-4a52-821c-ae76e93312d2
duration: 41
TQID: https://experienceleague.adobe.com/Z3UL0QT5KnSroyna4dDVS1Wv3LZaL3k6J4rD5WmMUU0
product_v2:
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
---
# Steps needed to test the two approaches

* Configure [Day CQ Mail Service](https://experienceleague.adobe.com/docs/experience-manager-65/administering/operations/notification.html?lang=en#configuring-the-mail-service) to send e-mails from AEM Forms server
* Deploy the [formattachments](assets/formattachments.formattachments.core-1.0-SNAPSHOT.jar) bundle using [felix web console](http://localhost:4502/system/console/bundles)

## Send zip file as an email attachment



* Deploy the [SendFormAttachmentsViaEmail workflow.](assets/zipped-form-attachments-model.zip) This workflow uses the send email component to send the zipped_attachments.zip file which is saved under the payload folder by the custom process step. Configure the senders' and recipients' email addresses according to your needs.
* Import the [sample form](assets/zip-form-attachments-form.zip) from [Forms And Document UI](http://localhost:4502/aem/forms.html/content/dam/formsanddocuments)
* [Preview the form](http://localhost:4502/content/dam/formsanddocuments/zippformattachments/jcr:content?wcmmode=disabled) and add a couple of attachments and submit the form.
* The workflow should get triggered and an email notification with the zip file should be sent.

## Send form attachments as individual files

* Deploy the [SendForm workflow.](assets/send-form-attachments-model.zip) This workflow uses send email component to send the form attachments as individual files. Configure the senders and recipients email address according to your needs.
* Import the [sample form](assets/send-list-attachments-form.zip) from [Forms And Document UI](http://localhost:4502/aem/forms.html/content/dam/formsanddocuments)
* [Preview the form](http://localhost:4502/content/dam/formsanddocuments/sendlistofattachments/jcr:content?wcmmode=disabled) and add a couple of attachments and submit the form.
* The workflow should get triggered and an email notification with the form attachments is sent.
