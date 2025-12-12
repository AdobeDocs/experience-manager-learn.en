---
title: Using Form Data Model Service as Step in AEM 6.5 Workflow
description: AEM Forms 6.5 introduced the ability to create variables in the AEM Workflow. With this new capability using the "Invoke Form Data Model Service" in AEM Workflow has become very easy. The following video will walk you through the steps involved in using Invoke Form Data Model Service in AEM Workflow.
feature: Workflow
type: Tutorial
version: Experience Manager 6.5
topic: Development
role: Developer
level: Intermediate
exl-id: 1f13d82e-c1d0-4c8c-8468-b4a4c5897c71
last-substantial-update: 2021-02-09
duration: 239
---
# Using Form Data Model Service as Step in AEM 6.5 Workflow {#using-form-data-model-service-as-step-in-workflow}

Starting with AEM Forms 6.4, we now have the ability to use Form Data Model Service as part of AEM Workflow. The following video walks thru the steps needed to configure Form Data Model step in AEM Workflow

>[!NOTE]
>
>The capability demonstrated in this video requires AEM Forms 6.5.1


>[!VIDEO](https://video.tv.adobe.com/v/28145?quality=12&learn=on)

To test this capability on your server, follow the below instructions

* Setup tomcat with SampleRest.war file as described [here](https://helpx.adobe.com/experience-manager/kt/forms/using/preparing-datasource-for-form-data-model-tutorial-use.html).The war file deployed in Tomcat has the code to return the applicant's credit score.The credit score is random number between 200 and 800

* [Import the assets into AEM using package manager](assets/aem65-loanapplication.zip)
* The package contains the following:

  * Workflow model which uses FDM step.
  * Form Data Model that is used in the FDM step.
  * Adaptive form to trigger the workflow on submission.
* Open the [MortgageApplicationForm](http://localhost:4502/content/dam/formsanddocuments/loanapplication/jcr:content?wcmmode=disabled). Fill in the details and submit. On the form submission the [loanapplication workflow](http://http://localhost:4502/editor.html/conf/global/settings/workflow/models/LoanApplication2.html) is triggered.

![workflow](assets/invokefdm651.PNG).

The workflow utilizes Or Split component to route the application to admin if the credit score is over 500. If the credit score is less than 500 the application is routed to cavery.
