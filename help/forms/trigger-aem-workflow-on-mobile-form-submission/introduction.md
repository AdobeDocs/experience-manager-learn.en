---
title: Trigger AEM workflow on HTML5 Form Submission introduction
description: Trigger an AEM workflow on mobile form submission
feature: Mobile Forms
doc-type: article
version: 6.4,6.5
topic: Development
role: Developer
level: Experienced
last-substantial-update: 2024-09-17
jira: kt-16215
badgeVersions: label="AEM Forms 6.5" before-title="false"

---
# Trigger AEM workflow on a Mobile Form Submission

A common use case is to have the ability to render the XDP as HTML for data capture activities.On submission of this form, there may be an need to trigger an AEM workflow. In the AEM workflow we could merge the data with the xdp template and present the generated PDF for review and approval.The form will be rendered on a publish instance and the workflow will be triggered on an AEM processing instance.
The following steps are involved in the use case

* User fills and submits an HTML5 form(HTML5 rendition of XDP).
* The submission is handled by an servlet in the publish instance.
* The servlet stores the data in a predefined folder in the repository of the AEM processing instance.
* Workflow launcher is configured to trigger an AEM workflow every time a new file is added under a particular folder.

This tutorial walks through the steps needed to accomplish the above use case. Sample code and assets related to this tutorial are [available here.](./deploy-assets.md)


## Next Steps

[Handle Form Submission](./handle-form-submission.md)