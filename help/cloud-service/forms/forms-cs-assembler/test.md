---
title: Test the Forms assembler solution
description: Run the ExecuteAssemblerService.java to test the solution
type: Documentation
role: Developer
level: Beginner, Intermediate
version: Cloud Service
feature: Adaptive Forms
topic: Development
exl-id: 5139aa84-58d5-40e3-936a-0505bd407ee8
---
# Import Eclipse Project

* Download and unzip the [zip file](./assets/pdf-manipulation.zip)
* Launch Eclipse and import the project into Eclipse
* The project includes the following folders in the resources folder:
    * ddxFiles - This folder contains the ddx file to describe the output you want to generate
    * pdffiles - This folder contains the pdf files you want to assemble and pdf files to test PDFA utitilites
    * credentials - This folder contains pdfa-options.json file

![resources-file](./assets/resources.png)

## Test Assembling PDF Files

* Copy and paste your service credentials in the service_token.json resource file in the project. 
* Open the AssemblePDFFiles.java file and specify the folder in which you want to save the generated PDF files
* Open ExecuteAssemblerService.java. Set the value of the variable _AEM_FORMS_CS_ to point to your instance.
* Uncomment the appropriate lines to test assembling two or more PDF files
* Run the ExecuteAssemblerService.java as java application

### Test PDFA utilities

* Copy and paste your service credentials in the service_token.json resource file in the project. 
* Open the PDFAUtilities.java file and specify the folder in which you want to save the generated PDF files.
* Open ExecuteAssemblerService.java. Set the value of the variable _AEM_FORMS_CS_ to point to your instance.
* Uncomment the appropriate lines to test PDFA operations.
* Run the ExecuteAssemblerService.java as java application.



>[!NOTE]
> The very first time you run the java program you will get HTTP 403 error. To get past this make sure you give the [appropriate permissions to the technical account user in AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html?lang=en#configure-access-in-aem).

**AEM Forms Users** is the role I have used for this course.
