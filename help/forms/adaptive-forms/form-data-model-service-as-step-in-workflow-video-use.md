---
title: Using Form Data Model Service as Step in Workflow
description: Starting with AEM Forms 6.4, we now have the ability to use Form Data Model as part of AEM Workflow. The following video walks thru the steps needed to configure Form Data Model step in AEM Workflow.
feature: Workflow
type: Tutorial
version: Experience Manager 6.4, Experience Manager 6.5
topic: Development
role: Developer
level: Intermediate
exl-id: 0c77a853-fa71-46ac-8626-99bc69d6222d
last-substantial-update: 2020-06-09T00:00:00.000Z
duration: 205
TQID: https://experienceleague.adobe.com/2nTrs439Pd2jmwxl5k9PFUSF0AhLpr7x-aQ1GJQSb94
product_v2:
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
    internal-label: Metadata
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
    internal-label: Security
---
# Using Form Data Model Service as Step in Workflow {#using-form-data-model-service-as-step-in-workflow}

Starting with AEM Forms 6.4, we now have the ability to use Form Data Model as part of AEM Workflow. The following video walks thru the steps needed to configure Form Data Model step in AEM Workflow


>[!VIDEO](https://video.tv.adobe.com/v/21719?quality=12&learn=on)

To test this capability on your server, follow the below instructions

* [Download and deploy the setvalue bundle](/help/forms/assets/common-osgi-bundles/SetValueApp.core-1.0-SNAPSHOT.jar). This is the custom OSGI bundle which sets metadata properties.

  >[!NOTE]
  >
  >In AEM Forms 6.5 and above this capability is available out of the box as [describe here](form-data-model-service-as-step-in-aem65-workflow-video-use.md)

* Setup tomcat with SampleRest.war file as described [here](https://experienceleague.adobe.com/docs/experience-manager-learn/forms/ic-print-channel-tutorial/introduction.html).The war file deployed in Tomcat has the code to return the applicant's credit score. The credit score is random number between 200 and 800

* [Import the assets into AEM using package manager](assets/invoke-fdm-as-service-step.zip).The package contains the following:

  * Workflow model which uses FDM step.
  * Form Data Model that is used in the FDM step.
  * Adaptive form to trigger the workflow on submission.
* Open the [MortgageApplicationForm](http://localhost:4502/content/dam/formsanddocuments/loanapplication/jcr:content?wcmmode=disabled). Fill in the details and submit. On the form submission the [loanapplication workflow](http://http://localhost:4502/editor.html/conf/global/settings/workflow/models/LoanApplication2.html) is triggered.

![workflow](assets/fdm-as-service-step-workflow.PNG).

The workflow utilizes Or Split component to route the application to admin if the credit score is over 500. If the credit score is less than 500 the application is routed to cavery
