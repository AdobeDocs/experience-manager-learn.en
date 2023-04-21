---
title: Deploy the assets locally
description: Deploy the tutorial assets on your local AEM instance
feature: Adaptive Forms
version: 6.5
topic: Development
role: Developer
level: Beginner
last-substantial-update: 2023-01-04
exl-id: d23b51ba-1efb-4505-b5b3-44a02177e467
---
# Deploy on your system

Please follow the steps listed below to get this use case working on your local AEM instance.

* [Deploy the DevelopingWithServiceUser Bundle](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/developingwithserviceuser.zip) contained in the zip file.

* Add the following entry in the Apache Sling Service User Mapper Service **DevelopingWithServiceUser.core:getformsresourceresolver=fd-service** using the [configMgr](http://localhost:4502/system/console/configMgr).

* [Deploy the newsletters bundle](assets/Newsletters.core-1.0.0-SNAPSHOT.jar). This bundle contains the code to list the folder contents and assemble the selected newsletter(s).

* [Import the package using Package Manager](assets/newsletter.zip). This package contains client library and sample pdf files to test the solution.

* [Import the sample adaptive form](assets/sample-adaptive-form.zip). This form will list the newsletters that can be selected.

* [Preview the form](http://localhost:4502/content/dam/formsanddocuments/downloadarchivednewsletters/jcr:content?wcmmode=disabled).
Select a couple of newsletters to download.The selected newsletters will be combined into one pdf and returned to you.
