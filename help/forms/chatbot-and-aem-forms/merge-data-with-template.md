---
title: Merge data with the XDP template
description: Create PDF document by merging data with the template
feature: Adaptive Forms
version: Experience Manager 6.5
jira: KT-15344
topic: Development
role: User
level: Intermediate
exl-id: 6a865402-db3d-4e0e-81a0-a15dace6b7ab
duration: 15
TQID: https://experienceleague.adobe.com/wvErOBv6LG31imk-HKk6kz4MMaseG6QrPh7DtC4H034
product_v2:
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
---
# Merge data with the XDP template

The next step is to merge the XML data with the template to generate the PDF. This PDF is then sent for signatures using Adobe Sign.

## Using OutputService to generate the PDF

The [generatePDF](https://developer.adobe.com/experience-manager/reference-materials/6-5/forms/javadocs/com/adobe/fd/output/api/OutputService.html#generatePDFOutput-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-com.adobe.fd.output.api.PDFOutputOptions-) method of the OutputService was used to generate the PDF.
The generated PDF was then sent for signatures using the Adobe Sign REST API.
