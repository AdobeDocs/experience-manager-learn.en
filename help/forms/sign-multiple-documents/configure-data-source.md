---
title: Configure AEM Data Source
description: Configure MySQL backed data source to store and retrieve form data
feature: Adaptive Forms
topic: Development
role: Developer
level: Beginner
version: 6.4,6.5
jira: KT-6899
thumbnail: 6899.jpg
exl-id: 2e851ae5-6caa-42e3-8af2-090766a6f36a
duration: 53
---
# Configure data source

There are many ways with which AEM enables integration with an external database. One of the most common ways to integrate a database is by using Apache Sling Connection Pooled DataSource configuration properties through the [configMgr](http://localhost:4502/system/console/configMgr).
The first step is to download and deploy the appropriate [MySql drivers](https://mvnrepository.com/artifact/mysql/mysql-connector-java) in AEM.
Create Apache Sling Connection Pooled DataSource and provide the properties as specified in the screen shot below. The database schema is provided to you as part of this tutorial assets.

![data-source](assets/data-source.PNG)

Database has one table called formdata with the 3 columns as shown in the screen-shot below.

![data-base](assets/data-base.PNG) 


>[!NOTE]
>Please make sure you name your datasource **aemformstutorial**. The sample code uses the name to connect to the database.

| Property Name| Value |
| ------------------------|--------------------------------------- |
| Datasource Name| `SaveAndContinue` |
| JDBC Driver Class| `com.mysql.cj.jdbc.Driver` |
| JDBC connection uri| `jdbc:mysql://localhost:3306/aemformstutorial` |

## Assets

The SQL file to create the schema can be [downloaded from here](assets/sign-multiple-forms.sql). You will need to import this file using MySql workbench to create the schema and the table.

## Next Steps

[Create an OSGi service to store and fetch data in database](./create-osgi-service.md)
