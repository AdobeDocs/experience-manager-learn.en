---
title: Create Acrobat Sign Cloud Configuration Cloud Service
description: Create the AEM Forms and Acrobat Sign integration using the cloud services configuration.
solution: Experience Manager,Experience Manager Forms
type: Documentation
role: Developer
level: Beginner, Intermediate
version: Experience Manager as a Cloud Service
feature: Adaptive Forms
topic: Development
jira: KT-7428
thumbnail: 332437.jpg
badgeIntegration: label="Integration" type="positive"
badgeVersions: label="AEM Forms as a Cloud Service" before-title="false"
exl-id: a55773a5-0486-413f-ada6-bb589315f0b1
duration: 222
TQID: https://experienceleague.adobe.com/-QChnfDACdq-vEtqwIMr2aQh8rbgtdTCTOM1iTqg4mk
product_v2:
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
    internal-label: Troubleshooting
---
# Create Acrobat Sign Cloud Configuration

Cloud services configuration in AEM allows you to create integration between AEM and other cloud applications.

The following video will walk you through the steps needed to create cloud services configuration to integrate AEM with Acrobat Sign

>[!VIDEO](https://video.tv.adobe.com/v/332437?quality=12&learn=on)

## Troubleshooting

If you get an error in configuring the Abobe Sign cloud clonfiguration, the following steps can be taken to trouble shoot
* Make sure the re-direct url specified in the Acrobat Sign API application is in the following format
 &lt;your instance name&gt;/libs/adobesign/cloudservices/adobesign/createcloudconfigwizard/cloudservices.html/conf/&lt;container&gt;.
For example - https://author-p24107-e32034.adobeaemcloud.com/libs/adobesign/cloudservices/adobesign/createcloudconfigwizard/cloudservices.html/conf/FormsCS. FormsCS is the name of the container that is going to hold the cloud configuration
* Make sure the oAuth url is correct
* Check your Client Id and Client Secret
* Try incognito window mode

