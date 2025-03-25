---
title: Handle a HTML5 Form Submission
description: Create HTML5 Form submission handler.
feature: Mobile Forms
doc-type: article
version: Experience Manager 6.4, Experience Manager 6.5
jira: KT-5269
thumbnail: kt-5269.jpg
topic: Development
role: Developer
level: Experienced
exl-id: 93e1262b-0e93-4ba8-aafc-f9c517688ce9
last-substantial-update: 2020-07-07
duration: 66
---

# Handle HTML5 form submission

HTML5 forms can be submitted to a servlet hosted in AEM. The submitted data can be accessed in the servlet as an input stream. To submit your HTML5 form, add an "HTTP Submit Button" on your form template using AEM Forms Designer.

## Create your submit handler

A simple servlet can handle the HTML5 form submission. Extract the submitted data using the following code snippet. Download the [servlet](assets/html5-submit-handler.zip) provided in this tutorial. Install the [servlet](assets/html5-submit-handler.zip) using the [package manager](http://localhost:4502/crx/packmgr/index.jsp).

```java
StringBuffer stringBuffer = new StringBuffer();
String line = null;
java.io.InputStreamReader isReader = new java.io.InputStreamReader(request.getInputStream(), "UTF-8");
java.io.BufferedReader reader = new java.io.BufferedReader(isReader);
while ((line = reader.readLine()) != null) {
    stringBuffer.append(line);
}
System.out.println("The submitted form data is " + stringBuffer.toString());
```

Ensure you have configured the [Adobe LiveCycle Client SDK Configuration](https://helpx.adobe.com/aem-forms/6/submit-form-data-livecycle-process.html) if you plan to use the code to invoke a J2EE process.

## Configure the Submit URL of the HTML5 form

![Submit URL](assets/submit-url.PNG)

- Open the xdp and navigate to _Properties_->_Advanced_.
- Copy http://localhost:4502/content/AemFormsSamples/handlehml5formsubmission.html and paste it into the Submit URL text field.
- Click the _SaveAndClose_ button.

### Add entry in the Exclude Paths

- Go to [configMgr](http://localhost:4502/system/console/configMgr).
- Search for _Adobe Granite CSRF Filter_.
- Add the following entry in the Excluded Paths section: _/content/AemFormsSamples/handlehml5formsubmission_.
- Save your changes.

### Test the form

- Open the xdp template.
- Click on _Preview_->Preview as HTML.
- Enter data in the form and click submit.
- Check the server's stdout.log file for the submitted data.

### Additional Reading

For more information on generating PDFs from HTML5 form submissions, refer to this [article](https://experienceleague.adobe.com/docs/experience-manager-learn/forms/document-services/generate-pdf-from-mobile-form-submission-article.html).

