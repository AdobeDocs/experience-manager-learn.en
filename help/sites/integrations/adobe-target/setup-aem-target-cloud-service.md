---
title:  Create Adobe Target Cloud Service account
description: Step by step walkthrough on how to integrate Adobe Experience Manager as a Cloud Service with Adobe Target using Cloud Service and Adobe IMS authentication
feature: cloud-services
topics: integrations, administration, development
audience: administrator, developer
doc-type: technical video
activity: setup
version: cloud-service
kt: 6044
thumbnail: 41244.jpg
---

# Create Adobe Target Cloud Service account {#adobe-target-cloud-service}

Step by step walkthrough on how to integrate Adobe Experience Manager as a Cloud Service with Adobe Target using Cloud Service and Adobe IMS authentication.

>[!VIDEO](https://video.tv.adobe.com/v/41244?quality=12&learn=on)

>[!CAUTION]
>
>There is a known issue with Adobe Target Cloud Services configuration shown in the video. It is recommended instead to follow the same steps in the video but use the [Legacy Adobe Target Cloud Services configuration](https://docs.adobe.com/content/help/en/experience-manager-learn/aem-target-tutorial/aem-target-implementation/using-aem-cloud-services.html).

## Common Issues

When exporting Experience Fragment to Adobe target, if your Target Integration in admin console doesn't have the right permission, you might receive an error as shown below.

**UI Error**
![Target API UI Error](assets/error-target-offer.png)

**Log Error**
![Target API Console Error](assets/target-console-error.png)


**Solution**

1. Navigate to [Admin Console](https://adminconsole.adobe.com/)
2. Select Products > Adobe Target > Product Profile
3. Under Integrations tab, select your Integration (Adobe I/O project)
4. Assign Editor or Approver role. 

![Target API Error](assets/target-permissions.png)

Adding right permission to your Target integration should help you resolve the above issue. 