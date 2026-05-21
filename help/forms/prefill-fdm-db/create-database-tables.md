---
title: Create database tables
description: Create database to be used by form data model
feature: Adaptive Forms
version: Experience Manager 6.4, Experience Manager 6.5
jira: KT-5811
thumbnail: kt-5811.jpg
topic: Development
role: Developer
level: Beginner
exl-id: 1136244a-c3e6-45f6-8af8-eb3c100f838e
duration: 21
TQID: https://experienceleague.adobe.com/NoDD08lZQm-pSEu8JzQ2emBZOX2T4N8PuCxX-qPD7oQ
product_v2:
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
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
