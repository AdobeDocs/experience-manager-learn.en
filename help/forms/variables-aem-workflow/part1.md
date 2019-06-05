---
title: Variables in AEM Workflow[Part1]
seo-title: Variables in AEM Workflow[Part1]
description: Using variables of type xml,json,arraylist,document in aem workflow
seo-description: Using variables of type xml,json,arraylist,document in aem workflow
---

# XML Variables in AEM Workflow

Variables of type XML are typically used when you have an XSD based Adaptive Form and want to extract values from the Adaptive Form submission in your workflow.

The following video walks you through the steps needed to create variables of type String and XML and use them in your workflow.

The XML variable can be used to pre-populate the adaptive form or store the adaptive form's submission data in your workflow.

String variable can be populated by Xpathing into the XML variable. This string variable is then typically used to populate the e-mail template placeholders in Send Email component

>[!NOTE]
If your adaptive form is not associated with XSD, then the XPath to get the value of an element will look like 
**/afData/afUnboundData/data/submitterName**

The adaptive form data is stored under the data element as shown above. **_In the above XPath submitterName is the name of the text field in the Adaptive Form._**

>[!NOTE]
When you are creating a variable of type XML to capture the submitted data in your workflow model, please do not associate the XSD with the variable. This is because when you submit XSD based Adaptive Form the submitted data is not compliant with the XSD. The XSD complaint data is enclosed in /afData/afBoundData/ element.

### Creating XML Variables

>[!VIDEO](https://video.tv.adobe.com/v/26440?quality=12?autoplay=1)

### Using the variable in send email
>[!VIDEO](https://video.tv.adobe.com/v/26441?quality=12)

To get the assets working on your system, please follow the following steps:

* [Download and import the assets into AEM using package manager](assets/xmlandstringvariable.zip)
* [Explore the workflow model](http://localhost:4502/editor.html/conf/global/settings/workflow/models/vacationrequest.html) to understand the variables that are used in the workflow
* [Configure the Email Service](https://helpx.adobe.com/experience-manager/6-5/sites/administering/using/notification.html#ConfiguringtheMailService)
* [Open the Adaptive Form](http://localhost:4502/content/dam/formsanddocuments/applicationfortimeoff/jcr:content?wcmmode=disabled)
* Fill in the details and submit the form

