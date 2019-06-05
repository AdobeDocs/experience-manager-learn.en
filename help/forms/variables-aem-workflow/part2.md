---
title: Variables in AEM Workflow[Part2]
seo-title: Variables in AEM Workflow[Part2]
description: Using variables of type xml,json,arraylist,document in aem workflow
seo-description: Using variables of type xml,json,arraylist,document in aem workflow
---
# Variables of type JSON in AEM Workflow

Starting with AEM Forms 6.5, we can now create variables of type JSON in AEM Workflow. Typically you will create variables of type JSON if you are submitting Adaptive Forms based on JSON schema to an AEM Workflow or you want to store the results of a Form Data Model Invoke operation. The following video walks you through the steps required to create and use a variable of type JSON in AEM workflow
>[!NOTE]
When you are creating a variable of type JSON to capture the submitted data in your workflow model, please do not associate the JSON schema with the variable. This is because when you submit JSON schema based Adaptive Form the submitted data is not compliant with the JSON schema. The JSON schema complaint data is enclosed in afData.afBoundData element.

>[!VIDEO](https://video.tv.adobe.com/v/26444?quality=12)

To get the assets working on your system, please follow the following steps:

* [Download and import the assets into AEM using package manager](assets/jsonandstringvariable.zip)
* [Explore the workflow model](http://localhost:4502/editor.html/conf/global/settings/workflow/models/jsonvariable.html) to understand the variables that are used in the workflow
* [Configure the Email Service](https://helpx.adobe.com/experience-manager/6-5/sites/administering/using/notification.html#ConfiguringtheMailService)
* [Open the Adaptive Form](http://localhost:4502/content/dam/formsanddocuments/afbasedonjson/jcr:content?wcmmode=disabled)
* Fill in the details and submit the form
