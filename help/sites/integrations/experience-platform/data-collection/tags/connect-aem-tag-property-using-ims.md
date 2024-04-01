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
duration: 72
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
