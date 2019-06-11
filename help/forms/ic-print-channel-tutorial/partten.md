---
title: Generating Print Channel Documents Using Watched Folder
seo-title: Generating Print Channel Documents Using Watched Folder
description: This is part 10 of multistep tutorial for creating your first interactive communications document for the print channel. In this part, we will generate print channel documents using the watched folder mechanism.
seo-description: This is part 10 of multistep tutorial for creating your first interactive communications document for the print channel. In this part, we will generate print channel documents using the watched folder mechanism.

---

# Generating Print Channel Documents Using Watched Folder {#generating-print-channel-documents-using-watched-folder}

In this part, we will generate print channel documents using the watched folder mechanism.

After creating and testing your print channel document, we need a mechanism to generate these document in batch mode or on demand. Typically, these kinds of documents are generated in batch mode and the most common mechanism is using watched folder.

When you configure a watched folder in AEM, you associate an ECMA script or java code that gets executed when a file is dropped into the watched folder. In this article, we will focus on ECMA script which will generate print channel documents and save them to the file system.

The watched folder configuration and the ECMA script are part of the assets you imported at the [beginning of this tutorial](introduction.md)

The input file that is dropped into the watched folder has the following structure. ECMA script reads the account numbers and generates print channel document for each of these accounts.

For more details on the ECMA script for generating documents, [refer to this article](https://helpx.adobe.com/experience-manager/kt/forms/using/generating-interactive-communications-print-document-using-api-tutorial-use.html)

```xml {.line-numbers}
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

* [Create a service user named data as mentioned in this document](/help/forms/adaptive-forms/service-user-tutorial-develop.md)
* Make sure this system user has read permissions on the following node. To give the permissions [login to user admin](https://helpx.adobe.com/useradmin) and search for the system user "data" and give the read permissions on the following node by tabbing to the permissions tab


    * /content/dam/formsanddocuments
    * /content/dam/formsanddocuments-fdm
    * /content/forms/af

* Login to crx and navigate to /etc/fd/watchfolder/scripts/PrintPDF.ecma

* Make sure the path to interactiveCommunicationsDocument is pointing to the correct document that you want to print.( Line 1)
* Make a note of the saveLocation(Line 2).You can change it as per your needs.
* Make sure the input parameter to the Form Data Model is bound to the Request Attribute and its binding value is set to "accountnumber". Refer to the screenshot below.
* Drop the  [accountnumbers.xml](assets/accountnumbers.xml) file into the C:\RenderPrintChannel\input

* Check the pdf files in the save location as specified in the ECMA script.

![request](assets/requestattributeprintchannel.gif) 

Account Numbers.xml file that needs to be dropped into the watched folder


