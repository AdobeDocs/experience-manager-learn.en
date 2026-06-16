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

# Test the solution

Test the solution by Filling out an adaptive form with the required details, including an email address and the cloud solution of interest. Ensure that the information corresponds to a new customer profile in Adobe Experience Platform. This triggers a journey in Adobe Journey Optimizer, which creates a personalized interactive communication. A PDF version of this communication is then sent to the provided email address.

Refer to the [server.js](https://github.com/gbedekar489/generate-and-send-ic-document) file in the GitHub repository for the complete sample implementation. This Node.js application exposes a REST endpoint that is invoked from the Adobe Journey Optimizer (AJO) journey. When the endpoint is called, the application invokes the AEM Forms Document Generation API and generates a personalized document. After the document is generated, the application uses the SendGrid API to send the document as an email attachment to the intended recipient. Review the server.js file to understand the end-to-end integration between AJO, AEM Forms Document Generation, and SendGrid email delivery.

Watch the embedded video below for a detailed walkthrough.

>[!VIDEO](https://video.tv.adobe.com/v/3492360/?learn=on&enablevpops)

