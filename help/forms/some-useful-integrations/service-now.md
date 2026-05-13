---
title: Integrating with [!DNL ServiceNow]
description: Create and display all the incidents using form data model.
feature: Adaptive Forms
version: Experience Manager 6.4, Experience Manager 6.5
jira: KT-9957
topic: Development
role: Developer
level: Intermediate
exl-id: 93a177b0-7852-44da-89cc-836d127be4e7
last-substantial-update: 2022-07-07T00:00:00.000Z
duration: 47
TQID: https://experienceleague.adobe.com/aSApRnMZm7XvbaueXEAyZ2j6YCO3CJDLIJCRO2IM-Vw
product_v2:
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: a1df6763-63b5-45b4-8c8a-155a692a2b3e
    internal-label: Integrations
  - id: ae478996-b206-4712-9b0c-dc78a2644453
    internal-label: Integrations
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
---
# Integrate AEM Forms with [!DNL ServiceNow]

Create and display incident in [!DNL ServiceNow] using Form Data Model in AEM Forms.

## Prerequisites

* [!DNL ServiceNow] account.
* Familiar with [creating data sources](https://experienceleague.adobe.com/docs/experience-manager-learn/forms/ic-web-channel-tutorial/parttwo.html)
* Familiar with [Form Data Model](https://experienceleague.adobe.com/docs/experience-manager-65/forms/form-data-model/create-form-data-models.html)

## Sample Assets

The sample assets provided with this article include the following

* Cloud service configuration
* Swagger files to create an incident and fetch all   incidents
* Form Data Model based on the swagger files
* Adaptive Form to create and list [!DNL ServiceNow] incidents

## Deploy the assets on your server

* Download the [sample assets](assets/service-now.zip)
* Import the assets into AEM using [package manager](http://localhost:4502/crx/packmgr/index.jsp)
* The swagger file used for this integration is located under the ```/conf/9957/settings/cloudconfigs/fdm``` folder in crx repository
* Edit the [CreateIncident cloud service configuration](http://localhost:4502/mnt/overlay/fd/fdm/gui/components/admin/fdmcloudservice/properties.html?item=%2Fconf%2F9957%2Fsettings%2Fcloudconfigs%2Ffdm%2Fcreateincident)to match your ServiceNow instance.
* Edit the [GetAllIncidents cloud service configuration](http://localhost:4502/mnt/overlay/fd/fdm/gui/components/admin/fdmcloudservice/properties.html?item=%2Fconf%2F9957%2Fsettings%2Fcloudconfigs%2Ffdm%2Fgetallincidents) to match your ServiceNow instance. You will need to change the host,username and password to match your ServiceNow instance credentials.

## Access ServiceNow instance credentials

* Click on your user profile
 ![click on user profile](assets/snow-1.png)
 
* Click on Manage instance Password
* The instance details is shown as below
![instance details](assets/snow-3.png)

## Test the integration

* [Open the Adaptive Form](http://localhost:4502/content/dam/formsanddocuments/create-incident-in-service-now/jcr:content?wcmmode=disabled)
* Enter some values in the description and comments field and click Create Incident button
* The incident Id of the newly create incident should get populated in the text field and the table below should list all the incidents.
