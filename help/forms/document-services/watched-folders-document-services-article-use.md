---
title: Using Watched Folders in AEM Forms
description: Configure and use watched folders in AEM Forms
feature: Output Service
version: 6.4,6.5
topic: Development
role: Developer
level: Intermediate
exl-id: abb74d44-d1b9-44d6-a49f-36c01acfecb4
last-substantial-update: 2020-07-07
duration: 86
---
# Using Watched Folders in AEM Forms{#using-watched-folders-in-aem-forms}

An administrator can configure a network folder, known as a Watched Folder, so that when a user places a file (such as a PDF file) in the Watched Folder a pre-configured workflow, service, or script operation is started to process the added file. After the service performs the specified operation, it saves the result file in a specified output folder. For more information about workflow, service, and script.

To learn more about creating a watched folder, [click here](https://helpx.adobe.com/experience-manager/6-4/forms/using/Creating-Configure-watched-folder.html)

Watched Folders are used to generate documents in batch mode. Using watched folder mechanism, you can generate Interactive Communications for the print channel, or use output service to merge data with the template.

This article will cover the use case of merging data with a template using the output service via watched folder mechanism.

Output service is an OSGi service that is part of AEM Document Services. Output service supports various output formats and output design features of AEM Forms Designer. Output service can convert XFA templates and XML data to generate print documents in various formats.

To learn more about the output service, [please click here](https://helpx.adobe.com/aem-forms/6/output-service.html).
To set up watched folder on your system, please follow the steps below:
* [Download and extract the contents of the zip file](assets/outputservicewatchedfolderkt.zip).This zip file contains package for creating watched folder and sample files to test the output service using watched folder mechanism
  * Windows System

      * Import the outputservicewatchedfolder.zip into AEM using package manager
     * This creates a watched folder called outputservicewatchedfolder on your C drive.
  * Non Windows System
    * [Open the configuration setting of the watched folder](http://localhost:4502/crx/de/index.jsp#/etc/fd/watchfolder/config/outputservice)
    * Set the folder path property of the outservice node to point to a suitable location
    * Save your changes
    * The location mentioned above is your watched folder.

Drop the SamplePdfFile and SampleXdpFile folders into the input folder of the watched folder. On successful processing of the files, the results are placed under the results folder of your watched folder.


>[!NOTE]
>
>If the script associated with watched folder needs more than one file, you need to create a folder and place all the required files in the folder and drop the folder into the input folder of your watched folder.
>
>If the script associated with watched folder needs only one input file, you can drop the file directly into the input folder of your watched folder
