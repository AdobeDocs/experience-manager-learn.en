---
title: Send adaptive form attachments
description: Send adaptive form attachments using send email component
feature: Adaptive Forms
version: Experience Manager 6.5
topic: Development
role: Developer
level: Beginner
kt: kt-8049
exl-id: bd9e1fc1-2fc7-452c-9a4a-2e16f6821760
last-substantial-update: 2020-07-07
duration: 28
---
# Introduction



Common use case is to send the adaptive form attachments using send email component in an AEM workflow. 
Customers typically would zip the form attachments or send the attachments as individual files using send email component.

## Send the form attachments in a zip file

To accomplish the use case a custom workflow process step was written. In this custom process step a zip file with the form attachments in created and stored under the payload folder in a file named *zipped_attachments.zip*

![send-form-attachments](assets/send-form-attachments.JPG)

## Send the form attachments individually

To accomplish this use case a custom workflow process step was written. In this custom process step we populate workflow variables of type ArrayList of Documents and ArrayList of Strings.

![send-list-of-documents](assets/send-list-of-documents.JPG)

## Next Steps

[Zip Form Attachments](./custom-process-step.md)
