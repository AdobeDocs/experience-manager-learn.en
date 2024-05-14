---
title: Adobe Asset Link and AEM
description: Adobe Experience Manager assets can be used by designers and creative users within their favorite Adobe Creative Cloud desktop applications. Adobe Asset Link extension for Adobe Creative Cloud for enterprise extends the capability to search and browse, sort, preview, upload assets, check out, modify, check-in, and view metadata of AEM assets within Creative Cloud tools like Adobe XD, Photoshop, InDesign, and Illustrator.
feature: Adobe Asset Link
version: 6.4, 6.5, Cloud Service
topic: Content Management
role: User
level: Beginner
thumbnail: 28988.jpg
jira: KT-8413, KT-3707
last-substantial-update: 2022-06-25
doc-type: Feature Video
exl-id: 6c49f8c2-f468-4b29-b7b6-029c8ab39ce9
duration: 1027
---
# Adobe Asset Link 3.0

Adobe Experience Manager assets can be used by designers and creative users within their favorite Adobe Creative Cloud desktop applications. 

Adobe Asset Link extension for Adobe Creative Cloud for enterprise extends the capability to search and browse, sort, preview, upload assets, check out, modify, check-in and view metadata of AEM assets within Creative Cloud applications.

>[!TIP]
>
> Learn more about how the [Adobe XD Premium Training Program](https://helpx.adobe.com/support/xd.html) can help you integrate Asset Link with your Adobe Experience Manager workflow.

## Adobe Asset Link and AEM creative workflows

The following video illustrates a common workflow used by creatives working in Adobe Creative Cloud applications, and integrating directly with AEM using Adobe Asset Link.

>[!VIDEO](https://video.tv.adobe.com/v/335927?quality=12&learn=on)

## Adobe Asset Link capabilities

+ Adobe Asset Link integrates with AEM Assets and Assets Essentials.
+ Adobe Asset Link auto-configures connection to cloud-based AEM environments (AEM Assets as a Cloud Service and Assets Essentials)
+ Adobe Asset Link is an extension that works within Adobe Creative Cloud applications:

    + Adobe XD
    + Adobe Photoshop
    + Adobe Illustrator
    + Adobe InDesign

+ Automatic authentication to AEM using their Adobe Enterprise ID or Federated ID
+ Browse and search for digital assets in AEM
+ Access file details for assets residing in AEM from with the panel:
    + Thumbnail
    + Basic metadata
    + Versions
+ Place, download or drag-n-drop assets into their layout
+ Modify assets by checking them out from AEM and working on them (WIP) within their Creative Cloud Assets account
+ Check an asset back into AEM after they have finished modifying it, and the new version is reflected in AEM
+ Search for assets in AEM from the Adobe Asset Link In-App panel
+ Browse AEM Assets collections and smart collections directly from the Asset Link panel
+ Add newly created assets to AEM directly from the panel
+ Drag-and-drop assets directly into InDesign frames

## Placing assets in InDesign

Adobe Asset Link provides InDesign direct linking support between Adobe Asset Link and AEM. With InDesign direct linking support, you can place (__Place Linked__ or __Place Copy__) or drag-n-drop digital assets into InDesign from AEM via the Adobe Asset Link panel. Also, introduces the *For Placement Only+ (FPO) rendition.

>[!VIDEO](https://video.tv.adobe.com/v/28988?quality=12&learn=on)

>[!NOTE]
>
>Use your Adobe Creative Cloud Enterprise ID or Federated ID only. Make sure you [configure AEM for Adobe Asset Link](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html).

You can place an asset to your InDesign layout using one of the below options:

+ **Place Copy** - Embedding an asset (using the Place Copy option) places a copy of the original asset into your InDesign layout after downloading the binaries to your local system. Adobe Asset Link does not maintain any link between the embedded copy and the original asset. If the original asset is modified in AEM, you must delete the embedded asset from the InDesign file, and re-embed the asset from AEM.

+ **Place Linked** - When working with InDesign documents, you have the option to reference the assets from AEM in addition to directly embedding the assets (using the Place Copy option in the context menu). Referencing assets lets you collaborate with other users and incorporate any updates made to the original asset in AEM. To reference an asset from AEM, use the Place Linked option in the context menu.

### For Placement Only images

When large asset files are placed into InDesign Documents from AEM using Adobe Asset Link, creatives users need to wait for few seconds after initiating the place operation. This impacts the overall user experience. With Adobe Asset Link you can temporarily place a low resolution image of the original asset from AEM, thereby reducing the time taken to place an image. At the same time, it increases the overall user experience and productivity. The lower resolution image is placed temporarily and when the final output is required for printing or publishing, you need to replace the FPO renditions with the originals. If you want to replace multiple FPO images with respective original images, navigate to **_Windows > Links_** panel and then download the original assets. After the original images are downloaded, choose Replace all FPO's With Originals.

FPO renditions are lightweight substitutes of the original assets. They have the same aspect ratio, but are of smaller size compared to the original images. Currently, InDesign supports importing FPO renditions for the following image types only:

+ JPEG
+ GIF
+ PNG
+ TIFF
+ PSD
+ BMP

If an FPO rendition is not available for a specific asset in AEM, the original high-resolution asset is referenced instead. For FPO images, the status FPO is displayed in the InDesign Links panel.

## Adobe Asset Link authentication with AEM Assets

How Adobe Asset Link authentication works in the context of Adobe Identity Management Services (IMS) and Adobe Experience Manager Author.

![Adobe Asset Link Architecture](assets/adobe-asset-link-article-understand.png)

1. The Adobe Asset Link extension makes an authorization request, via the Adobe Creative Cloud Desktop App, to Adobe Identity Manage Service (IMS), and upon success, receives a Bearer token.
1. Adobe Asset Link extension connects to AEM Author over HTTP(S), including the Bearer token obtained in **Step 1**, using the scheme (HTTP/HTTPS), host and port provided in the extension's settings JSON.
1. AEM's Bearer Authentication Handler extracts the Bearer token from the request and validates it with Adobe IMS.
1. Once Adobe IMS validates the Bearer token, a user is created in AEM (if it doesn't already exist), and syncs profile and group/memberships data from Adobe IMS. The AEM user is issued a standard AEM login token, which is sent back to the Adobe Asset Link extension as a Cookie on the HTTP(S) response.
1. Subsequent interactions (ie. browsing, searching, checking in/out assets, etc.) with the Adobe Asset Link extension results in HTTP(S) requests to AEM Author which are validated using the AEM login token, using the standard AEM Token Authentication Handler.

>[!NOTE]
>
>Upon expiry of login token, **Steps 1-5** will automatically invoke, authenticating the Adobe Asset Link extension using the Bearer token, and re-issues a new, valid login token.

## Additional resources

+ [Adobe Asset Link website](https://www.adobe.com/creativecloud/business/enterprise/adobe-asset-link.html)
