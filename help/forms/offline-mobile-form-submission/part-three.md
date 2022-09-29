---
title: Trigger AEM workflow on HTM5 Form Submission - Review and approve PDF
seo-title: Trigger AEM Workflow on HTML5 Form Submission
description: Continue filling mobile form in offline mode and submit mobile form to trigger AEM workflow
seo-description: Continue filling mobile form in offline mode and submit mobile form to trigger AEM workflow
feature: Mobile Forms
topics: development
audience: developer
doc-type: article
activity: implement
version: 6.4,6.5
topic: Development
role: Developer
level: Experienced
exl-id: a767d8f8-d75e-4472-9139-c08d804ee076
---
# Workflow to review and approve the submitted PDF

The last and final step is to create AEM workflow which will generate a static, or non-interactive, PDF for review and approval. Workflow is triggered via an AEM Launcher configured on the node `/content/pdfsubmissions`.

The following screenshot shows the steps involved in the workflow.

![workflow](assets/workflow.PNG)

## Generate Non-Interactive PDF workflow step

The XDP template and the data to be merged with the template is specified here. The data to be merged is the submitted data from the PDF. This submitted data is stored under the node `/content/pdfsubmissions`. 

![workflow](assets/generate-pdf1.PNG)

The generated PDF is assigned to workflow variable called `submittedPDF`.

![workflow](assets/generate-pdf2.PNG)

### Assign the generated pdf for review and approval

Assign task workflow component is used here to assign the generated PDF for review and approval. The variable `submittedPDF` is used in the Forms and Documents tab of the Assign Task workflow component.

![workflow](assets/assign-task.PNG)
