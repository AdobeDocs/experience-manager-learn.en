---
title: Submit data to SharePoint list using workflow step
description: Insert data in to sharepoint list using invoke FDM workflow step
feature: Adaptive Forms
type: Documentation
role: Developer
level: Beginner
version: Cloud Service
topic: Integrations
jira: KT-15126
exl-id: b369ed05-ba25-4b0e-aa3b-e7fc1621067d
duration: 52
---
# Insert data into SharePoint list using invoke FDM workflow step


This article explains the steps required to insert data into SharePoint list using the invoke FDM step in AEM workflow.

This article assumes you have [successfully configured adaptive form to submit data to SharePoint list.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/configure-submit-actions-core-components.html?lang=en#connect-af-sharepoint-list)


## Create a form data model based on the SharePoint list data source

* Create a new form data model based on the SharePoint list data source.
* Add the appropriate model and the get service of the form data model.
* Configure the insert service to insert the top level model object.
* Test the insert service.


## Create a workflow

* Create a simple workflow with invoke FDM step.
* Configure the invoke FDM step to use the form data model created in the previous step.
* ![associate-fdm](assets/fdm-insert-1.png)

## Adaptive Form based on core components

The submitted data is in the following format. We need to extract the ContactUS object using dot notation in the invoke Form Data Model Service workflow step as shown in the screenshot 

```json
{
  "ContactUS": {
    "Title": "Mr",
    "Products": "Photoshop",
    "HighNetWorth": "1",
    "SubmitterName": "John Does"
  }
}
```


* ![map-input-parameters](assets/fdm-insert-2.png)


## Adaptive Form based on foundation components

The submitted data is in the following format. Extract the ContactUS JSON object using the dot notation in the invoke Form Data Model Service workflow step

```json
{
    "afData": {
        "afUnboundData": {
            "data": {}
        },
        "afBoundData": {
            "data": {
                "ContactUS": {
                    "Title": "Lord",
                    "HighNetWorth": "true",
                    "SubmitterName": "John Doe",
                    "Products": "Forms"
                }
            }
        },
        "afSubmissionInfo": {
            "lastFocusItem": "guide[0].guide1[0].guideRootPanel[0].afJsonSchemaRoot[0]",
            "stateOverrides": {},
            "signers": {},
            "afPath": "/content/dam/formsanddocuments/foundationform",
            "afSubmissionTime": "20240517100126"
        }
    }
}

```

![foundation-based-form](assets/foundation-based-form.png)

## Configure Adaptive Form to trigger AEM workflow

* Create Adaptive Form using the Form Data Model created in the earlier step.
* Drag and drop some fields from the data source onto your form.
* Configure the submit action of the form as shown below
* ![submit-action](assets/configure-af.png)



## Test the form

Preview the form created in the previous step. Fill out the form and submit. The data from the form should get inserted into the SharePoint list.
