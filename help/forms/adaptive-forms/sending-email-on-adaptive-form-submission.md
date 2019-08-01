---
title: Sending Email on Adaptive Form Submission
seo-title: Sending Email on Adaptive Form Submission
description: Send confirmation email on adaptive form submission using the send email component
seo-description: Send confirmation email on adaptive form submission using the send email component
uuid: 6c9549ba-cb56-4d69-902c-45272a8fd17e
sub-product: forms
feature: adaptive-forms
topics: authoring, integrations
audience: developer
doc-type: article
activity: use
discoiquuid: 1187357f-2f36-4a04-b708-44bb9c174fb5
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
