---
title: Test Solution With Personalized PDF
description: Learn how to test solutions that deliver personalized PDFs via interactive communication using Adobe Journey Optimizer.
version: Experience Manager as a Cloud Service
feature: Interactive Communication
role: User
level: Intermediate
doc-type: Technical Video
duration: 42
last-substantial-update: 2026-06-15
jira: KT-21618
---

# Deploy and Test the solution


To deploy this solution, use the provided [server.js](https://github.com/gbedekar489/generate-and-send-ic-document) file as the entry point for your Node.js application. The sample application exposes an endpoint that is invoked by the custom action configured in Adobe Journey Optimizer.

## Prerequisites

Before deploying the application, ensure that you have:

* A valid **SendGrid account** with permission to send emails.
* A verified sender email address configured in SendGrid.
* Access to Adobe Experience Manager Forms services and a valid bearer token.
* A Node.js runtime environment for hosting the sample application.

### Environment Variables

Configure the following environment variables before starting the application:

```javascript
const SENDGRID_API_KEY = process.env.SEND_GRID_API_KEY;
const SENDGRID_FROM = process.env.SENDGRID_FROM;
const AEM_BEARER = process.env.AEM_BEARER;
```

* **SENDGRID_API_KEY** – API key used to authenticate with SendGrid for email delivery.
* **SENDGRID_FROM** – Verified sender email address used for outgoing communications.
* **AEM_BEARER** – Bearer token used to authenticate requests to Adobe Experience Manager services.

### Adobe Journey Optimizer Integration

Once deployed, the endpoint exposed by the Node.js application can be referenced in an Adobe Journey Optimizer custom action. When the custom action is invoked during a journey, the application generates a personalized PDF communication and delivers it to the recipient using SendGrid.



Test the solution by Filling out an adaptive form with the required details, including an email address and the cloud solution of interest. Ensure that the information corresponds to a new customer profile in Adobe Experience Platform. This triggers a journey in Adobe Journey Optimizer, which creates a personalized interactive communication. A PDF version of this communication is then sent to the provided email address.


The video demonstrates the end-user experience for this use case.

>[!VIDEO](https://video.tv.adobe.com/v/3492360/?learn=on&enablevpops)

