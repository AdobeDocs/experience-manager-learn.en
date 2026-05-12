---
title: React app with AEM Forms and Acrobat Sign
description: Acrobat Sign and AEM Forms lets automate complex transactions and include legal e-signatures as part of a seamless digital experience.
feature: Adaptive Forms,Acrobat Sign
version: Experience Manager 6.4, Experience Manager 6.5
topic: Development
role: Developer
level: Beginner
jira: KT-13099
last-substantial-update: 2023-04-13T00:00:00.000Z
exl-id: 64172af3-2905-4bc8-8311-68c2a70fb39e
duration: 31
TQID: https://experienceleague.adobe.com/FG9M-sEMI6nD3jz5jm7AVHBbH13fs6a3afGCYlSc4vM
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
