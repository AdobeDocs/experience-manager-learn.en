---
title: Using PDFG in AEM Forms
description: Demonstrating Drag and Drop capability to create PDF using AEM Forms
feature: PDF Generator
version: 6.4,6.5
topic: Development
role: Developer
level: Intermediate
exl-id: bc79fcbf-b8b3-4d3a-9cd6-0bcd9321c7d5
---
# Using PDFG in AEM Forms{#using-pdfg-in-aem-forms}

Demonstrating Drag and Drop capability to create PDF using AEM Forms

 PDFG  stands for PDF Generation. This means you can convert a variety of file formats into PDF. The most common ones are Microsoft Office documents. PDFG has been part of AEM Forms since 6.1.
 [The javadoc for PDFG API is listed here](https://www.adobe.io/experience-manager/reference-materials/6-5/forms/javadocs/index.html?com/adobe/fd/output/api/OutputService.html)

The assets associated with this article will allow you to drag and drop MS office documents or JPG file into the drop zone of the HTML page. Once the document is dropped, it will invoke the PDFG service and convert the document into PDF and save it on the file system of AEM Server.

To install the demo assets, please perform the following steps

1. Configure PDFG as mentioned in this document [here](https://helpx.adobe.com/experience-manager/6-4/forms/using/install-configure-pdf-generator.html).
1. Please follow the appropriate documentation related to your AEM Forms version.
1. [Import and install assets related to this article using the package manager.](assets/createpdfgdemov2.zip)
1. [Navigate to  post.jsp](http://localhost:4502/apps/AemFormsSamples/components/createPDF/POST.jsp) in your CRX
1. Change the save location as per your preference(line 9)
1. Save your changes.
1. Open the [  html  page](http://localhost:4502/content/DocumentServices/CreatePDFG.html) for dragging and dropping files for conversion.
1. Drop a word file or jpg into the drop zone.
1. The input document will be converted into PDF and saved in the same location as specified in point 4.

The following code snippet shows the usage of PDFG service to convert files to PDF

```java
com.adobe.pdfg.service.api.GeneratePDFService pdfService = sling.getService(com.adobe.pdfg.service.api.GeneratePDFService.class);
System.out.println("Got PDF Service");
java.util.Map map = pdfService.createPDF(uploadedDocument,fileName,"","Standard","No Security", null, null);
```
