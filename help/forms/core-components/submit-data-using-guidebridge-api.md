---
title: Using GuideBridge API to Post Form Data
description: Learn how to access and send form data using GuideBridge API for adaptive forms. Save and retrieve form data with ease.
duration: 68
feature: Adaptive Forms
version: Experience Manager 6.5
topic: Development
role: Developer
level: Experienced
jira: KT-15286
last-substantial-update: 2024-04-05
exl-id: 099aaeaf-2514-4459-81a7-2843baa1c981
---

# Accessing and Sending Form Data with GuideBridge API

Learn how to utilize the GuideBridge API to access and send form data to a REST endpoint for storage and retrieval. This functionality enables users to save and resume form completion seamlessly.

The form data is saved by triggering a JavaScript function upon clicking a button in the rule editor.

![Rule Editor](assets/rule-editor.png)

The JavaScript function below demonstrates how to send the form data to the specified endpoint:

```javascript
/**
* Submits data and attachments 
* @name submitFormDataAndAttachments Submit form data and attachments to REST endpoint
* @param {string} endpoint in String format
* @return {string} 
 */
 
function submitFormDataAndAttachments(endpoint) {
    guideBridge.getFormDataObject({
        success: function(resultObj) {
            const afFormData = resultObj.data.data;
            const formData = new FormData();
            formData.append("dataXml", afFormData);
            resultObj.data.attachments.forEach(attachment => {
                console.log(attachment.name);
                formData.append(attachment.name, attachment.data);
            });
            fetch(endpoint, {
                method: 'POST',
                body: formData
            })
            .then(response => {
                if (response.ok) {
                    console.log("Successfully saved");
                    const fld = guideBridge.resolveNode("$form.confirmation");
                    return "Form data was saved successfully";
                } else {
                    throw new Error('Failed to save form data');
                }
            })
            .catch(error => {
                console.error('Error:', error);
            });
        }
    });
}
```

## Server Side Code

The following server-side Java code handles the form data processing. This Java servlet in AEM is invoked via an XHR call in the JavaScript function above.

```java
package com.azuredemo.core.servlets;

import com.adobe.aemfd.docmanager.Document;
import org.apache.sling.api.SlingHttpServletRequest;
import org.apache.sling.api.SlingHttpServletResponse;
import org.apache.sling.api.request.RequestParameter;
import org.apache.sling.api.servlets.SlingAllMethodsServlet;
import org.apache.sling.servlets.annotations.SlingServletResourceTypes;
import org.osgi.service.component.annotations.Component;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import javax.servlet.Servlet;
import javax.servlet.http.HttpServletResponse;
import java.io.File;
import java.io.IOException;
import java.io.Serializable;
import java.util.List;

@Component(
   service = {
      Servlet.class
   }
)
@SlingServletResourceTypes(
   resourceTypes = "azure/handleFormSubmission",
   methods = "POST",
   extensions = "json"
)
public class StoreFormSubmission extends SlingAllMethodsServlet implements Serializable {
   private static final long serialVersionUID = 1L;
   private final transient Logger log = LoggerFactory.getLogger(this.getClass());

   protected void doPost(SlingHttpServletRequest request, SlingHttpServletResponse response) throws IOException {
      List<RequestParameter> listOfRequestParameters = request.getRequestParameterList();
      log.debug("The size of the list is " + listOfRequestParameters.size());
      
      for (int i = 0; i < listOfRequestParameters.size(); i++) {
         RequestParameter requestParameter = listOfRequestParameters.get(i);
         log.debug("Is this request parameter a form field?" + requestParameter.isFormField());
         
         if (!requestParameter.isFormField()) {
            Document attachmentDOC = new Document(requestParameter.getInputStream());
            attachmentDOC.copyToFile(new File(requestParameter.getName()));
         } else {
            log.debug("Not a form field " + requestParameter.getName());
            log.debug(requestParameter.getString());
         }
      }
      
      response.setStatus(HttpServletResponse.SC_OK);
   }
}
```