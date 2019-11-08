---
title: Trigger AEM workflow on HTM5 Form Submission
seo-title: Trigger AEM Workflow on HTML5 Form Submission
description: Continue filling mobile form in offline mode and submit mobile form to trigger AEM workflow
seo-description: Continue filling mobile form in offline mode and submit mobile form to trigger AEM workflow
feature: mobile-forms
topics: development
audience: developer
doc-type: article
activity: implement
version: 6.4,6.5
---

# Getting this use case to work on your system

>[!NOTE]For the sample assets to work on your system, it is assumed that you have AEM Author and Publish instance running on port 4502 and 4503 respectively. It is also assumed the AEM Author is accessible via `admin`/`admin`. If the port numbers or the admin password has been changed then these sample assets will not work. You will have to create your own assets using the provided sample code.

To get this use case working on your local system, following these steps:

* Install AEM Author instance on port 4502 and AEM Publish instance on port 4503
* [Follow the instructions specified in developing with service user in AEM Forms](https://docs.adobe.com/content/help/en/experience-manager-learn/forms/adaptive-forms/service-user-tutorial-develop.html). Please make sure to create the service user and deploy the bundle on your AEM Author and Publish instance.
* [Deploy the custom AEMFormDocumentService Bundle](https://forms.enablementadobe.com/content/DemoServerBundles/AEMFormsDocumentServices.core-1.0-SNAPSHOT.jar).This bundle needs to be deployed on your AEM Publish instance. This bundle has the code to generate interactive PDF from mobile form.
* [Download and Unzip the assets related to this article.](assets/offline-pdf-submission-assets.zip) You will get the following
    * **offline-submission-profile.zip** - This AEM package contains the custom profile that allows you to download the interactive pdf to your local file system. Deploy this package on your AEM Publish instance.
    * **xdp-form-and-workflow.zip** - This AEM package contains XDP, sample workflow,launcher configured on node content/pdfsubmissions. Deploy this package on both your AEM Author and Publish instance.
    * **HandlePDFSubmission.HandlePDFSubmission.core-1.0-SNAPSHOT.jar** - This is the AEM bundle which does most of the work. This bundle contains the servlet mounted on `/bin/startworkflow`. This servlet saves the submitted form data under `/content/pdfsubmissions` node in AEM's repository. Deploy this bundle on both your AEM Author and Publish instance.
* [Preview the mobile form](http://localhost:4503/content/dam/formsanddocuments/testsubmision.xdp/jcr:content)
* Fill in several fields and then click the button on the toolbar to download the interactive PDF.
* Fill in the downloaded PDF using Acrobat and hit submit button.
* You should get a success message
* Login to AEM Author instance as admin
* [Check the AEM Inbox](http://localhost:4502/aem/inbox)
* You should have workitem to review the submitted PDF

