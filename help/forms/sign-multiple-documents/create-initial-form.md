---
title: Create the Initial Form to Trigger the Process
description: Create initial form to trigger the e-mail notification to start the process of signing.
feature: Adaptive Forms
version: Experience Manager 6.4, Experience Manager 6.5
topic: Development
role: User
level: Intermediate
jira: KT-6892
thumbnail: 6892.jpg
exl-id: d7c55dc8-d886-4629-bb50-d927308d12e3
duration: 35
TQID: https://experienceleague.adobe.com/jlIx4Z1fawOXJB02CWAa1ULx5NYDEifl64og1MblYaE
product_v2:
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
---
# Create initial form

The initial form (Refinance Form) is used for signing multiple forms by triggering the **Sign Multiple Forms** AEM workflow. You can enter values of your choice but ensure the following fields are added to the form.

| Field Type | Name | Purpose | Hidden | Default Value |
|--- |--- |---|--- |--- |
| TextField | signed | To indicate the signing status | Y | N |
| TextField | guid | To uniquely identify form | Y | 3889 |
| TextField | customerName | To capture customers name | N | |
| TextField | customerEmail | Customer email to send notification | N | |
| CheckBox| formsToSign | The items identify the forms in the package | N | |

The initial form needs to be configure to trigger an AEM workflow called **signmultipleforms**
Make sure the Data File Path is set to **Data.xml**. This is very important as the sample code looks for a file called Data.xml in the payload the process the form submission.

## Assets

The initial form (Refinance Form) can be [downloaded from here](assets/refinance-form.zip)

## Next Steps

[Create forms to be used for signing](./create-forms-for-signing.md)
