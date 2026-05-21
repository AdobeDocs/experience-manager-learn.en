---
title: Using style system in AEM Forms
description: Define the style policy for the button component
solution: Experience Manager, Experience Manager Forms
type: Documentation
role: Developer
level: Beginner, Intermediate
version: Experience Manager as a Cloud Service
topic: Development
feature: Adaptive Forms
badgeVersions: label="AEM Forms as a Cloud Service" before-title="false"
jira: KT-16276
exl-id: 52205a93-d03c-430c-a707-b351ab333939
TQID: https://experienceleague.adobe.com/SPL83dIyUHfoeVtgzmjULfznDW3m4BJ3hZp9NqMf3W4
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
# Define the style in the policy for the component

* Login to your local cloud ready AEM instance and navigate to Tools | General | Templates | your project name.

* Select and open the  the **Blank with Core Components** template in edit mode.
* Click on the policy icon of the button component to open the policy editor.

* ![button-policy](assets/button-policy.png)

Define the policy as shown below

![button-policy-details](assets/styling-policy.png)

We have defined 2 style/variations called Marketing and Corporate.These variations are associated with corresponding CSS classes.**Please make sure there is no space before and after the CSS class names**.
Save your changes.

| Style     | CSS Class                          |
|-----------|------------------------------------|
| Marketing | cmp-adaptiveform-button--marketing |
| Corporate | cmp-adaptiveform-button--corporate |

These CSS classes will be defined in the component's scss file(_button.scss).

## Next Steps

[Define CSS Classes](./create-variations.md)
