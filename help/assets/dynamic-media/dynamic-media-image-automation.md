---
title: Dynamic Media for transparency and Content Automation batch processing
description: Learn how to use Dynamic Media in AEM to create virtual renditions, manage transparency, and automate image processing for scalable content reuse.
feature: Image Profiles, Viewer Presets
topic: Content Management
role: User
level: Beginner, Intermediate, Experienced
doc-type: Feature Video
duration: 560
last-substantial-update: 2025-05-28
jira: KT-18197
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
