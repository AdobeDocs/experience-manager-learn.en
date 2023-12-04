---
title: Deploy the sample assets on your server
description: Test the save as draft functionality for Interactive Communications
feature: Interactive Communication
doc-type: article
version: 6.5
topic: Development
role: Developer
level: Intermediate
jira: KT-10208
exl-id: 9053ee29-436a-439a-b592-c3fef9852ea4
duration: 46
---
# Deploy the sample assets on your server

Please follow the below instructions to get this functionality working on your AEM Server

* [Create the database schema](assets/icdrafts.sql)
* [Import the client library](assets/icdrafts.zip)
* [Import the Adaptive Form](assets/SavedDraftsAdaptiveForm.zip)
* Create data source called _SaveAndContinue_

![Create Data Source](assets/data-source.png)

|Property Name|Property Value   |
|---|---|
|Datasource Name|SaveAndContinue|
|JDBC driver class|com.mysql.cj.jdbc.Driver|
|JDBC Connection URL|jdbc:mysql://localhost:3306/aemformstutorial?autoReconnect=true&useSSL=false&characterEncoding=utf8&useUnicode=true|

* [Deploy the icdrafts bundle](assets/icdrafts.icdrafts.core-1.0-SNAPSHOT.jar)
* Make sure you _Enable Save Using CCRDocumentInstanceService_ in OSGI config as shown below
![Enable Drafts](assets/enable-drafts.png)
* Open any Interactive Communication. Click the Save as Draft to save
* [View Saved Drafts](http://localhost:4502/content/dam/formsanddocuments/saveddrafts/jcr:content?wcmmode=disabled)

>[!NOTE]
>The xml files are stored in the root folder of your AEM server installation. The eclipse project >is provided to you to customize the solution as per your requirements.

The eclipse project with sample implementation can be [downloaded from here](assets/icdrafts-eclipse-project.zip)
