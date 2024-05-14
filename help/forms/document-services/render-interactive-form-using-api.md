---
title: Rendering Interactive PDF using Forms Services in AEM Forms
description: Using Forms Service API in AEM Forms to render interactive PDF
feature: Forms Service
version: 6.4,6.5
topic: Development
role: Developer
level: Intermediate
exl-id: 9b2ef4c9-8360-480d-9165-f56a959635fb
last-substantial-update: 2020-07-07
duration: 75
---
# Rendering Interactive PDF using Forms Services in AEM Forms

Using Forms Service API in AEM Forms to render interactive PDF

In this article we will take a look at the following service

* FormsService - This is a very versatile service which allows you to export/import data from and into PDF file and also generate interactive pdf by merging xml data into xdp template

The official [javadoc for AEM Forms API is listed here](https://helpx.adobe.com/aem-forms/6/javadocs/com/adobe/fd/output/api/package-summary.html)

The following code snippet renders interactive pdf using the renderPDFForm operation of the FormsService. The schengen.xdp is template that is being used to merge the xml data.

```java
String uri = "crx:///content/dam/formsanddocuments";
PDFFormRenderOptions renderOptions = new PDFFormRenderOptions();
renderOptions.setAcrobatVersion(AcrobatVersion.Acrobat_11);
renderOptions.setContentRoot(uri);
Document interactivePDF = null;
try {
interactivePDF = formsService.renderPDFForm("schengen.xdp", xmlData, renderOptions);
} catch (FormsServiceException e) {
 e.printStackTrace();
}
return interactivePDF;

```

Line 1: Location of the folder which contains the xdp template

Line2-4: Create PDFFormRenderOptions and set its properties

Line 7: Generate Interactive PDF using the renderPDFForm service operation of FormsService

Line 11: Returns the generated interactive pdf to the calling application

**To test the sample package on your system**
1. [Download and install DevelopingWithServiceUserBundle](/help/forms/assets/common-osgi-bundles/DevelopingWithServiceUser.jar)
1. [Download and install the DocumentServices Sample Bundle using the Felix Web Console](/help/forms/assets/common-osgi-bundles/AEMFormsDocumentServices.core-1.0-SNAPSHOT.jar)
1. [Download and install the package using the AEM package manager](assets/downloadinteractivepdffrommobileform.zip)

1. [Login to configMgr](http://localhost:4502/system/console/configMgr)
1. Search for Adobe Granite CSRF Filter
1. Add the following path in the excluded sections and save
1. /bin/generateinteractivepdf
1. Search for _Apache Sling Service User Mapper Service_ and click to open the properties
   1. Click the *+* icon (plus) to add the following Service Mapping
      * DevelopingWithServiceUser.core:getformsresourceresolver=fd-service
   1. Click ' Save '
1. [Open the mobile form](http://localhost:4502/content/dam/formsanddocuments/schengen.xdp/jcr:content)
1. Fill in a couple of fields and then click the ***Download and fill ....*** button
1. The interactive pdf should be downloaded to your local system


The sample package contains the custom profile that is associated with the Mobile Form. Please explore the [customtoolbar.jsp](http://localhost:4502/apps/AEMFormsDemoListings/customprofiles/addImageToMobileForm/demo/customtoolbar.jsp) file. This jsp extracts the data from the mobile form and makes a POST request to servlet mounted on ***/bin/generateinteractivepdf*** path. The servlet return the interactive pdf to the calling application. The code in the customtoolbar.jsp then downloads the file to your local system
