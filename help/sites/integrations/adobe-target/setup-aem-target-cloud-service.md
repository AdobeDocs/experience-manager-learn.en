---
title: Create Adobe Target Cloud Service account in AEM
description: Integrate Adobe Experience Manager as a Cloud Service with Adobe Target using Cloud Service and Adobe IMS authentication.
jira: KT-6044
thumbnail: 41244.jpg
topic: Integrations
feature: Integrations
role: Admin
level: Intermediate
badgeIntegration: label="Integration" type="positive"
badgeVersions: label="AEM Sites as a Cloud Service, AEM Sites 6.5" before-title="false"
doc-type: Tutorial
exl-id: dd6c17ae-8e08-4db3-95f9-081cc7dbd86e
duration: 316
---
# Create Adobe Target Cloud Service account {#adobe-target-cloud-service}

The following video provides a walk through on how to connect AEM as a Cloud Service with Adobe Target. 

This integration allows the AEM Author service to communicate directly with Adobe Target, and push Experience Fragments from AEM to Target as offers.  This integration does *not* add Adobe Target JavaScript (AT.js) to AEM Sites web pages, for that integrate [AEM and tags using the Target extension](../experience-platform/data-collection/tags/connect-aem-tag-property-using-ims.md).

>[!WARNING]
>
>The video shows deprecated JWT authentication method to connect AEM to Adobe Target. However, the recommended method is to use the OAuth Server-to-Server authentication method. For more information, see [JWT-To-OAuth credential migration for AEM](https://experienceleague.adobe.com/en/docs/experience-manager-learn/foundation/authentication/jwt-to-oauth-migration.html). We are working on updating the video to reflect this change.


>[!VIDEO](https://video.tv.adobe.com/v/41244?quality=12&learn=on)

>[!CAUTION]
>
>There is a known issue with Adobe Target Cloud Services configuration shown in the video. Until this issue is resolved, follow the same steps in the video but use the [legacy Adobe Target Cloud Services configuration](https://experienceleague.adobe.com/docs/experience-manager-learn/aem-target-tutorial/aem-target-implementation/using-aem-cloud-services.html).
