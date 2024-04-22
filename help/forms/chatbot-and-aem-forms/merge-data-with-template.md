---
title: Merge data with the XDP template
description: Create PDF document by merging data with the template
feature: Adaptive Forms
version: 6.5
jira: KT-15344
topic: Development
role: User
level: Intermediate
exl-id: 6a865402-db3d-4e0e-81a0-a15dace6b7ab
---
# Merge data with the XDP template

The next step is to merge the XML data with the template to generate the PDF. This PDF is then sent for signatures using Adobe Sign.

## Using OutputService to generate the PDF

The [generatePDF](https://developer.adobe.com/experience-manager/reference-materials/6-5/forms/javadocs/com/adobe/fd/output/api/OutputService.html#generatePDFOutput-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-com.adobe.fd.output.api.PDFOutputOptions-) method of the OutputService was used to generate the PDF.
The generated PDF was then sent for signatures using the Adobe Sign REST API.
