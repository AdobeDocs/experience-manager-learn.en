---
title: Using vertical tabs in AEM Forms as a Cloud Service
description: Creata an Adaptive Form using vertical tabs
solution: Experience Manager, Experience Manager Forms
type: Documentation
role: Developer
level: Beginner, Intermediate
version: Experience Manager as a Cloud Service
topic: Development
feature: Adaptive Forms
thumbnail: 331891.jpg
badgeVersions: label="AEM Forms as a Cloud Service" before-title="false"
jira: KT-16023
exl-id: c5bbd35e-fd15-4293-901e-c81faf6025f9
TQID: https://experienceleague.adobe.com/vYN-iAw7R9PzIIfsUFpoGIuHDAB9SEEVS41gdlaq58c
product_v2:
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
---
# Navigating between the tabs

You can navigate between the tab by clicking on the individual tabs or by using previous and next buttons on the form. 
To navigate using buttons, add two buttons to your form and name them Previous and Next. Associate the following custom function with the click event of the button to navigate between the tabs.

The following is the custom function to navigate between the tabs.



``` javascript
/**
 * Navigate in panel with focusOption
 * @name navigateInPanelWithFocusOption
 * @param {object} panelField
 * @param {string} focusOption - values can be 'nextItem'/'previousItem'
 * @param {scope} globals
 */
function navigateInPanelWithFocusOption(panelField, focusOption, globals)
{
    globals.functions.setFocus(panelField, focusOption);
}

```

The following is the rule editor for the Next and Previous buttons

**Next Button**

![next-button](assets/next-button.png)

**Previous Button**

![prev-button](assets/prev-button.png)
