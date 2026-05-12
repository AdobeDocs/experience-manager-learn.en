---
title: Import data from a PDF file into Adaptive Form
description: Tutorial to populate an adaptive form by importing a PDF file
feature: Adaptive Forms
version: Experience Manager 6.5
topic: Development
role: Developer
level: Beginner
exl-id: f21753b2-f065-4556-add4-b1983fb57031
duration: 21
TQID: https://experienceleague.adobe.com/L8rut-iadjV1Q--lFFI0gwhVoSGOQCo7LU13TXTKYWM
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
# Deploy the sample assets

You can deploy the sample assets to get this solution working on your local AEM Forms instance

* [Import the client library and custom component for uploading the pdf form via Package Manager](./assets/client-libs-custom-component.zip)
* Download and deploy the bundle using the OSGi web console[Custom Document Services Bundle](/help/forms/assets/common-osgi-bundles/AEMFormsDocumentServices.core-1.0-SNAPSHOT.jar)
* Download and deploy the bundle using the OSGi web console [Developing with Service User Bundle](/help/forms/assets/common-osgi-bundles/DevelopingWithServiceUser.jar)
* Download and deploy the bundle using the OSGi web console[import data from pdf file](./assets/onlineToOffline.core-1.0.0-SNAPSHOT.jar)
* Add the entry _**DevelopingWithServiceUser.core:getresourceresolver=data**_ in the _**Apache Sling Service User Mapper Service**_ OSGi configuration console
