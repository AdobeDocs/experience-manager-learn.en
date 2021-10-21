---
title: Pushing cloud services configuration and form data model to cloud instance
description: Create and push an Adaptive Form based on Azure storage form data model to the cloud instance.
solution: Experience Manager
type: Documentation
role: Developer
level: Beginner, Intermediate
version: cloud-service
topic: Development
kt: 9006
---

# Include cloud services configuration in your project

Create a configuration container called 'FormsTutorial' to hold your cloud services configuration
Create a cloud services configuration for Azure Storage called 'Store Form Submissions in Azure' in the 'FormsTutorial' container. Provide the Azure storage account details and the account key

Open your AEM project in IntelliJ. Make sure you add the folder FormTutorial as shown below in the ui.content project
![cloud-services-configuration](assets/cloud-services-configuration.png)

Make sure you add the following entry in the ui.content project's filter.xml

``` xml
<filter root="/conf/FormTutorial" mode="replace"/>
```

![filter-xml](assets/ui-content-filter.png)

## Include form data model in your project

Create form data model based on the cloud services configuration that your created in the earlier step. To include the form data model in your project create the appropriate folder structure in your AEM project in intelliJ. For example my form data model is in a folder called registrations
![fdm-content](assets/ui-content-fdm.png)

Include the appropriate entry in the ui.content project's filter.xml

``` xml
<filter root="/content/dam/formsanddocuments-fdm/registrations" mode="replace"/>
```


>[!NOTE]

>Now when you build and deploy your project, the project will have the form data model based on the cloud services configuration available in your cloud instance





