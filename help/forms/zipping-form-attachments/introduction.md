---
title: Send adaptive form attachments

description: Zip adaptive form attachments and send them using send email component


feature: adaptive forms

topics: adaptive forms
audience: developer
doc-type: article
activity: setup
version: 6.5
topic: Development
role: Developer
level: Beginner
kt: kt-8049
---

# Introduction



Common use case is to zip the adaptive form attachments and send using send email component in an AEM workflow. To accomplish the use case a custom workflow process step was written. In this custom process step a zip file with the form attachments in created and stored under the payload folder in a file named *zipped_attachments.zip*

![send-form-attachments](assets/send-form-attachments.JPG)


