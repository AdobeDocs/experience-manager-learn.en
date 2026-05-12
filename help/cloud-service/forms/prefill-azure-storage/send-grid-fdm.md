---
title: Send e-mail using SendGrid
description: Trigger an e-mail with a link to the saved form
feature: Adaptive Forms
type: Documentation
role: Developer
level: Beginner
version: Experience Manager as a Cloud Service
topic: Integrations
jira: KT-13717
exl-id: 4b2d1e50-9fa1-4934-820b-7dae984cee00
duration: 37
TQID: https://experienceleague.adobe.com/3D3UMNFyX8MTpxwhnKq9-5NM0GxNRKAsmuQzQg428e8
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: ae478996-b206-4712-9b0c-dc78a2644453
    internal-label: Integrations
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
topic_v2:
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
    internal-label: Data integration
---
# Integrate with SendGrid

AEM Forms Data Integration allows configuring and connecting disparate data sources with AEM Forms. It provides an intuitive user interface to create a unified data representation schema of business entities and services across connected data sources.

We have used SendGrid API to send e-mails using dynamic template. It is assumed that you are familiar with SendGrid API for sending e-mails using dynamic templates. A swagger file to describe to API has been provided to you as part of this tutorial.

## Create the integration

Please follow the following steps to create the integration between AEM Forms and SendGrid

* Create a RESTful data source using the [swagger file](./assets/SendGridWithDynamicTemplate.yaml). [Follow this video for  detailed instructions](https://experienceleague.adobe.com/docs/experience-manager-learn/forms/ic-web-channel-tutorial/parttwo.html) on creating data sources in AEM Forms
* Create Form Data Model based on the data source created in the earlier step.[Follow the detailed documentation](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/create-form-data-models.html) on creating Form Data Model.

The form data model created for this tutorial is included as part of the article assets.

### Next Steps

[Create Azure Storage Integration](./create-fdm.md)
