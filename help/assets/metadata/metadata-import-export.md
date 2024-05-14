---
title: Using Metadata Import and Export in AEM Assets
description: Learn how to use the import and export metadata features of Adobe Experience Manager Assets. The import and export capabilities allow content authors to bulk update metadata for existing assets.
version: 6.4, 6.5, Cloud Service
topic: Content Management
feature: Metadata
role: Admin
level: Intermediate
kt: 647, 917
thumbnail: 22132.jpg
last-substantial-update: 2022-06-13
doc-type: Feature Video
exl-id: 0681e2c4-8661-436c-9170-9aa841a6fa27
duration: 419
---
# Using Metadata Import and Export in AEM Assets {#metadata-import-and-export}

Learn how to use the import and export metadata features of Adobe Experience Manager Assets. The import and export capabilities allow content authors to bulk update metadata for existing assets.

## Metadata Export {#metadata-export}

>[!VIDEO](https://video.tv.adobe.com/v/22132?quality=12&learn=on)

## Metadata Import {#metadata-import}

>[!VIDEO](https://video.tv.adobe.com/v/21374?quality=12&learn=on)

>[!NOTE]
>
> When preparing a CSV file to import, it is easier to generate a CSV with the list of assets by using the Metadata Export feature. You can then modify the generated CSV file and import it using the Import feature.

## Metadata CSV File Format {#metadata-file-format}

### First Row

* The first row of the CSV file defines the metadata schema.
* The First column defaults to `assetPath`, which holds the absolute JCR Path for an asset.

* Subsequent columns in the first-row point to other metadata properties of an asset.
  * For example : `dc:title, dc:description, jcr:title`

* Single Value Property format

  * `<metadata property name> {{<property type}}`
  * If property type is not specified, it defaults to String.
  * For example: `dc:title {{String}}`

* Property Name is case-sensitive
  * Correct : `dc:title {{String}}`
  * Incorrect: `Dc:Title {{String}}`

* Property Type is case insensitive
* All valid [JCR Property types](https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/PropertyType.html) are supported  

* Multi Value Property format - `<metadata property name> {{<property type : MULTI }}`

### Second Row to N rows

* The first column holds the absolute JCR path for an asset. For example: /content/dam/asset1.jpg
* Metadata property for an asset could have missing values in the CSV file. Missing metadata properties for that particular asset are not updated.
