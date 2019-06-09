---
title: Generating Print Channel Documents Using Watched Folder
seo-title: Generating Print Channel Documents Using Watched Folder
description: This is part 10 of multistep tutorial for creating your first interactive communications document for the print channel. In this part, we will generate print channel documents using the watched folder mechanism.
seo-description: This is part 10 of multistep tutorial for creating your first interactive communications document for the print channel. In this part, we will generate print channel documents using the watched folder mechanism.
uuid: 9e39f4e3-1053-4839-9338-09961ac54f81
contentOwner: gbedekar
discoiquuid: 23fbada3-d776-4b77-b381-22d3ec716ae9
index: y
internal: n
snippet: y
---

# Generating Print Channel Documents Using Watched Folder{#generating-print-channel-documents-using-watched-folder}

This is part 10 of multistep tutorial for creating your first interactive communications document for the print channel. In this part, we will generate print channel documents using the watched folder mechanism.

After creating and testing your print channel document, we need a mechanism to generate these document in batch mode or on demand. Typically, these kinds of documents are generated in batch mode and the most common mechanism is using watched folder.

When you configure a watched folder in AEM, you associate an ECMA script or java code that gets executed when a file is dropped into the watched folder. In this article, we will focus on ECMA script which will generate print channel documents and save them to the file system.

The watched folder configuration and the ECMA script is provided as part of this article  assets .

The input file that is dropped into the watched folder has the following structure. The ECMA script reads the account numbers and generates print channel document for each of these accounts.

For more details on the ECMA script for generating documents, [refer to this article](https://helpx.adobe.com/experience-manager/kt/forms/using/generating-interactive-communications-print-document-using-api-tutorial-use.html)

```xml
<accountnumbers>
 <accountnumber>509840</accountnumber>
 <accountnumber>948576</accountnumber>
 <accountnumber>398762</accountnumber>
 <accountnumber>291723</accountnumber>
 <accountnumber>291724</accountnumber>
 <accountnumber>291725</accountnumber>
 <accountnumber>291726</accountnumber>
 <accountnumber>291727</accountnumber>
</accountnumbers>
```

To generate print channel document using the watched folder mechanism, please follow the steps below:

* Download and import the first file into AEM using the package manager. This file has service user bundle which is needed to generate the print channel document using watched folder.
* [Create a system user called data.](http://localhost:4502/crx/explorer/index.jsp) Make sure you are logged in as admin to create the system user
* Make sure this system user has** read** permissions on the following node. To give the permissions [login to user admin](http://localhost:4502/useradmin) and search for the system user "data" and give the read permissions on the following node by tabbing to the permissions tab

*

    * **/content/dam/  formsanddocuments **
    * **/content/dam/  formsanddocuments -  fdm **
    * **/content/forms/af**

* Navigate to /etc/  fd /  watchfolder /scripts/PrintPDF.ecma

* Make sure the path to interactiveCommunicationsDocument is pointing to the correct document that you want to print  .( Line 1)
* Make a note of the saveLocation(Line 2)  .You  can change it as per your needs.
* Make sure the input parameter to the Form Data Model is bound to the Request Attribute and its binding value is set to "  accountnumber ". Refer to the screenshot below.
* Drop the  accountnumbers .  xml  file into the C:\RenderPrintChannel\input

* Check the pdf files in the  save  location as specified in the ECMA script.

![](assets/requestattributeprintchannel.gif) 
Service User Bundle

[Get File](assets/serviceuserbundle.zip)

Account Numbers.xml file that needs to be dropped into the watched folder

[Get File](assets/accountnumbers.xml)
