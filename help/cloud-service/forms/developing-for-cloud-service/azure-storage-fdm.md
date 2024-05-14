---
title: Pushing cloud services configuration and form data model to cloud instance
description: Create and push an Adaptive Form based on Azure storage form data model to the cloud instance.
solution: Experience Manager
type: Documentation
role: Developer
level: Beginner, Intermediate
version: Cloud Service
topic: Development
feature: Developer Tools
jira: KT-9006
exl-id: 77c00a35-43bf-485f-ac12-0fffb307dc16
duration: 45
---
# Include cloud services configuration in your project

Create a configuration container called 'FormTutorial' to hold your cloud services configuration
Create a cloud services configuration for Azure Storage called 'FormsCSAndAzureBlob' in the 'FormTutorial' container by providing the Azure storage account details and Azure access key.

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
>
>Now when you build and deploy your project using cloud manager, you will have to re-enter your Azure access key in the cloud services configuration. To avoid re-entering the access key, it is recommended to create context aware configuration using the environment variables as explained in the [next article](./context-aware-fdm.md)

## Next Steps

[Create context aware configuration](./context-aware-fdm.md)
