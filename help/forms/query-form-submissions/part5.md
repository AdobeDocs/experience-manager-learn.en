---
title: Deploy the sample on your local server
description: Multi-part tutorial to walk you through the steps involved in querying form submissions stored in Azure portal
feature: Adaptive Forms
doc-type: Tutorial
version: Experience Manager 6.5
topic: Development
role: Developer
level: Experienced
jira: kt-14884
last-substantial-update: 2024-03-03T00:00:00.000Z
exl-id: 44841a3c-85e0-447f-85e2-169a451d9c68
duration: 20
TQID: https://experienceleague.adobe.com/VM3c5VradssfWepQBRXBGIfVjffIX8LMdToaQ6gcgFA
product_v2:
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
---
# Deploy the sample on your local server

To get this usecase working on your local server, please follow the steps listed below.It is assumed your AEM instance is running on localhost, 4502 port.

* [Install the package](assets/azuredemo.all-1.0.0-SNAPSHOT.zip) using package manager.

* Provide the Azure portal credentials using the OSGi configMgr
![azure-portal](assets/azure-portal-config.png)
    Make sure the Storage URI ends in slash and the SAS token starts with a ?
* Navigate to [AzureDemo](http://localhost:4502/libs/fd/fdm/gui/components/admin/fdmcloudservice/fdm.html/conf/azuredemo)

* Edit the authentication settings of the following 3 datasources to match your environment
![data-sources](assets/fdm-data-sources.png)

* Preview and submit [ContactUs form](http://localhost:4502/content/dam/formsanddocuments/azureportal/contactus/jcr:content?wcmmode=disabled)

* [Query your form submission](http://localhost:4502/content/dam/formsanddocuments/azureportal/queryformsubmissions/jcr:content?wcmmode=disabled)
