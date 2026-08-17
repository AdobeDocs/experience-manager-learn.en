---
title: Draft Forms Dashboard
description: Learn how to build an automated draft reminder solution using AEM Forms Portal and Adobe Journey Optimizer
solution: Experience Manager, Experience Manager Forms, Journey Optimizer
type: Documentation
role: Developer
level: Beginner, Intermediate
version: Experience Manager as a Cloud Service
feature: Adaptive Forms
topic: Integrations, Development
jira: KT-22325
badgeIntegration: label="Integration" type="positive"
badgeVersions: label="AEM Forms as a Cloud Service" before-title="false"
---

# Draft Forms Dashboard


The Draft Forms Dashboard provides a centralized view of forms that have been saved but not yet submitted. It queries Adobe Experience Platform to display the form name, owner email, and save date, and allows an operator to manually send a reminder by triggering a `form.nudge` event in AEP, which starts an Adobe Journey Optimizer journey to deliver the reminder email.

## Implementation Overview

1. **Configure the Node.js Application**
   - Configure the Node.js application with the credentials required to connect to **Adobe Experience Platform Query Service**.
   - Obtain the **Adobe Experience Platform Query Service** connection credentials from **Adobe Experience Platform > Queries > Credentials**.
   - Store the Query Service host, port, database, username, and password as environment variables.
   - Configure the Adobe Experience Platform credentials and datastream information required to send the `form.nudge` Experience Event.
   - For this implementation, these configuration values are defined as environment variables in **Render**.
   - Update the Query Service table name in the application to match the form status dataset in your Adobe Experience Platform environment.

2. **Create the Draft Forms Dashboard**
   - Build a **Node.js application** to provide a dashboard for viewing forms that have been saved but not yet submitted.
   - For this implementation, the Node.js application is hosted on **Render**.
   - Connect the application to **Adobe Experience Platform Query Service**.
   - Query the form status dataset for records where `submitted = false`.
   - Display information such as the **form name, owner email, and saved date** for forms that are still in draft mode.

3. **Add the Send Reminder Action**
   - Add a **Send Reminder** button for each draft form displayed on the dashboard.
   - When the button is selected, send the corresponding `ownerId` and `formId` to the Node.js backend hosted on Render.
   - The backend sends a **`form.nudge`** Experience Event to Adobe Experience Platform using the `Auth0Owner` identity.

4. **Create the Nudge Journey in Adobe Journey Optimizer**
   - Create a custom **`form.nudge`** event in Adobe Journey Optimizer.
   - Create a journey that is triggered when the `form.nudge` event is received.
   - Use the owner's profile associated with the `Auth0Owner` identity to determine the email recipient.
   - Send a reminder email encouraging the user to return to the Forms Portal and complete the saved form.

This implementation provides an **on-demand reminder capability** from a Node.js dashboard hosted on Render, in addition to the automated reminder sent after the configured form abandonment period.

Use the provided [JavaScript file as a reference implementation](assets/javascript_files.zip) for building the Draft Forms dashboard. The sample demonstrates how to query Adobe Experience Platform for forms that have not been submitted and how to trigger a form.nudge event when the Send Reminder action is selected. You can adapt the implementation to suit your application and environment.
