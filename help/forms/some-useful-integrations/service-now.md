---
title: Integrating with Service Now
description: Create and display all the incidents using form data model.
feature: Adaptive Forms
version: 6.4,6.5
kt: 9957
topic: Development
role: Developer
level: Intermediate

---
# Integrate AEM Forms with servicenow

Create and display incident in ServiceNow using Form Data Model in AEM Forms.

## Prerequisites

* ServiceNow account.
* Familiar with [creating data sources](https://experienceleague.adobe.com/docs/experience-manager-learn/forms/ic-web-channel-tutorial/parttwo.html)
* Familiar with [Form Data Model](https://experienceleague.adobe.com/docs/experience-manager-65/forms/form-data-model/create-form-data-models.html)

## Sample Assets

The sample assets provided with this article include the following
* Cloud service configuration
 * Swagger files to create an incident and fetch all   incidents
 * Form Data Model based on the swagger files
 * Adaptive Form to create and list servicenow incidents

## Deploy the assets on your server

* Download the [sample assets](assets/service-now.zip)
* Import the assets into AEM using [package manager](http://localhost:4502/crx/packmgr/index.jsp)
* Edit the [CreateIncident cloud service configuration](http://localhost:4502/mnt/overlay/fd/fdm/gui/components/admin/fdmcloudservice/properties.html?item=%2Fconf%2F9957%2Fsettings%2Fcloudconfigs%2Ffdm%2Fcreateincident)to match your ServiceNow instance.
* Edit the [GetAllIncidents cloud service configuration](http://localhost:4502/mnt/overlay/fd/fdm/gui/components/admin/fdmcloudservice/properties.html?item=%2Fconf%2F9957%2Fsettings%2Fcloudconfigs%2Ffdm%2Fgetallincidents) to match your ServiceNow instance


## Test the integration

* [Open the Adaptive Form](http://localhost:4502/content/dam/formsanddocuments/create-incident-in-service-now/jcr:content?wcmmode=disabled)
* Enter some values in the description and comments field and click Create Incident button
* The incident Id of the newly create incident should get populated in the text field and the table below should list all the incidents.

