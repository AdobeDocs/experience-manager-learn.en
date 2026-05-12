---
title: Integrate Tags in Adobe Experience Platform
description: Learn how to integrate AEM as a Cloud Service with Tags in Adobe Experience Platform. The integration allows you to deploy the Adobe Web SDK and inject custom JavaScript for data collection and personalization into your AEM pages.
version: Experience Manager as a Cloud Service
feature: Personalization, Integrations
topic: Personalization, Integrations, Architecture, Content Management
role: Developer, Leader, User
level: Beginner
doc-type: Tutorial
last-substantial-update: 2025-08-07T00:00:00.000Z
jira: KT-18719
thumbnail: null
exl-id: 71cfb9f5-57d9-423c-bd2a-f6940cc0b4db
TQID: https://experienceleague.adobe.com/U8h8uGzKvBSHAsRcwXDt7SbWihR-h-g-ReIfu-43dZ4
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: ae478996-b206-4712-9b0c-dc78a2644453
    internal-label: Integrations
  - id: eb3ad9f8-54a2-45f3-abb1-d3976415a718
    internal-label: Personalization
  - id: f2d27a5f-0d67-4d85-8a24-86a8d8a3574b
    internal-label: Developer tools
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
    internal-label: Leader
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
topic_v2:
  - id: bcc5edb5-84c3-4940-9f84-ed88b6c16274
    internal-label: Experimentation
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
    internal-label: Security
  - id: d3cdead0-685a-4489-9250-4bb709942f66
    internal-label: Data collection
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
    internal-label: Personalization
---
# Integrate Tags in Adobe Experience Platform

Learn how to integrate AEM as a Cloud Service (AEMCS) with Tags in Adobe Experience Platform. The Tags (aka Launch) integration enables you to deploy the Adobe Web SDK and inject custom JavaScript for data collection and personalization into your AEM pages.

The integration allows your marketing or development team to manage and deploy JavaScript for personalization and data collection—without needing to redeploy AEM code.

## High-Level Steps

The integration process involves four main steps that establish the connection between AEM and Tags:

1. **Create, configure, and publish a Tags property in Adobe Experience Platform**
2. **Verify an Adobe IMS configuration for Tags in AEM**
3. **Create a Tags configuration in AEM**
4. **Apply the Tags configuration to your AEM pages**

## Create, Configure, and Publish a Tags Property in Adobe Experience Platform

Start by creating a Tags property in Adobe Experience Platform. This property helps you manage the deployment of the Adobe Web SDK and any custom JavaScript required for personalization and data collection.

1. Go to the [Adobe Experience Platform](https://experience.adobe.com/platform), sign in with your Adobe ID, and navigate to **Tags** from the left-hand menu.  
   ![Adobe Experience Platform Tags](../assets/setup/aep-tags.png)

2. Click **New Property** to create a new Tags property.  
   ![Create New Tags Property](../assets/setup/aep-create-tags-property.png)

3. In the **Create Property** dialog, enter the following:
   - **Property Name**: A name for your Tags property
   - **Property Type**: Select **Web**
   - **Domain**: The domain where you deploy the property (for example, `.adobeaemcloud.com`)
   
   Click **Save**.  
   
   ![Adobe Tags Property](../assets/setup/adobe-tags-property.png)

4. Open the new property. The **Core** extension should already be included. Later, you are going to add the **Web SDK** extension  when setting up the Experimentation use case, as it requires additional configuration such as the **Datastream ID**.  
   ![Adobe Tags Core Extension](../assets/setup/adobe-tags-core-extension.png)

5. Publish the Tags property by going to **Publishing Flow** and clicking **Add Library** to create a deployment library.
   ![Adobe Tags Publishing Flow](../assets/setup/adobe-tags-publishing-flow.png)

6. In the **Create Library** dialog, provide:
   - **Name**: A name for your library
   - **Environment**: Select **Development**
   - **Resource Changes**: Choose **Add All Changed Resources**  
   
   Click **Save & Build to Development**.  
   
   ![Adobe Tags Create Library](../assets/setup/adobe-tags-create-library.png)

7. To publish the library to production, click **Approve & Publish to Production**. Once the publishing is complete, the property is ready for use in AEM.  
   ![Adobe Tags Approve & Publish](../assets/setup/adobe-tags-approve-publish.png)

## Verify an Adobe IMS Configuration for Tags in AEM

When an AEMCS environment is provisioned, it automatically includes an Adobe IMS configuration for Tags, along with a corresponding Adobe Developer Console project. This configuration ensures secure API communication between AEM and Tags.

1. In AEM, navigate to **Tools** > **Security** > **Adobe IMS Configurations**.  
   ![Adobe IMS Configurations](../assets/setup/aem-ims-configurations.png)

2. Locate the **Adobe Launch** configuration. If available, select it and click **Check Health** to verify the connection. You should see a success response.  
   ![Adobe IMS Configuration Health Check](../assets/setup/aem-ims-configuration-health-check.png)

## Create a Tags Configuration in AEM

Create a Tags configuration in AEM to specify the property and settings needed for your site pages.

1. In AEM, go to **Tools** > **Cloud Services** > **Adobe Launch Configurations**.  
   ![Adobe Launch Configurations](../assets/setup/aem-launch-configurations.png)

2. Select the root folder of your site (for example, WKND Site) and click **Create**.  
   ![Create Adobe Launch Configuration](../assets/setup/aem-create-launch-configuration.png)

3. In the dialog, enter the following:
   - **Title**: For example, "Adobe Tags"
   - **IMS Configuration**: Select the verified **Adobe Launch** IMS configuration
   - **Company**: Select the company linked to your Tags property
   - **Property**: Choose the Tags property created earlier  
   
   Click **Next**.  
   
   ![Adobe Launch Configuration Details](../assets/setup/aem-launch-configuration-details.png)

4. For demonstration purposes, keep the default values for **Staging** and **Production** environments. Click **Create**.  
   ![Adobe Launch Configuration Details](../assets/setup/aem-launch-configuration-create.png)

5. Select the newly created configuration and click **Publish** to make it available to your site pages.  
   ![Adobe Launch Configuration Publish](../assets/setup/aem-launch-configuration-publish.png)

## Apply the Tags Configuration to Your AEM Site

Apply the Tags configuration to inject the Web SDK and personalization logic into your site pages.

1. In AEM, go to **Sites**, select your root site folder (for example, WKND Site), and click **Properties**.  
   ![AEM Site Properties](../assets/setup/aem-site-properties.png)

2. In the **Site Properties** dialog, open the **Advanced** tab. Under **Configurations**, ensure `/conf/wknd` is selected for **Cloud Configuration**.  
   ![AEM Site Advanced Properties](../assets/setup/aem-site-advanced-properties.png)

## Verify the Integration

To confirm that the Tags configuration is working correctly, you can:

1. Check the view source of an AEM publish page or inspect it using browser developer tools
2. Use the [Adobe Experience Platform Debugger](https://chromewebstore.google.com/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob) to validate Web SDK and JavaScript injection

![Adobe Experience Platform Debugger](../assets/setup/aep-debugger.png)

## Additional Resources

- [Adobe Experience Platform Debugger overview](https://experienceleague.adobe.com/en/docs/experience-platform/debugger/home)
- [Tags overview](https://experienceleague.adobe.com/en/docs/experience-platform/tags/home)
