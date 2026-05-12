---
title: Using Table Component in AEM Forms Print Channel Document
description: The following video walks through the steps required to use table component in Interactive Communications for print channel documents.
feature: Interactive Communication
doc-type: technical video
version: Experience Manager 6.4, Experience Manager 6.5
topic: Development
role: Developer
level: Intermediate
exl-id: 54afd047-c6e6-4557-9336-39420f30df88
last-substantial-update: 2019-07-07T00:00:00.000Z
duration: 277
TQID: https://experienceleague.adobe.com/aN8Rhwxy-l3qBh8WPD9zXqsXiFdaUoyIxDflNF5pOkg
product_v2:
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
---
# Using Table Component in AEM Forms Print Channel Document {#using-table-component-in-aem-forms-print-channel-document}

The following video walks through the steps required to use table component in Interactive Communications for print channel documents.

>[!VIDEO](https://video.tv.adobe.com/v/27769?quality=12&learn=on)

Tables are used to display data in tabular manner. The rows in the table need to grow or shrink depending on the data returned by the data source. To use a table in print channel document, we need to create layout file(xdp file) using AEM Forms Designer. In this layout file, we add the table with the required number of columns. Make sure the column field object type is either TextField or Numeric Field depending on your requirements. For each of the column, fields make sure the data binding is set to Use Name.

>[!NOTE]
>
>To make table dynamic, make sure you have marked the Row as repeating.

**Try it on your own server**

* [Download and unzip the assets file on to your hard drive](assets/usingtablesinprintchannel.zip)

* Import the two zip files into AEM using package manager 

* Included in the assets associated with this article are the following:

    * Layout Fragment

    * Form Data Modal

    * Interactive Communication Document
    * sampleretirementaccountdata.json

* Open the Interactive Communication Document in [edit mode](http://localhost:4502/editor.html/content/forms/af/401kstatement/tablesinprintdocument/channels/print.html).

* Add the TableDemo layout fragment to the contributions section.
* Bind the table cells to the appropriate Form Data Model elements as shown in the video

* Preview Interactive Communication Document with the sample json data file provided to you
