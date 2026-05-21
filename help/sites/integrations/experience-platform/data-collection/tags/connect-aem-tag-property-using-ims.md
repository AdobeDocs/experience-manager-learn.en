---
title: Connect AEM Sites with Tag Property using IMS
description: Learn how to connect AEM Sites with Tag Property using IMS configuration in AEM.
solution: Experience Manager, Data Collection, Experience Platform
jira: KT-5981
thumbnail: 38555.jpg
topic: Integrations
feature: Integrations
role: Developer
level: Intermediate
badgeIntegration: label="Integration" type="positive"
badgeVersions: label="AEM Sites as a Cloud Service, AEM Sites 6.5" before-title="false"
doc-type: Tutorial
exl-id: 92dbd185-bad4-4a4d-b979-0d8f5d47c54b
duration: 50
TQID: https://experienceleague.adobe.com/Tn5hNOXtgc8fRdsKtyCXfhSZP9-tWDbjCv8lTHkQsb4
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
    internal-label: Experience Platform
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: a01bfd36-4ab8-4bf8-9dc0-5b45b890552e
    internal-label: APIs
  - id: ae478996-b206-4712-9b0c-dc78a2644453
    internal-label: Integrations
  - id: e08599ea-8888-4294-ba74-3ba0a7762a46
    internal-label: Data collection
  - id: ed0d8d0e-04b9-4326-be72-a0fbca265377
    internal-label: Integrations
subfeature_v2:
  - id: d9830f6f-ceb6-4faa-9744-f281fe4439f9
    internal-label: Tags
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
topic_v2:
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
    internal-label: Security
  - id: d3cdead0-685a-4489-9250-4bb709942f66
    internal-label: Data collection
---
# Connect AEM Sites with Tag Property using IMS{#connect-aem-and-tag-property-using-ims}

Learn how to connect AEM with tags Property using the IMS (Identity Management System) configuration in AEM. This setup authenticates AEM with the tags API and allows AEM to communicate via the tags APIs to access Tag properties.

## Create or reuse IMS configuration

The IMS configuration using the Adobe Developer Console project is required to integrate AEM with newly created Tag Property. This configuration allows AEM to communicate with Tags application using tags APIs and IMS handles the security aspect of this integration.

Whenever a AEM as Cloud Service environment is provisioned a few IMS configurations such as Asset Compute, Adobe Analytics, and tags are automatically created. The auto created **tags in Adobe Experience Platform** IMS configuration can be used or a new IMS configuration should be created if you are using AEM 6.X environment.

Review auto created **tags in Adobe Experience Platform** IMS configuration using following steps.

1.  In AEM Author open the **Tools** menu
1.  In the Security section, select Adobe IMS Configurations.
1.  Select the **Adobe Launch** card and click **Properties**, review the details from **Certificate** and **Account** tabs. Then click **Cancel** to return without modifying any auto created details.
1.  Select the **Adobe Launch** card and this time click **Check Health**, you should see the **Success** message like below.

    ![Tags Healthy IMS Configuration](assets/adobe-launch-healthy-ims-config.png)

## Next Steps

[Create a tags Cloud Service configuration in AEM](create-aem-launch-cloud-service.md)
