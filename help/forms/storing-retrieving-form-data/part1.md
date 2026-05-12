---
title: Storing and Retrieving Form Data from MySQL Database - Configure Data Source
description: Multi-Part tutorial to walk you through the steps involved in storing and retrieving form data
version: Experience Manager 6.4, Experience Manager 6.5
feature: Adaptive Forms
topic: Development
role: Developer
level: Experienced
exl-id: dccca658-3373-4de2-8589-21ccba2b7ba6
duration: 36
TQID: https://experienceleague.adobe.com/w2V8M2Co7Jske-MjI1vECnogpHa2AqwRukBIxKQLvHk
product_v2:
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
---
# Configure Data Source

There are many ways with which AEM enables integration with external database. One of the most common & standard practice of database integration is by using Apache Sling Connection Pooled DataSource configuration properties through the [configMgr](http://localhost:4502/system/console/configMgr).
The first step is to download and deploy the appropriate [MySql drivers](https://mvnrepository.com/artifact/mysql/mysql-connector-java) in AEM.
Create Apache Sling Connection Pooled DataSource and provide the properties as specified in the screen shot below. The database schema is provided to you as part of this tutorial assets.

![data-source](assets/save-continue.PNG)

Database has one table called formdata with the 3 columns as shown in the screen-shot below.

![data-base](assets/data-base-tables.PNG) 

The sql file to create the schema can be [downloaded from here](assets/form-data-db.sql). You will need to import this file using MySql workbench to create the schema and the table.

>[!NOTE]
>Please make sure you name your datasource **SaveAndContinue**. The sample code uses the name to connect to the database.

| Property Name| Value |
| ------------------------|---------------------------------------|
| Datasource Name| `SaveAndContinue` |
| JDBC Driver Class| `com.mysql.cj.jdbc.Driver` |
| JDBC connection uri| `jdbc:mysql://localhost:3306/aemformstutorial` |
