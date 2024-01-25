---
title: Using API to generate Document of Record with AEM Forms
description: Generate Document Of Record (DOR) programmatically
feature: Adaptive Forms
version: 6.4,6.5
topic: Development
role: Developer
level: Experienced
exl-id: 9a3b2128-a383-46ea-bcdc-6015105c70cc
last-substantial-update: 2023-01-26
duration: 74
---
# Using API to generate Document of Record in AEM Forms {#using-api-to-generate-document-of-record-with-aem-forms}

Generate Document Of Record (DOR) programmatically

This article illustrates the use of the `com.adobe.aemds.guide.addon.dor.DoRService API` to generate **Document of Record** programmatically. [Document of Record](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/generate-document-of-record-for-non-xfa-based-adaptive-forms.html) is a PDF version of the data captured in Adaptive Form.

1. The following is the code snippet. The first line gets the DOR Service.
1. Set the DoROptions.
1. Invoke the render method of the DoRService and pass the DoROptions object to the render method

```java
String dataXml = request.getParameter("data");
System.out.println("Got " + dataXml);
Session session;
com.adobe.aemds.guide.addon.dor.DoRService dorService = sling.getService(com.adobe.aemds.guide.addon.dor.DoRService.class);
System.out.println("Got ... DOR Service");
com.mergeandfuse.getserviceuserresolver.GetResolver aemDemoListings = sling.getService(com.mergeandfuse.getserviceuserresolver.GetResolver.class);
System.out.println("Got aem DemoListings");
resourceResolver = aemDemoListings.getFormsServiceResolver();
session = resourceResolver.adaptTo(Session.class);
resource = resourceResolver.getResource("/content/forms/af/sandbox/1201-borrower-payments");
com.adobe.aemds.guide.addon.dor.DoROptions dorOptions = new com.adobe.aemds.guide.addon.dor.DoROptions();
dorOptions.setData(dataXml);
dorOptions.setFormResource(resource);
java.util.Locale locale = new java.util.Locale("en");
dorOptions.setLocale(locale);
com.adobe.aemds.guide.addon.dor.DoRResult dorResult = dorService.render(dorOptions);
byte[] fileBytes = dorResult.getContent();
com.adobe.aemfd.docmanager.Document dorDocument = new com.adobe.aemfd.docmanager.Document(fileBytes);
resource = resourceResolver.getResource("/content/usergenerated/content/aemformsenablement");
Node paydotgov = resource.adaptTo(Node.class);
java.util.Random r = new java.util.Random();
String nodeName = Long.toString(Math.abs(r.nextLong()), 36);
Node fileNode = paydotgov.addNode(nodeName + ".pdf", "nt:file");

System.out.println("Created file Node...." + fileNode.getPath());
Node contentNode = fileNode.addNode("jcr:content", "nt:resource");
Binary binary = session.getValueFactory().createBinary(dorDocument.getInputStream());
contentNode.setProperty("jcr:data", binary);
JSONWriter writer = new JSONWriter(response.getWriter());
writer.object();
writer.key("filePath");
writer.value(fileNode.getPath());
writer.endObject();
session.save();
```

To try this on your local system, please follow the following steps

1. [Download and install the article assets using package manager](assets/dor-with-api.zip)
1. Make sure you have installed and started the DevelopingWithServiceUser bundle provided as part of [Create Service User article](service-user-tutorial-develop.md)
1. [Login to configMgr](http://localhost:4502/system/console/configMgr)
1. Search for Apache Sling Service User Mapper Service
1. Make sure you the following entry _DevelopingWithServiceUser.core:getformsresourceresolver=fd-service_ in the Service Mappings section
1. [Open the form](http://localhost:4502/content/dam/formsanddocuments/sandbox/1201-borrower-payments/jcr:content?wcmmode=disabled)
1. Fill out the form and click on ' View PDF '
1. You should see DOR in new tab in your browser


**Troubleshooting Tips**

PDF isn't displayed in new browser tab:

1. Make sure you are not blocking popups in your browser
1. Make sure you are starting AEM server as an administrator(at least on windows)
1. Make sure the 'DevelopingWithServiceUser' bundle is in *active state* 
1. [Make sure the system user](http://localhost:4502/useradmin) ' fd-service' has Read, Modify, and Create permissions on the following node `/content/usergenerated/content/aemformsenablement`
