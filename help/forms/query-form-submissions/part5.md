---
title: Deploy the sample on your local server
description: Multi-part tutorial to walk you through the steps involved in querying form submissions stored in Azure portal
feature: Adaptive Forms
doc-type: Tutorial
version: 6.5
topic: Development
role: Developer
level: Experienced
jira: kt-14884
last-substantial-update: 2024-03-03
exl-id: 44841a3c-85e0-447f-85e2-169a451d9c68
duration: 20
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
