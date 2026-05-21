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
exl-id: 9982e041-fff7-4be6-91c9-e322d2fd3e01
duration: 41
TQID: https://experienceleague.adobe.com/0bTp32DpjL4kxzN9KUCOgGgo-bmHdPsWxfRgPdwzZbo
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
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
---
# Define the rule

In the Tags property we created 2 new [rules](https://experienceleague.adobe.com/docs/platform-learn/implement-in-websites/configure-tags/add-data-elements-rules.html) (**Field Validation Error and FormSubmit**).

![adaptive-form](assets/rules.png)


## Field Validation Error

The **Field Validation Error** rule gets triggered every time there is validation error in adaptive form field. For example in our form if the telephone number or the email is not in the expected format a validation error message is displayed. 

The Field Validation Error rule is configured by setting the event to _**Adobe Experience Manager Forms-Error**_ as shown in the screen shot



![applicant-state-residence](assets/field_validation_error_rule.png)

The Adobe Analytics - Set Variables is configured as follows

![set action](assets/field_validation_action_rule.png)

## Form Submit Rule

The Form Submit rule is triggered every time an Adaptive Form is successfully submitted.

The Form Submit rule is configured using the _**Adobe Experience Manager Forms - Submit**_ event

![form-submit-rule](assets/form-submit-rule.png)

In the Form Submit rule, the value of the data element _**ApplicantsStateOfResidence**_ is mapped to prop5 and the value of the data element FormTitle is mapped to prop8.

The Adobe Analytics - Set variables is configured as follows.
![form-submit-rule-set-variables](assets/form-submit-set-variable.png)

When you're ready to test your Tags code,[publish your changes made to the tags](https://experienceleague.adobe.com/docs/experience-platform/tags/publish/publishing-flow.html) using the publishing flow.

## Next steps

[Test the solution](./test.md)