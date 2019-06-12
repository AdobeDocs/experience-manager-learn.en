---
title: Using Table Component in AEM Forms Print Channel Document
seo-title: Using Table Component in AEM Forms Print Channel Document
description: The following video walks through the steps required to use table component in Interactive Communications for print channel documents.
seo-description: The following video walks through the steps required to use table component in Interactive Communications for print channel documents.
uuid: caec462c-e730-4bdc-9603-41fe0070a8df
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: correspondence-management
topic-tags: forms
discoiquuid: a4605994-dfbb-449f-bee6-26461bc9a667
index: y
internal: n
snippet: y
---

# Using Table Component in AEM Forms Print Channel Document{#using-table-component-in-aem-forms-print-channel-document}

The following video walks through the steps required to use table component in Interactive Communications for print channel documents.

>[!VIDEO](https://video.tv.adobe.com/v/21415/?quality=9)

Tables are used to display data in a tabular manner. The rows in the table need to grow or shrink depending on the data returned by the data source. To use a table in print channel document, we need to create layout file(xdp file) using AEM Forms Designer. In this layout file, we add the table with the required number of columns. Make sure the column field object type is either TextField or Numeric Field depending on your requirements. For each of the column, fields make sure the data binding is set to Use Name.

To make table dynamic, make sure you have marked the Row as repeating.Once you have defined your table, you will import this xdp into AEM Forms. This xdp will be the basis for creating the layout fragment

To use a table in print channel document, we need to create layout fragment. Layout fragment is a special type of document fragment which is based on xdp. Typically you will use layout fragments for displaying tabular data. To create layout fragment please follow steps below

1. Point your browser to [forms and documents.](/aem/forms.html/content/dam/formsanddocuments) [](http://localhost:4502/aem/forms.html/content/dam/formsanddocuments)

2. Click Create | File Upload.

3. Select the xdp which contains the table.

4. Point your browser to [document fragment](http://localhost:4502/aem/forms/assets.html/content/apps/cm/modules)

5. Select "Create | Layout Fragment"

6. Select the xdp that you uploaded in the earlier step.

**Try it on your own server**

Download the assets file.

Included in the assets associated with this article are the following:

Layout Fragment

Form Data Modal

Interactive Communication Document

Unzip the assets file on to your local drive. Import the following files using package manager into crx.

KTDataModal.zip

ConfigureTableExercise.zip

Configure Tomcat as [described here](https://helpx.adobe.com/experience-manager/kt/forms/using/preparing-datasource-for-form-data-model-tutorial-use.html).

Open the Interactive Communication Document in [edit mode](http://localhost:4502/editor.html/content/forms/af/401kstatement/tablesinprintdocument/channels/print.html).

Add and configure the table to the "Contributions" section.

Preview Interactive Communication Document.

Assets related to this article

[Get File](assets/usingtablesinprintchannel.zip)
