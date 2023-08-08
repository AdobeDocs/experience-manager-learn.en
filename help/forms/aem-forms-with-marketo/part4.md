---
title: AEM Forms with Marketo(Part 4)
description: Tutorial to integrate AEM Forms with Marketo using AEM Forms Form Data Model.
feature: Adaptive Forms, Form Data Model
version: 6.4,6.5
topic: Integrations, Development
role: Developer
level: Experienced
badgeIntegration: label="Integration" type="positive"
badgeVersions: label="AEM Forms 6.5" before-title="false"
exl-id: 6b44e6b2-15f7-45b2-8d21-d47f122c809d
---
# Creating Adaptive Form using Form Data Model

The next step is to create an Adaptive Form and base it on the  Form Data Model created in the earlier step.
The user enters the Lead Id  and on tabbing out the Marketo service to get the leads by id is invoked. The results of the service operation are then mapped to the appropriate fields of the Adaptive Forms.

1. Create an Adaptive Form and base it on "Blank Form Template", associate it with the Form Data Model created in the earlier step.
1. Open the form in edit mode
1. Drag and drop a TextField component and a Panel component on to the Adaptive Form. Set the title of  the TextField component "Enter Lead Id" and set its name to "LeadId"
1. Drag and drop 2 TextField components on to the Panel component
1. Set the Name and Title of the 2 Textfield components as FirstName and LastName
1. Configure the Panel component to be a repeatable component by setting the Minimum to 1 and Maximum to -1. This is required as the Marketo service returns an array of Lead Objects and you need to have a repeatable component to display the results. However, in this case, we are getting only one Lead object back because we are searching on Lead objects by its ID.
1. Create a rule on the LeadId field as shown in the image below
1. Preview the form and enter a valid Lead Id in the LeadID field and tab out. The First Name and Last Name fields should get populated with the results of the service call.

The following screenshot explains the rule editor settings

![ruleeditor](assets/ruleeditor.jfif)

## Debugging

If you are using the bundles provided with this article, you may want to enable [debug logs](http://localhost:4502/system/console/slinglog) for the following classes:

+ `com.marketoandforms.core.impl.MarketoServiceImpl`
+ `com.marketoandforms.core.MarketoConfigurationService`

## Congratulations

You have successfully integrated AEM Forms with Marketo using AEM Forms Form Data Model.