---
title: Querying form submission
description: Multi-part tutorial to walk you through the steps involved in querying form submissions stored in Azure portal
feature: Adaptive Forms
doc-type: Tutorial
version: 6.5
topic: Development
role: Developer
level: Experienced
jira: kt-14884
last-substantial-update: 2024-03-03
exl-id: b814097c-0066-44da-bba5-6914dee0df75
duration: 32
---
# Create custom submit

A custom submit handler was written to handle the form submission. At a high level the custom submit handler does the following

* Extracts the name of the submitted form.
* Extracts the submitted data.The submitted data of an core component based form is always in JSON format.
* Extracts and stores the form attachments in Azure portal. Updates the submitted json data with the attachment's url.
* Creates blob index tags - Finds the list of searchable field for the form and its corresponding value from the submitted data.
* Associates the blob index tags with the submitted data and stores it in Azure portal.

The following screen shot shows you the blob index tags in Azure portal

![blob-index-tags](assets/blob-index-tags.png)

The custom submit code is in **_StoreFormDataWithBlobIndexTagsInAzure_** and the code for storing and retrieving data from Azure is in the component **_SaveAndFetchFromAzure_**

## Next Steps

[Build query interface](./part3.md)
