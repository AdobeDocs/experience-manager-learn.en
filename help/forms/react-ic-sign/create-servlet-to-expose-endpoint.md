---
title: Expose endpoint that can be invoked to return the web form url
description: Create AEM servlet to return the web form url
feature: Adaptive Forms,Acrobat Sign
version: Experience Manager 6.4, Experience Manager 6.5
topic: Development
role: Developer
level: Beginner
jira: KT-13099
last-substantial-update: 2023-04-13T00:00:00.000Z
exl-id: 3b7632bd-3820-4c1e-aa3f-8a6a4fc26847
duration: 38
TQID: https://experienceleague.adobe.com/s3HdQtHZEJq92jiSRnJXsVJjXYOQSTj-Igtup5s4duA
product_v2:
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
---
# Create Acrobat Sign Web Form URL

The following code was written to expose a POST endpoint. This endpoint extracts the icTemplateName from the submitted data and returns an Acrobat Sign web form URL for the end user to sign.


```java
package com.acrobatsign.core.servlets;

import java.io.ByteArrayInputStream;
import java.io.InputStream;
import java.io.PrintWriter;
import java.nio.charset.StandardCharsets;

import javax.servlet.Servlet;

import org.apache.commons.io.IOUtils;
import org.apache.sling.api.SlingHttpServletRequest;
import org.apache.sling.api.SlingHttpServletResponse;
import org.apache.sling.api.servlets.SlingAllMethodsServlet;
import org.osgi.service.component.annotations.Component;
import org.osgi.service.component.annotations.Reference;
import org.slf4j.Logger;

import com.acrobatsign.core.PrintChannelDocumentHelperMethods;
import com.google.gson.JsonObject;
import com.google.gson.JsonParser;
@Component(service = {
  Servlet.class
}, property = {
  "sling.servlet.methods=post",
  "sling.servlet.paths=/bin/getwidgeturl"
})
public class GetWidgetUrl extends SlingAllMethodsServlet {
  private static final long serialVersionUID = 1 L;
  private static final Logger log = org.slf4j.LoggerFactory.getLogger(GetWidgetUrl.class);
  @Reference
  PrintChannelDocumentHelperMethods printChannelDocument;
  protected void doPost(SlingHttpServletRequest request, SlingHttpServletResponse response) {
    String jsonString;
    try {

      jsonString = IOUtils.toString(request.getInputStream(), StandardCharsets.UTF_8.name());
      log.debug("####Form Data is  " + jsonString);
      JsonObject jsonObject = JsonParser.parseString(jsonString).getAsJsonObject();
      log.debug("The json object is " + jsonObject.toString());
      String icTemplate = jsonObject.get("icTemplate").getAsString();
      log.debug("The icTemplate is " + icTemplate);

      //InputStream targetStream = IOUtils.toInputStream(jsonObject.toString());
      InputStream targetStream = new ByteArrayInputStream(jsonString.getBytes());
      String widgetURL = printChannelDocument.getPrintChannelDocument(icTemplate, targetStream);
      log.debug("The widget url is " + widgetURL);

      JsonObject jsonResponse = new JsonObject();
      jsonResponse.addProperty("widgetURL", widgetURL);

      PrintWriter out = response.getWriter();
      response.setContentType("application/json");
      response.setCharacterEncoding("utf-8");
      out.println(jsonResponse.toString());
      out.flush();
    } catch (Exception e) {
      
      log.error("Error while getting the widget URL, details are :" + e.getMessage());
    }

  }

}
```

## Next Steps

[Deploy the tutorial assets on your local system](./deploy-assets-on-your-server.md)
