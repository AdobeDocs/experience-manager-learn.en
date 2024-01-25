---
title: Create database tables
description: Create database to be used by form data model
feature: Adaptive Forms
version: 6.4,6.5
jira: KT-5811
thumbnail: kt-5811.jpg
topic: Development
role: Developer
level: Beginner
exl-id: 1136244a-c3e6-45f6-8af8-eb3c100f838e
duration: 28
---
# Create Database Tables

Form data model can be based on RDBMS, RESTfull, SOAP or OData sources. This course's focus is on pre-filing Adaptive Form using form data model backed by RDBMS data source. For the purpose of this tutorial MYSQL database was used. We created the following two tables to demonstrate the use case

* **newhire** table - This table stores the newhire information

  ![newhire](assets/newhire-table.png)


* **beneficiaries** table - This stores newhire beneficiaries

  ![beneficiaries](assets/beneficiaries-table.png)

You can import the [sql file](assets/db-schema.sql) using MySQL workbench to create to tables with some sample data.

## Next Steps

[Configure Form Data Model](./configuring-form-data-model.md)
