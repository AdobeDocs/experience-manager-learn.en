---
title: Dynamic Media for transparency and Content Automation batch processing
description: Learn how to use Dynamic Media in AEM to create virtual renditions, manage transparency, and automate image processing for scalable content reuse.
feature: Image Profiles, Viewer Presets
topic: Content Management
role: User
level: Beginner, Intermediate, Experienced
doc-type: Feature Video
duration: 560
last-substantial-update: 2025-05-28T00:00:00.000Z
jira: KT-18197
exl-id: 13a09ad3-bf55-4524-bf43-f1cdad368034
TQID: https://experienceleague.adobe.com/tIBdIg91YI8sVfvL0ppSSxnSUKmMiQxfFAJ-coPnbYs
product_v2:
  - id: d09181b5-a36a-43de-ba01-36641440bc43
    internal-label: Experience Manager Assets
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: a01bfd36-4ab8-4bf8-9dc0-5b45b890552e
    internal-label: APIs
  - id: a45b1e7f-e65f-4cd3-be86-5cec5d9449ef
    internal-label: Content management
  - id: bd0d2470-932c-4269-8eca-6d939b72d9ef
    internal-label: Dynamic Media
subfeature_v2:
  - id: d8e79b3c-92b5-4c4d-a46c-5f16d63a14dc
    internal-label: Viewer presets
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
topic_v2:
  - id: f5c2a4bb-71ca-4d7e-8efd-442250e6ba48
    internal-label: Content reuse
---
# Dynamic Media for transparency and Content Automation batch processing

Learn how to use Dynamic Media in AEM to create virtual renditions, manage transparency, and automate image processing for scalable content reuse.

>[!VIDEO](https://video.tv.adobe.com/v/3459589/?learn=on&enablevpops)


## Example Dynamic Media assets

The following are example Dynamic Media assets and their URLs used in the video.

>[!BEGINTABS]

>[!TAB Image transparency examples]

The following are the Dynamic Media Image Server sample URLs used in the video.

| Preview | Description | Dynamic Media URL |
|-----------|------------------|---------|
| ![Default](https://smartimaging.scene7.com/is/image/DynamicMediaNA/AdobeStock_322150086%20trans?bgc=255,255,255){width="250"}  | Default | [Link](https://smartimaging.scene7.com/is/image/DynamicMediaNA/AdobeStock_322150086%20trans?bgc=255,255,255) |
| ![Composited with seamless background image layer](https://smartimaging.scene7.com/is/image/DynamicMediaNA/AdobeStock_322150086%20trans?&layer=1&src=backdrop5-Camera&size=8500,8500&layer=2&src=AdobeStock_322150086%20trans){width="250"}  | Composited with seamless background image layer | [Link](https://smartimaging.scene7.com/is/image/DynamicMediaNA/AdobeStock_322150086%20trans?&layer=1&src=backdrop5-Camera&size=8500,8500&layer=2&src=AdobeStock_322150086%20trans) |
| ![Red Background](https://smartimaging.scene7.com/is/image/DynamicMediaNA/AdobeStock_322150086%20trans?&layer=1&color=200,50,50&size=8500,8500&layer=2&src=AdobeStock_322150086%20trans){width="250"}  | Red Background | [Link](https://smartimaging.scene7.com/is/image/DynamicMediaNA/AdobeStock_322150086%20trans?&layer=1&color=200,50,50&size=8500,8500&layer=2&src=AdobeStock_322150086%20trans) |
| ![Clipped to oval path](https://smartimaging.scene7.com/is/image/DynamicMediaNA/AdobeStock_322150086%20paths?clipPathE=round&bgc=255,255,255){width="250"}  | Clipped to oval path | [Link](https://smartimaging.scene7.com/is/image/DynamicMediaNA/AdobeStock_322150086%20paths?clipPathE=round&bgc=255,255,255) |


>[!TAB Image path examples]

The following are the Dynamic Media Image Server sample URLs used in the video.

| Preview | Description | Dynamic Media URL |
|-----------|------------------|---------|
| ![Normalized to 80 pixels wide (no transparency)](https://smartimaging.scene7.com/is/image/DynamicMediaNA/AdobeStock_322150086%20paths?wid=800){width="250"}  | Normalized to 80 pixels wide (no transparency){width="250"}  | [Link](https://smartimaging.scene7.com/is/image/DynamicMediaNA/AdobeStock_322150086%20paths?wid=800) |
| ![Crop to Path](https://smartimaging.scene7.com/is/image/DynamicMediaNA/AdobeStock_322150086%20paths?cropPathE=Path%201&wid=800){width="250"}  | Crop to Path | [Link](https://smartimaging.scene7.com/is/image/DynamicMediaNA/AdobeStock_322150086%20paths?cropPathE=Path%201&wid=800) |
| ![Clip to Path](https://smartimaging.scene7.com/is/image/DynamicMediaNA/AdobeStock_322150086%20paths?clipPathE=Path%201&wid=800){width="250"}  | Clip to Path | [Link](https://smartimaging.scene7.com/is/image/DynamicMediaNA/AdobeStock_322150086%20paths?clipPathE=Path%201&wid=800) |
| ![Clip to Path and Crop to path](https://smartimaging.scene7.com/is/image/DynamicMediaNA/AdobeStock_322150086%20paths?clipPathE=Path%201&cropPathE=Path%201&wid=800){width="250"}  | Clip to Path and Crop to path | [Link](https://smartimaging.scene7.com/is/image/DynamicMediaNA/AdobeStock_322150086%20paths?clipPathE=Path%201&cropPathE=Path%201&wid=800) |
| ![Clip to another path](https://smartimaging.scene7.com/is/image/DynamicMediaNA/AdobeStock_322150086%20paths?clipPathE=round&wid=800){width="250"}  | Clip to another path | [Link](https://smartimaging.scene7.com/is/image/DynamicMediaNA/AdobeStock_322150086%20paths?clipPathE=round&wid=800) |
| ![Clip to another path and make red background](https://smartimaging.scene7.com/is/image/DynamicMediaNA/AdobeStock_322150086fullpaths?cropPathE=round&clipPathE=round&bgc=200,50,50&wid=800){width="250"}  | Clip to another path and make red background | [Link](https://smartimaging.scene7.com/is/image/DynamicMediaNA/AdobeStock_322150086fullpaths?cropPathE=round&clipPathE=round&bgc=200,50,50&wid=800) |

>[!ENDTABS]


## Dynamic Media Image Server APIs

* [Dynamic Media Image Serving and Rendering API](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/c-http-protocol-reference)
* [Dynamic Media Snapshot preview](https://snapshot.scene7.com/)
