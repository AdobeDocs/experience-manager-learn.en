---
title: Updating cloud service project with latest archetype
description: Updating AEM Forms cloud service project with latest archetype
solution: Experience Manager
type: Documentation
role: Developer
level: Beginner, Intermediate
version: Cloud Service
topic: Development
feature: AEM Project Archetype
jira: KT-9534
exl-id: c2cd9c52-6f00-4cfe-a972-665093990e5d
duration: 85
---
# Migrating from old aem archetype 

To update your existing AEM Forms project with the latest maven archetype, you will have to manually copy your code/configurations etc., from the old project to the new project. 

The following steps were followed to migrate the project created using archetype 30 to archetype 33 project

## Create maven project using the latest archetype

* Open command prompt and navigate to c:\cloudmanager
* Create maven project using the latest archetype.
* Copy and paste the content of the [text file](assets/creating-maven-project.txt) in your command prompt window. You may have to change the DarchetypeVersion=33 depending on the [latest version](https://github.com/adobe/aem-project-archetype/releases). Archetype 33 includes new AEM Forms themes.
Since we are creating the new maven project in the cloudmanager folder which already has aem-banking-application project, you should change the **DartifactId** from aem-banking-application to something different. I have used aem-banking-application1 for this article.

>[!NOTE]
>
>If you deploy this new project as is the cloud service instance will not have HandleFormSubmission and the SubmitToAEMServlet. This is because every time you deploy a project using Cloud Manager anything under the `/apps` folder is deleted and overwritten.

## Copy your java code

Once your project is successfully created, you can then start copying code/configurations etc., from old project to this new project

* Copy the HandleFormSubmission servlet from ```C:\CloudManager\aem-banking-application\core\src\main\java\com\aem\bankingapplication\core\servlets``` 
to
```C:\CloudManager\aem-banking-application1\core\src\main\java\com\aem\bankingapplication\core\servlets```

* Copy the CustomSubmit from
```C:\CloudManager\aem-banking-application\ui.apps\src\main\content\jcr_root\apps\bankingapplication\SubmitToAEMServlet``` from aem-banking-application to aem-banking-application1 project

* import the new project into IntelliJ

* Update the filter.xml in the ui.apps module  of the aem-banking-application1 project to include the following line
```<filter root="/apps/bankingapplication/SubmitToAEMServlet"/>```

After you have copied all the code to your new project, you can push this project to cloud manager.

>[!NOTE]
>
>To sync the content(Adaptive Forms,Form Data Model,etc.,)into your new project you will have to create the appropriate folder structure in your IntelliJ project and then sync your IntelliJ project with your AEM instance using the Get command of the repo tool.
