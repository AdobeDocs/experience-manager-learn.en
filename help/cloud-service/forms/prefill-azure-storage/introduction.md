---
title: Implement save and resume functionality for an adaptive form
description: Learn how to store and retrieve adaptive form data from Azure storage account.
feature: Adaptive Forms
type: Documentation
role: Developer
level: Beginner
version: Cloud Service
topic: Integrations
jira: KT-13717
exl-id: b40b0ef4-efa9-400e-82d8-aa0c7feb7be4
duration: 28
---
# Introduction

In this tutorial we will implement a simple use case of allowing the form fillers to save and resume the form filling process. The flow of the use case is as follows

* User starts filling out an adaptive form.
* User save's the form and would like to continue the form filling at a later date.
* User gets an e-mail notification with an link to the saved form.

## Pre-requisites

* Experience with AEM Forms CS especially creating Form Data Model's.
* Experience in deploying code using cloud manager.
* Access to cloud ready instance of AEM Forms CS.

To implement the above use case in AEM Forms CS, you will need the following

* [AEM Forms CS cloud ready instance](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/forms/developing-for-cloud-service/intellij-and-aem-sync.html?lang=en#set-up-aem-author-instance)
* [Azure portal account](https://portal.azure.com/)
* [SendGrid Account](https://sendgrid.com/)

### Next Steps

[Create Page Component](./page-component.md)
