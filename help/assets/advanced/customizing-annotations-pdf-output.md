---
title: Customizing Annotations in AEM Assets
description: AEM Assets format and style when output to PDF can be configued by AEM Developers.
feature: Collaboration
version: Experience Manager 6.4, Experience Manager 6.5
topic: Collaboration
role: Developer
level: Intermediate
last-substantial-update: 2022-06-03T00:00:00.000Z
doc-type: Feature Video
exl-id: 972737dd-8ca6-47b4-a4ec-b73355c09cec
duration: 13
TQID: https://experienceleague.adobe.com/mjgJJ8eUOPycPHmteHiNz3gDZXG3Lfbxz9ikLnUrzXs
product_v2:
  - id: d09181b5-a36a-43de-ba01-36641440bc43
    internal-label: Experience Manager Assets
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
---
# Customizing Annotations in AEM Assets{#using-annotations-in-aem-assets}

AEM supports the customization of the annotation's output to PDF.

## PDF annotation sling:OsgiConfig definition

To customize PDF annotations, create a **sling:OsgiConfig** node in your AEM project under

`/apps/my-project/config.author/com.day.cq.dam.core.impl.annotation.pdf.AnnotationPdfConfig.xml` and adjust the values as needed:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:sling="http://sling.apache.org/jcr/sling/1.0" xmlns:jcr="http://www.jcp.org/jcr/1.0"
    jcr:primaryType="sling:OsgiConfig"

    cq.dam.config.annotation.pdf.document.padding.vertical="{Long}20"
    cq.dam.config.annotation.pdf.reviewStatus.color.changesRequested="fad269"
    cq.dam.config.annotation.pdf.document.height="{Long}792"
    cq.dam.config.annotation.pdf.document.width="{Long}612"
    cq.dam.config.annotation.pdf.reviewStatus.width="{Long}150"
    cq.dam.config.annotation.pdf.font.size="{Long}7"
    cq.dam.config.annotation.pdf.font.color="3B3B3B"
    cq.dam.config.annotation.pdf.font.light="A4A4A4"
    cq.dam.config.annotation.pdf.reviewStatus.color.rejected="fa7d73"
    cq.dam.config.annotation.pdf.minImageHeight="{Long}100"
    cq.dam.config.annotation.pdf.reviewStatus.color.approved="009933"
    cq.dam.config.annotation.pdf.marginTextImage="{Long}14"
    cq.dam.config.annotation.pdf.document.padding.horizontal="{Long}20"
    cq.dam.config.annotation.pdf.annotationMarker.width="{Long}5"
    />
```
