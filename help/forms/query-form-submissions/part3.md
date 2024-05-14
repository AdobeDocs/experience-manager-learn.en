---
title: Build query interface
description: Multi-part tutorial to walk you through the steps involved in querying form submissions stored in Azure portal
feature: Adaptive Forms
doc-type: Tutorial
version: 6.5
topic: Development
role: Developer
level: Experienced
jira: kt-14884
last-substantial-update: 2024-03-03
exl-id: 570a8176-ecf8-4a57-ab58-97190214c53f
duration: 25
---
# Build query interface

A simple query interface was built to allow the "Administrator" to input search criteria in order to retrieve specifc form submissions. The results are then displayed in a simple tabular format with the option to view a particular form submission.

![query-submissions](assets/query-submissions.png)

The dropdowns in this interface are cascading dropdown. The options available in the dropdown change based on the selections made in the previous dropdown.

The dropdowns are populated using RESTful data sources.

The search results are displayed in a custom component called "SearchResults". When the user clicks the view button the form is prefilled with the submitted data and attachments.

## Next Steps

[Write the prefill service](./part4.md)
