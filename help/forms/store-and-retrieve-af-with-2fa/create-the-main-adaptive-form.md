---
title: Create the main adaptive form
description: Create the adaptive forms to capture applicant information and adaptive form to retrieve the saved adaptive form
feature: Adaptive Forms
type: Tutorial
version: Experience Manager 6.4, Experience Manager 6.5
jira: KT-6552
thumbnail: 6552.jpg
topic: Development
role: User
level: Beginner
exl-id: 73de0ac4-ada6-4b8e-90a8-33b976032135
duration: 41
TQID: https://experienceleague.adobe.com/UOOgXv6KmnGoMOShZ6FgKZsu1vkeLueMYnJ4YyBqrxs
product_v2:
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
level_v2:
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
---
# Create the main adaptive form

The form **StoreAFWithAttachments** is the main adaptive form. This adaptive form is the entry point to the use case. In this form user details including mobile number are captured. This form also has the ability to add some attachments. When the Save and Exit button is clicked the server side code is executed to store the form data in the database and a unique application id is generated and presented to the user for safe keeping. This application id is used to retrieve the mobile number associated with the application.

![main application form](assets/6552.JPG)

This form is associated with **bootboxjs540,storeAFWithAttachments** client libraries created earlier in the course and an AEM workflow which gets triggered on form submission.


* The sample forms are based on [custom adaptive form template](assets/custom-template-with-page-component.zip) that needs to be imported into AEM for the sample forms to render correctly.

* The completed [StoreAfWithAttachments Form](assets/store-af-with-attachments-form.zip) can be downloaded and imported into your AEM instance.

* The [AEM workflow associated with this form](assets/workflow-model-store-af-with-attachments.zip) need to be imported into your AEM instance for the form to work.


## Next steps

[Create the form retrieving saved form](./retrieve-saved-form.md)