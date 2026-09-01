---
title: Using Metadata Import and Export in AEM Assets
description: Learn how to bulk update asset metadata in AEM Assets with the metadata import and export features.
solution: Experience Manager, Experience Manager Assets
sub-product: Experience Manager Assets
feature-set: Experience Manager Assets
version: Experience Manager 6.4, Experience Manager 6.5, Experience Manager as a Cloud Service
topic: Content Management
feature: Metadata
role: Admin
level: Intermediate
kt: 647, 917
thumbnail: 22132.jpg
team: TM
last-substantial-update: 2026-08-27
doc-type: Feature Video
exl-id: 0681e2c4-8661-436c-9170-9aa841a6fa27
duration: 419
TQID: https://experienceleague.adobe.com/OV-DC4CKLo-ejAyRCnewNL-bbsAt1eSTXDbx5xFa8Cw
product_v2:
  - id: d09181b5-a36a-43de-ba01-36641440bc43
    internal-label: Experience Manager Assets
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: a45b1e7f-e65f-4cd3-be86-5cec5d9449ef
    internal-label: Content management
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
    internal-label: Metadata
---
# Import and export metadata {#metadata-import-and-export}

Import and export let content authors bulk update metadata for existing assets.

>[!BEGINTABS]

>[!TAB Admin view]

## Metadata export {#metadata-export}

>[!VIDEO](https://video.tv.adobe.com/v/22132?quality=12&learn=on)

>[!TIP]
>
> When opening metadata export CSV file in Excel, use the [Excel importer](https://support.microsoft.com/en-us/excel/import-data-from-a-csv-html-or-text-file) rather than double-clicking the file to avoid issues with UTF-8 encoded CSV files.
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

## Metadata import {#metadata-import}

>[!VIDEO](https://video.tv.adobe.com/v/21374?quality=12&learn=on)

>[!NOTE]
>
> When preparing a CSV file to import, it is easier to generate a CSV with the list of assets by using the Metadata Export feature. You can then modify the generated CSV file and import it using the Import feature. 

## Metadata CSV file format {#metadata-file-format}

### First row

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
* All valid [JCR Property types](https://developer.adobe.com/experience-manager/reference-materials/spec/javax.jcr/javadocs/jcr-2.0/javax/jcr/PropertyType.html) are supported  

* Multi Value Property format - `<metadata property name> {{<property type : MULTI }}`

### Second row to N rows

* The first column holds the absolute JCR path for an asset. For example: /content/dam/asset1.jpg
* Metadata property for an asset could have missing values in the CSV file. Missing metadata properties for that particular asset are not updated.

>[!ENDTABS]
