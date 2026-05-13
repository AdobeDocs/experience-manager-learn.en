---
title: Sending Email on Adaptive Form Submission
description: Send confirmation email on adaptive form submission using the send email component
feature: Adaptive Forms
doc-type: article
discoiquuid: 1187357f-2f36-4a04-b708-44bb9c174fb5
topic: Development
role: Developer
level: Beginner
exl-id: 19c5aeec-2893-4ada-b6df-b80c4be2468a
last-substantial-update: 2020-07-07T00:00:00.000Z
duration: 40
TQID: https://experienceleague.adobe.com/CV3baQ1cB9Wmr0vUau2Co751zjnmvuXLVdK7lksea7g
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
# Sending Email on Adaptive Form Submission {#sending-email-on-adaptive-form-submission}

One of the common actions is to send a confirmation email to the submitter on successful submission of Adaptive Form. To accomplish this we will select the "Send Email" as submit action.

You can use email template or just type in the body of the email as shown in this screenshot below.

Notice the syntax to insert form field values in the email.We also have the option to include form attachments in the email, by selecting the checkbox "include attachments" in the configuration properties.

When the Adaptive Form is submitted, the recipient will get email.

![SendEmail](assets/sendemailaction.gif)

## Configurations Needed {#configurations-needed}

You will have to configure Day CQ Mail service. This can be configured by pointing your browser to [Felix Configuration Manager](http://localhost:4502/system/console/configMgr)

The screenshot shows you the configuration properties for adobe mail server.

![mailservice](assets/mailservice.png)

To try this on your server follow these instructions:

* [Import the assets](assets/timeoffrequest.zip) associated with this article in AEM using the package manager.

* Open the [TimeOffRequestForm](http://localhost:4502/content/dam/formsanddocuments/helpx/timeoffrequestform/jcr:content?wcmmode=disabled).

* Fill in the details.Make sure you provide a valid email address in the email field.

* Submit the form.
