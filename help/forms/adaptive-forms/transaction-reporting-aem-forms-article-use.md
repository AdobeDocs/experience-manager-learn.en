---
title: Using Transaction Reporting in AEM Forms
description: Transaction reports in AEM Forms allow you to keep a count of all transactions taken place since a specified date on your AEM Forms deployment.
feature: Adaptive Forms
version: 6.4.1,6.5
topic: Development
role: Developer
level: Beginner
exl-id: 36c38cb6-6f6a-4328-abf5-7a30059b66ce
---
# Using Transaction Reporting in AEM Forms{#using-transaction-reporting-in-aem-forms}

Transaction reporting to capture the number of Form submissions, rendering of documents using document services and rendering of interactive communications(Web and Print channels) has been introduced with AEM Forms 6.4.1. This capability is primarily for customers wanting to license the software based on the number of form submissions and/or documents rendered. This capability is currently available on AEM Forms OSGI stack only.

## Enabling Transaction Reporting {#enabling-transaction-reporting}

By default transaction recording is disabled. To enable transaction recording please follow the steps mentioned below:

* [Open the configMgr](http://localhost:4502/system/console/configMgr)
* Search for "Forms Transaction Reporting"
* Select the "Record Transactions" checkbox
* Save your changes

Once transaction reporting is enabled, you can submit Adaptive Forms, generate documents using document services or render Interactive Communication documents to see transaction reporting in action.

## Viewing Transaction Report {#viewing-transaction-report}

To view the transaction report, log in to AEM Forms as admin. Only members of the fd-Administrator group can view the transaction report.

Select Tools | Forms | View Transaction Report

or view the transaction report by clicking [here](http://localhost:4502/mnt/overlay/fd/transaction/gui/content/report.html)

![TransctionReporting](assets/transactionreporting.gif)

In the screenshot above Document Processed is the number of documents generated using document services. Documents rendered is the number of Interactive Communication documents(Web and Print) rendered. Forms Submitted is the number of Adaptive Form Submissions.

A transaction remains in the buffer for a specified period (Flush Buffer time + Reverse replication time). By default, it takes approximately 90 seconds for the transaction count to reflect in the transaction report.

Actions like submitting a PDF Form, using Agent UI to preview an interactive communication, or using non-standard form submission methods are not accounted as transactions. AEM Forms provides an API to record such transactions. Call the API from your custom implementations to record a transaction.

If you are viewing the transaction report on the author instance, make sure reverse replication is configured on all the publish instances.

To learn more about transaction reporting [please click here](https://helpx.adobe.com/experience-manager/6-4/forms/using/transaction-reports-overview.html)
