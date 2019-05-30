---
title: Using Annotations in AEM Assets
seo-title: Using Annotations in AEM Assets
description: AEM Assets provides annotation capabilities to allow users to collaborate and review an individual asset. Users can set preferences for annotation colors to more easily differentiate between users. Print capabilities are available for offline review.
seo-description: AEM Assets provides annotation capabilities to allow users to collaborate and review an individual asset. Users can set preferences for annotation colors to more easily differentiate between users. Print capabilities are available for offline review.
uuid: 9d1e411e-f602-4a76-9c67-fbe372fbb73e
products: SG_EXPERIENCEMANAGER/6.3/ASSETS
products: SG_EXPERIENCEMANAGER/6.4/ASSETS
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: collaboration
discoiquuid: 148164ea-d4bc-4314-93ac-6af26c6dee9d
targetaudience: target-audience new
---

# Using Annotations in AEM Assets{#using-annotations-in-aem-assets}

AEM Assets provides annotation capabilities to allow users to collaborate and review an individual asset. Users can set preferences for annotation colors to more easily differentiate between users. Print capabilities are available for offline review.

>[!VIDEO](https://video.tv.adobe.com/v/16435/?quality=9)

>[!NOTE]
>
>The above video was recorded using AEM 6.3. The same features and capabilities are available in AEM 6.4 and AEM 6.5.

## Annotation Features

* User can choose different color for annotation to easily distinguish from other users
* Print feature is available on any asset which has been annotated for offline review.
* A PDF output is generated for review purposes
* By default, all annotations are printed.
* User can choose to print selected annotations using the check boxes in timeline
* PDF output can be modified by custom configuration

## PDF annotation sling:OsgiConfig definition {#pdf-annotation-sling-osgiconfig-definition}

To customize PDF annotations, create a **sling:OsgiConfig** node in your AEM project under

**/apps/my-project/config.author/com.day.cq.dam.core.impl.annotation.pdf.AnnotationPdfConfig.xml** and adjust the values as needed.

```java
<?xml version='1.0' encoding='UTF-8'?>
<jcr:root xmlns:sling='http://sling.apache.org/jcr/sling/1.0' xmlns:jcr='http://www.jcp.org/jcr/1.0'
    jcr:primaryType='sling:OsgiConfig'
    cq.dam.config.annotation.pdf.document.padding.vertical='{Long}20'
    cq.dam.config.annotation.pdf.reviewStatus.color.changesRequested='fad269'
    cq.dam.config.annotation.pdf.document.height='{Long}792'
    cq.dam.config.annotation.pdf.document.width='{Long}612'
    cq.dam.config.annotation.pdf.reviewStatus.width='{Long}150'
    cq.dam.config.annotation.pdf.font.size='{Long}7'
    cq.dam.config.annotation.pdf.font.color='3B3B3B'
    cq.dam.config.annotation.pdf.font.light='A4A4A4'
    cq.dam.config.annotation.pdf.reviewStatus.color.rejected='fa7d73'
    cq.dam.config.annotation.pdf.minImageHeight='{Long}100'
    cq.dam.config.annotation.pdf.reviewStatus.color.approved='009933'
    cq.dam.config.annotation.pdf.marginTextImage='{Long}14'
    cq.dam.config.annotation.pdf.document.padding.horizontal='{Long}20'
    cq.dam.config.annotation.pdf.annotationMarker.width='{Long}5'/>
```

Download [Asset PDF Annotations sling:OsgiConfig XML](assets/com.day.cq.dam.core.impl.annotation.pdf.annotationpdfconfig.xml)
