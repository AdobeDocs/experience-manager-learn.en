---
title: Integrate AEM Forms Cloud Service and Marketo(Part 2)
description: Learn how to integrate AEM Forms and Marketo using AEM Forms Form Data Model.
feature: Form Data Model,Integration
version: Cloud Service
topic: Integrations, Development
role: Developer
level: Experienced
badgeIntegration: label="Integration" type="positive"
badgeVersions: label="AEM Forms as a Cloud Service" before-title="false"
last-substantial-update: 2024-07-24
jira: KT-15876
---
# Create Data Source

Marketo's REST APIs are authenticated with 2-legged OAuth 2.0. We can easily create a data source using the swagger file downloaded in the previous step 

## Create configuration container

* Login to AEM.
* Click on the tools menu and then **Configuration Browser** as shown below

* ![tools menu](assets/datasource3.png)

* Click on **Create** and provide a meaningful name as shown below. Make sure you select the Cloud Configurations option as shown below

* ![configuration container](assets/datasource4.png)

## Create cloud services

* Navigate to the tools menu and then click on cloud  services -> Data Sources

* ![cloud-services](assets/datasource5.png)

* Select the configuration container created in the earlier step and click on **Create** to create a new data source.Provide a meaningful name and select RESTful service from the Service Type drop down list and click **Next**
* ![new-data-source](assets/datasource6.png)

* Upload the swagger file and specify the Grant type, Client Id,Client Secret and Access Token url specific to your Marketo instance as shown in the screen shot below.

* Test the connection and if the connection is successful make sure you click on the blue **Create** button to finish the process of creating the data source.

* ![data-source-config](assets/datasource1.png)


## Next Steps

[Create Form Data Model](./part3.md)
