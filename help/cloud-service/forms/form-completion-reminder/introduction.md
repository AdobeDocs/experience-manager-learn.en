---
title: User Re-Engagement for Unsubmitted Forms
description: This solution demonstrates how to recover abandoned form submissions by integrating AEM Forms, Adobe Experience Platform Launch, and Adobe Journey Optimizer (AJO) to deliver automated reminder emails to users who start filling out a form but do not complete the submission process.
solution: Experience Manager, Experience Manager Forms, Journey Optimizer
type: Documentation
role: Developer
level: Beginner, Intermediate
version: Experience Manager as a Cloud Service
feature: Adaptive Forms
topic: Integrations, Development
jira: KT-21185
badgeIntegration: label="Integration" type="positive"
badgeVersions: label="AEM Forms as a Cloud Service" before-title="false"
---

# User Re-Engagement for Unsubmitted Forms

This solution demonstrates how to recover abandoned form submissions by integrating AEM Forms, Adobe Experience Platform Launch, and Adobe Journey Optimizer (AJO) to deliver automated reminder email(s) to users who start filling out a form but do not complete the submission process.

The workflow begins with an adaptive form built using AEM Forms, where user interactions and form progress are captured in real time. Using Adobe Launch, key behavioral events such as form initiation, field interactions, and incomplete submissions are tracked and sent to Adobe Experience Platform.

When a user abandons the form before submission, the captured event data is used to trigger a journey in Adobe Journey Optimizer. AJO then sends a personalized reminder email encouraging the user to return and complete the form submission. The email can include contextual messaging and a direct link to resume the process, helping improve conversion and completion rates.

## Prerequisites

Before starting this tutorial, you should have:

- Basic familiarity with Adobe Experience Platform (AEP)
- Understanding of AEP Tags / Adobe Data Collection concepts
- Basic understanding of XDM schemas and datasets
- Familiarity with Adobe Journey Optimizer (AJO) journeys and events
- General understanding of Web SDK event collection
- Created and [deployed an AEM Forms project](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/forms/developing-for-cloud-service/getting-started) using the latest AEM Archetype through Cloud Manager.
