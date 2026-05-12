---
title: Report on submitted form data fields using Adobe Analytics
description: Integrate AEM Forms CS with Adobe Analytics to report on form data fields
solution: Experience Manager, Experience Manager Forms
type: Documentation
role: Developer
level: Beginner, Intermediate
version: Experience Manager as a Cloud Service
feature: Adaptive Forms
topic: Integrations, Development
jira: KT-12557
badgeIntegration: label="Integration" type="positive"
badgeVersions: label="AEM Forms as a Cloud Service" before-title="false"
exl-id: 43665a1e-4101-4b54-a6e0-d189e825073e
duration: 38
TQID: https://experienceleague.adobe.com/AZUXxeOhIr0BgAff5-44tOx-T3TTBwYBLCFrvsxKmZs
product_v2:
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: a1df6763-63b5-45b4-8c8a-155a692a2b3e
    internal-label: Integrations
  - id: ae478996-b206-4712-9b0c-dc78a2644453
    internal-label: Integrations
  - id: f2d27a5f-0d67-4d85-8a24-86a8d8a3574b
    internal-label: Developer tools
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
    internal-label: Reporting
---
# Test your solution

Preview and submit your form using several combinations of form values. Allow several to 30 minutes to see your data in Adobe Analytics reports. Data set to props show up in reporting sooner than data set to eVars.

## Report Suite

The form data captured in Adobe Analytics is presented in donut format

**Submissions by State**

![applicantsbystate](assets/donut.png)

Field Validation Errors

![field-validation-error](assets/donut-field-validation.png)

## Debugging

Make sure the Adaptive Form is using the same configuration container which contains the Adobe Launch Configuration.

To confirm that the form is sending data to Adobe Analytics, do the following

* Open the Developer Tools in your browser.
* Enter in the following text in the Console panel.

```javascript
_satellite.setDebug(true)
```

Interact with your form while keeping the console window open. You should see something like this

![console-debug](assets/debug.png)

## Use Adobe Experience Platform Debugger

 Add the [AEP debugger extension](https://experienceleague.adobe.com/docs/experience-platform/debugger/home.html) to your browser(you are required to sign in) to get more debugging information

![platform-debugger](assets/platform-debugger.png)

## Congratulations

You have successfully integrated AEM Forms as a Cloud Service with Adobe Analytics to report on form data fields.