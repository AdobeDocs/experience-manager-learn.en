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

>[!TIP]
>
> When opening metadata export CSV file in Excel, use the [Excel importer](https://support.microsoft.com/en-us/office/import-data-from-a-csv-html-or-text-file-b62efe49-4d5b-4429-b788-e1211b5e90f6) rather than double-clicking the file to avoid issues with UTF-8 encoded CSV files.
>
> To open the metadata export CSV file in Excel, follow these steps:
> 
> 1. Open Microsoft Excel 
> 1. Select __File > New__ to create an empty spreadsheet
> 1. With the empty spreadsheet open, select __File > Import__
> 1. Select __Text__ file and click __Import__
> 1. Select the exported CSV file from the file system and click __Get Data__
> 1. On step 1 of the import wizard, select __Delimited__ and set __File origin__ to __Unicode (UTF-8)__, and click __Next__
> 1. On step 2, set the __Delimiters__ to __Comma__, and click __Next__
> 1. On step 3, leave the __Column data format__ as is, and click __Finish__
> 1. Select __Import__ to add the data to spreadsheet 

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
