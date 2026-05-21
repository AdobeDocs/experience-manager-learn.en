---
title: AEM Forms with Marketo(Part 2)
description: Tutorial to integrate AEM Forms with Marketo using AEM Forms Form Data Model.
feature: Adaptive Forms, Form Data Model
version: Experience Manager 6.4, Experience Manager 6.5
topic: Integrations, Development
role: Developer
level: Experienced
badgeIntegration: label="Integration" type="positive"
badgeVersions: label="AEM Forms 6.5" before-title="false"
exl-id: f8ba3d5c-0b9f-4eb7-8609-3e540341d5c2
duration: 137
TQID: https://experienceleague.adobe.com/VcmPiMzYTL-hSfJZkJ-AkB4fWaVc0Fe0VoR9q1c2D3o
product_v2:
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: a01bfd36-4ab8-4bf8-9dc0-5b45b890552e
    internal-label: APIs
  - id: a1df6763-63b5-45b4-8c8a-155a692a2b3e
    internal-label: Integrations
  - id: ae478996-b206-4712-9b0c-dc78a2644453
    internal-label: Integrations
  - id: f013e6ab-27b8-4645-b5a7-31ffa474d04f
    internal-label: APIs
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
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
