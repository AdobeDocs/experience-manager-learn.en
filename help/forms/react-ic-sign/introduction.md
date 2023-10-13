---
title: React app with AEM Forms and Acrobat Sign
description: Acrobat Sign and AEM Forms lets automate complex transactions and include legal e-signatures as part of a seamless digital experience.
feature: Adaptive Forms,Acrobat Sign
version: 6.4,6.5
topic: Development
role: Developer
level: Beginner
kt: 13099
last-substantial-update: 2023-04-13
exl-id: 64172af3-2905-4bc8-8311-68c2a70fb39e
---
# AEM Forms with Acrobat Sign Web Form


This tutorial walks you through the use case of generating an interactive communication document with the data submitted from the [React](https://react.dev/) app and presenting the generated document for signing using Acrobat Sign webform.

The following is the flow of the use case

* User fills out a form in React app. 
* The form data is submitted to an AEM Forms endpoint to generate interactive communications document.
* Create  Acrobat Sign widget url using the generated document.
* Present the widget url to the calling application for the user to sign the document. 

## Prerequisites

You will require the following for the use case to work:

* An AEM server with Forms add on package
* An [integration key for an Acrobat Sign application](https://helpx.adobe.com/sign/kb/how-to-create-an-integration-key.html)

## Next Steps

Write a [custom OSGi service to generate Interactive Communication Document](./create-ic-document.md) using documented API
