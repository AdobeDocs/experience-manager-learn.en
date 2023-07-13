---
title: Integrate AEM Forms with SendGrid
description: Leverage SengGrid cloud-based email delivery platform using AEM Forms.
feature: Adaptive Forms
version: 6.4,6.5
kt: 13605
topic: Development
role: Developer
level: Intermediate
last-substantial-update: 2023-07-14
---
# Integrate AEM Forms with SendGrid

Welcome to this technical guide, where we will explore the process of sending emails with SendGrid dynamic templates from AEM Forms. This guide aims to provide you with a clear understanding of how to leverage dynamic templates to personalize your email content effectively.

Dynamic templates allow you to create email templates that can display different content to recipients based on the data captured in the adaptive form. By utilizing personalization variables, you can deliver targeted and customized email experiences that resonate with your audience.

Furthermore, we will delve into the use of the Swagger file, which enables you to further personalize your emails by including the customer's name and email address, as well as selecting the appropriate dynamic email template.

Follow the step-by-step instructions in this document to harness the power of SendGrid dynamic templates and AEM Forms, and elevate your email communications to new levels of engagement and relevance. Let's begin!

## Prerequisites

Before you proceed with sending emails using SendGrid dynamic templates from AEM Forms, ensure you have met the following prerequisites:

1. **SendGrid Account**: Sign up for a SendGrid account at [https://sendgrid.com](https://sendgrid.com) to access their email delivery services. You will need the account credentials to integrate SendGrid with AEM Forms.
1. **Familiarity with Creating Data Sources**: Have a working knowledge of creating data sources in AEM Forms. If needed, refer to the documentation on [creating data sources](https://experienceleague.adobe.com/docs/experience-manager-learn/forms/ic-web-channel-tutorial/parttwo.html) for detailed instructions.
1. **Familiarity with Form Data Model**: Understand the concept of the Form Data Model in AEM Forms. If required, review the documentation on [creating form data models](https://experienceleague.adobe.com/docs/experience-manager-65/forms/form-data-model/create-form-data-models.html) to ensure you have the necessary understanding.

By meeting these prerequisites, you will be equipped with the essential knowledge and resources to effectively send emails using SendGrid dynamic templates from AEM Forms.

## Sample assets

The sample assets provided with this article include:

* **[Swagger file](assets/SendGridWithDynamicTemplate.yaml)**: This file allows you to send emails using a dynamic email template. It provides the necessary specifications and configurations to integrate with SendGrid and AEM Forms for seamless email delivery.

Feel free to utilize the provided Swagger file as a reference or starting point for implementing email functionality with dynamic templates.
 
## Testing instructions

To test the functionality described in this guide, follow these steps:

1. Download the [swagger file](assets/SendGridWithDynamicTemplate.yaml) provided in the assets folder.
2. Create a Restful data source using the downloaded swagger file and your SendGrid credentials.
3. Create a Form Data Model based on the Restful data source.
4. Invoke the `mail/send` POST operation of the Form Data Model according to your requirements. For example, you can trigger the email on button click or include it as part of your AEM Forms workflow.

The sample payload for the service is as follows. Replace the placeholder values with your own data:

```json
{
    "sendgridpayload": {
        "from": {
            "email": "gs@xyz.com"
        },
        "personalizations": [{
            "to": [{
                "email": "johndoe@xyz.com"
            }],
            "dynamic_template_data": {
                "customerName": "John Doe"
            }
        }],
        "template_id": "d-72aau292a3bd60b5300c"
    }
}
```

Ensure that the `template_id` corresponds to the ID of your SendGrid dynamic email template, and the email addresses are valid and verified by SendGrid. The values in the `personalizations` section allow you to personalize the email using the user-entered data from the adaptive form.

By following these steps and customizing the provided payload, you can effectively test the integration of SendGrid dynamic templates with AEM Forms.

