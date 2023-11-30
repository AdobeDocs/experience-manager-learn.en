---
title: Report on submitted form data fields using Adobe Analytics
description: Integrate AEM Forms CS with Adobe Analytics to report on form data fields
solution: Experience Manager, Experience Manager Forms
type: Documentation
role: Developer
level: Beginner, Intermediate
version: Cloud Service
feature: Adaptive Forms
topic: Integrations, Development
jira: KT-12557
badgeIntegration: label="Integration" type="positive"
badgeVersions: label="AEM Forms as a Cloud Service" before-title="false"
exl-id: b9dc505d-72c8-4b6a-974b-fc619ff7c256
---
# Create data elements

In the Tags property we added two new data elements(ApplicantsStateOfResidence and validationError).

![adaptive-form](assets/data_elements.png)

## ApplicantStateOfResidence

The **ApplicantStateOfResidence** data element was configured by selecting **Core** in the extension drop-down and **Custom Code** for the Data Element Type as shown in the screen shot below
![applicant-state-residence](assets/applicantstateofresidence.png)

The following custom code was used to capture the value from the **_state_** adaptive form field.

``` javascript
// use the GuideBridge API to access adaptive form elements
//The state field's SOM expression is used to access the state field
var ApplicantsStateOfResidence = guideBridge.resolveNode("guide[0].guide1[0].guideRootPanel[0].state[0]").value;
_satellite.logger.log("Returning  Applicants State Of Residence is "+ApplicantsStateOfResidence);
return ApplicantsStateOfResidence;
```

## validationError

The **ValidationError** data element was configured by selecting **Core** in the extension drop-down and **Custom Code** for the Data Element Type as shown in the screen shot below

![validation-error](assets/validation-error.png)

The following custom code was written to set the `validationError` data element value.

```javascript
var validationError = "";
// Using GuideBridge API to access adaptive forms fields using the fields SOM expression
var tel = guideBridge.resolveNode("guide[0].guide1[0].guideRootPanel[0].telephone[0]");
var email = guideBridge.resolveNode("guide[0].guide1[0].guideRootPanel[0].email[0]");

_satellite.logger.log("Got tel in Tags custom script "+tel.isValid)
_satellite.logger.log("Got email in Tags custom script "+email.isValid)

if (tel.isValid == false) {  
  validationError = "error: telephone number";
  _satellite.logger.log("Validation error is "+ validationError);
}

if (email.isValid == false) {  
  validationError = "error: invalid email";
  _satellite.logger.log("Validation error is "+ validationError);
}

return validationError;
```

## Next steps

[Create Rules](./rules.md)