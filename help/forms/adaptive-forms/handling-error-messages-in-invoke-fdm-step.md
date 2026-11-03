---
title: Capturing Error Messages in Form Data Model Service as Step in Workflow
description: Starting with AEM Forms 6.5.1, we now have the ability to capture error messages generated on using invoke Form Data Model Service as a step in AEM Workflow. Workflow.
feature: Workflow
version: Experience Manager 6.5
topic: Development
role: Developer
level: Intermediate
exl-id: 8cae155c-c393-4ac3-a412-bf14fc411aac
last-substantial-update: 2020-06-09T00:00:00.000Z
duration: 51
TQID: 'https://experienceleague.adobe.com/meDSZ7ffEJYLEi5yvYgqUqHOrUDcYTabuBp6ZBU6mqo'
product_v2:
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: 4876a742-a341-5402-aba7-e749c45e777c
    internal-label: Form Data Model
  - id: f6a6f91a-8819-530a-8e7b-c50884a25aef
    internal-label: Workflow
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
topic_v2:
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
    internal-label: Customer experience
---
# Capturing Error Messages in Invoke Form Data Model Service Step

Starting with AEM Forms 6.5.1, we now have the option to capture error messages and specify validation options. Invoke Form Data Model Service step has been enhanced to provide the following capabilities.

* Providing an option for 3 tier validation  ("OFF", "BASIC" and "FULL") to handle Exceptions encountered on invoking Form Data Model Service. The 3 options successively denote a stricter version of checking Database-specific requirements.
![validation-levels](assets/validation-level.PNG)
 
* Providing a checkbox for customizing the execution of Workflow. Hence, user now have the flexibility to go ahead with the Workflow Execution, even if Invoke Form Data Model step throws Exceptions.

* Storing important information of Error arising due to validation exceptions. Three Autocomplete-type variable selectors have been incorporated to select relevant variables to store the ErrorCode(String), ErrorMessage(String) and ErrorDetails(JSON). The ErrorDetails however would be set to null incase the exception is not a DermisValidationException. 
![capturing error messages](assets/fdm-error-details.PNG)

With these changes, Invoke Form Data Model Service step makes sure the input values adhere to the data constraints provided in the swagger file. For example the following error message is thrown when the accountId and balance values are not compliant to the data constraints specified in the swagger file.

```json
{
    "errorCode": "AEM-FDM-001-049"
    "errorMessage": "Input validations failed during operation execution"
    "violations": {
        "/accountId": ["numeric instance is greater than the required maximum (maximum: 20, found: 97)"],
        "/newAccount/balance": ["instance type (string) does not match any allowed primitive type (allowed: [\"integer\",\"number\"])"]
    }   
}
```
