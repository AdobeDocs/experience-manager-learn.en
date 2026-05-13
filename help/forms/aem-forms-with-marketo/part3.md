---
title: AEM Forms with Marketo(Part 3)
description: Tutorial to integrate AEM Forms with Marketo using AEM Forms Form Data Model.
feature: Adaptive Forms, Form Data Model
version: Experience Manager 6.4, Experience Manager 6.5
topic: Integrations, Development
role: Developer
level: Experienced
badgeIntegration: label="Integration" type="positive"
badgeVersions: label="AEM Forms 6.5" before-title="false"
exl-id: 7096340b-8ccf-4f5e-b264-9157232e96ba
duration: 78
TQID: https://experienceleague.adobe.com/YFcMQI4xu1yMd-J0OQ0Qh1KngS5dLBip-0BF0OVLqZ0
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
topic_v2:
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
    internal-label: Data integration
---
# Create Form Data Model

After configuring the data source the next step is to create a Form Data Model based on the data source configured in the earlier step. To create Form Data Model please follow the following steps:

Point your browser to the [data integrations page.](http://localhost:4502/aem/forms.html/content/dam/formsanddocuments-fdm) This lists all the data integrations created on your AEM instance. 

1. Click Create | Form Data Model
1. Provide meaningful title such as FormsAndMarketo and click Next
1. Select the data source that was configured in the earlier step and click create and edit to open the Form Data Model in the edit mode
1. Expand the "FormsAndMarketo" node. Expand the Services node
1. Select the first "Get" operation 
1. Click on Add Selected
1. Click on "Select All" in the "Add Associated Model Objects" dialog box and then click on Add
1. Save your form data model by clicking the Save button
1. Tab to the Services tab
1. Select the only service that is listed and click on Test Service
1. Provide a valid leadId and click on Test. If everything goes well you should get back the lead details as shown in the screenshot below
![testresults](assets/testresults.png)

## Next Steps

[Putting it all together for testing](./part4.md)
