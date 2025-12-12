---
title: Experimentation (A/B Testing)
description: Learn how to test different content variations in AEM as a Cloud Service (AEMCS) using Adobe Target for A/B testing.
version: Experience Manager as a Cloud Service
feature: Personalization
topic: Personalization,Content Management, Integrations
role: Developer, Leader
level: Beginner
doc-type: Tutorial
last-substantial-update: 2025-08-07
jira: KT-18720
thumbnail: KT-18720.jpeg
exl-id: c8a4f0bf-1f80-4494-abe6-9fbc138e4039
---
# Experimentation (A/B Testing)

Learn how to test different content variations on an AEM as a Cloud Service (AEMCS) website using Adobe Target.

A/B testing helps you compare different versions of content to determine which performs better in achieving your business goals. Common scenarios include:

- Testing variations in headlines, images, or call-to-action buttons on a landing page
- Comparing different layouts or designs for a product detail page
- Evaluating promotional offers or discount strategies

## Demo Use Case

In this tutorial, you configure A/B testing for the **Camping in Western Australia** Experience Fragment (XF) on the WKND website. You create three XF variations and manage the A/B test through Adobe Target.

The variations are displayed on the WKND homepage, allowing you to measure performance and determine which version drives better engagement and conversions.

![A/B Test](../assets/use-cases/experiment/view-ab-test-variations.png)

### Live Demo

Visit the [WKND Enablement website](https://wknd.enablementadobe.com/us/en.html) to see the A/B test in action. In the video below, you see all three variations of **Camping in Western Australia** displayed on the homepage via different browsers.

>[!VIDEO](https://video.tv.adobe.com/v/3473005/?learn=on&enablevpops)

## Prerequisites

Before proceeding with the experimentation use case, ensure you have completed the following:

- [Integrate Adobe Target](../setup/integrate-adobe-target.md): Enables your team to create and manage personalized content centrally in AEM and activate it as offers in Adobe Target.
- [Integrate Tags in Adobe Experience Platform](../setup/integrate-adobe-tags.md): Allows your team to manage and deploy JavaScript for personalization and data collection without needing to redeploy AEM code.

## High-Level Steps

The A/B testing setup process involves six main steps that create and configure the experiment:

1. **Create content variations in AEM**
2. **Export the variations as offers to Adobe Target**
3. **Create an A/B test activity in Adobe Target**
4. **Create and configure a Datastream in Adobe Experience Platform**
5. **Update the Tags property with the Web SDK extension**
6. **Verify the A/B test implementation on your AEM pages**

## Create Content Variations in AEM

In this example, you use the **Camping in Western Australia** Experience Fragment (XF) from the AEM WKND project to create three variations, which will be used on the WKND website homepage for A/B testing.

1. In AEM, click the **Experience Fragments** card, navigate to **Camping in Western Australia**, and click **Edit**.
   ![Experience Fragments](../assets/use-cases/experiment/camping-in-western-australia-xf.png)

1. In the editor, under the **Variations** section, click **Create**, and select **Variation**.  
   ![Create Variation](../assets/use-cases/experiment/create-variation.png)

1. In the **Create Variation** dialog:
   - **Template**: Experience Fragment Web Variation Template  
   - **Title**: For example, "Off the Grid"  

   Click **Done**.  

   ![Create Variation Dialog](../assets/use-cases/experiment/create-variation-dialog.png)

1. Author the variation by copying the **Teaser** component from the master variation, then customize the content (e.g., update the title and image).  
   ![Author Variation-1](../assets/use-cases/experiment/author-variation-1.png)

   >[!TIP]
   >You can use [Generate Variations](https://experience.adobe.com/aem/generate-variations/) to quickly create new variations from the master XF.

1. Repeat the steps to create another variation (e.g., "Wandering the Wild").  
   ![Author Variation-2](../assets/use-cases/experiment/author-variation-2.png)

   You now have three Experience Fragment variations for A/B testing.

1. Before displaying variations using Adobe Target, you need to remove the existing static teaser from the homepage. It prevents duplicate content, as the Experience Fragment variations are injected dynamically via Target.

   - Navigate to the **English** homepage `/content/wknd/language-masters/en`
   - In the editor, delete the **Camping in Western Australia** teaser component.  
     ![Delete Teaser Component](../assets/use-cases/experiment/delete-teaser-component.png)

1. Roll out the changes to the **US > English** homepage (`/content/wknd/us/en`) to propagate the updates.  
   ![Rollout Changes](../assets/use-cases/experiment/rollout-changes.png)

1. Publish the **US > English** homepage to make the updates live.  
   ![Publish Homepage](../assets/use-cases/experiment/publish-homepage.png)

## Export the Variations as Offers to Adobe Target

Export the Experience Fragment variations so they can be used as offers in Adobe Target for the A/B test.

1. In AEM, navigate to **Camping in Western Australia**, select the three variations, and click **Export to Adobe Target**.  
   ![Export to Adobe Target](../assets/use-cases/experiment/export-to-adobe-target.png)

2. In Adobe Target, go to **Offers** and confirm the variations have been imported.  
   ![Offers in Adobe Target](../assets/use-cases/experiment/offers-in-adobe-target.png)

## Create an A/B Test Activity in Adobe Target

Now create an A/B test activity to run the experiment on the homepage.

1. Install the [Adobe Experience Cloud Visual Editing Helper](https://chromewebstore.google.com/detail/adobe-experience-cloud-vi/kgmjjkfjacffaebgpkpcllakjifppnca) Chrome extension.

1. In Adobe Target, navigate to **Activities** and click **Create Activity**.  
   ![Create Activity](../assets/use-cases/experiment/create-activity.png)

1. In the **Create A/B Test Activity** dialog, enter the following:
   - **Type**: Web  
   - **Composer**: Visual  
   - **Activity URL**: e.g., `https://wknd.enablementadobe.com/us/en.html`  

   Click **Create**.  
   
   ![Create A/B Test Activity](../assets/use-cases/experiment/create-ab-test-activity.png)

1. Rename the activity to something meaningful (e.g., "WKND Homepage A/B Test").  
   ![Rename Activity](../assets/use-cases/experiment/rename-activity.png)

1. In **Experience A**, add the **Experience Fragment** component above the **Recent Articles** section.  
   ![Add Experience Fragment Component](../assets/use-cases/experiment/add-experience-fragment-component.png)

1. In the component dialog, click **Select an Offer**.  
   ![Select Offer](../assets/use-cases/experiment/select-offer.png)

1. Choose the **Camping in Western Australia** variation and click **Add**.  
   ![Select Camping in Western Australia XF](../assets/use-cases/experiment/select-camping-in-western-australia-xf.png)

1. Repeat for **Experience B** and **C**, selecting **Off the Grid** and **Wandering the Wild** respectively.  
   ![Add Experience B and C](../assets/use-cases/experiment/add-experience-b-and-c.png)

1. In the **Targeting** section, confirm the traffic is split evenly across all experiences.  
   ![Traffic Allocation](../assets/use-cases/experiment/traffic-allocation.png)

1. In **Goals & Settings**, define your success metric (e.g., CTA clicks on the Experience Fragment).  
   ![Goals & Settings](../assets/use-cases/experiment/goals-and-settings.png)

1. Click **Activate** in the top-right corner to launch the test.  
   ![Activate Activity](../assets/use-cases/experiment/activate-activity.png)

## Create and Configure a Datastream in Adobe Experience Platform

To connect the Adobe Web SDK to Adobe Target, create a Datastream in Adobe Experience Platform. The Datastream acts as a routing layer between the Web SDK and Adobe Target.

1. In Adobe Experience Platform, navigate to **Datastreams** and click **Create Datastream**.  
   ![Create New Datastream](../assets/use-cases/experiment/aep-create-datastream.png)

1. In the **Create Datastream** dialog, enter a **Name** for your Datastream and click **Save**.  
   ![Enter Datastream Name](../assets/use-cases/experiment/aep-datastream-name.png)

1. Once the Datastream is created, click **Add Service**.  
   ![Add Service to Datastream](../assets/use-cases/experiment/aep-add-service.png)

1. In the **Add Service** step, select **Adobe Target** from the dropdown and enter the **Target Environment ID**. You can find the Target Environment ID in Adobe Target under **Administration** > **Environments**. Click **Save** to add the service.  
   ![Configure Adobe Target Service](../assets/use-cases/experiment/aep-target-service.png)

1. Review the Datastream details to verify that the Adobe Target service is listed and correctly configured.  
   ![Review Datastream](../assets/use-cases/experiment/aep-datastream-review.png)

## Update the Tags Property with the Web SDK Extension

To send personalization and data collection events from AEM pages, add the Web SDK extension to your Tags property and configure a rule that triggers on page load.

1. In Adobe Experience Platform, navigate to **Tags** and open the property you created in the [Integrate Adobe Tags](../setup/integrate-adobe-tags.md) step.
   ![Open Tags Property](../assets/use-cases/experiment/open-tags-property.png)

1. From the left-hand menu, click **Extensions**, switch to the **Catalog** tab, and search for **Web SDK**. Click **Install** in the right-side panel.  
   ![Install Web SDK Extension](../assets/use-cases/experiment/web-sdk-extension-install.png)

1. In the **Install Extension** dialog, select the **Datastream** you created earlier and click **Save**.  
   ![Select Datastream](../assets/use-cases/experiment/web-sdk-extension-select-datastream.png)

1. After installing, verify that both **Adobe Experience Platform Web SDK** and **Core** extensions appear under the **Installed** tab.  
   ![Installed Extensions](../assets/use-cases/experiment/web-sdk-extension-installed.png)

1. Next, configure a rule to send the Web SDK event when the library is loaded. Navigate to **Rules** from the left-hand menu and click **Create New Rule**.  

   ![Create New Rule](../assets/use-cases/experiment/web-sdk-rule-create.png)

   >[!TIP]
   >
   >A rule allows you to define when and how tags fire based on user interactions or browser events.

1. In the **Create Rule** screen, enter a rule name (for example, `All Pages - Library Loaded - Send Event`) and click **+ Add** under the **Events** section.
   ![Rule Name](../assets/use-cases/experiment/web-sdk-rule-name.png)

1. In the **Event Configuration** dialog:
   - **Extension**: Select **Core**
   - **Event Type**: Select **Library Loaded (Page Top)**
   - **Name**: Enter `Core - Library Loaded (Page Top)`
   
   Click **Keep Changes** to save the event.  
   
   ![Create Event Rule](../assets/use-cases/experiment/web-sdk-rule-event.png)

1. Under the **Actions** section, click **+ Add** to define the action that occurs when the event fires.

1. In the **Action Configuration** dialog:
   - **Extension**: Select **Adobe Experience Platform Web SDK**
   - **Action Type**: Select **Send Event**
   - **Name**: Select **AEP Web SDK - Send Event**
   
   ![Configure Send Event Action](../assets/use-cases/experiment/web-sdk-rule-action.png)

1. In the right panel's **Personalization** section, check the **Render visual personalization decisions** option. Then, click **Keep Changes** to save the action.  
   ![Create Action Rule](../assets/use-cases/experiment/web-sdk-rule-action.png)

   >[!TIP]
   >
   >   This action sends an AEP Web SDK event when the page loads, allowing Adobe Target to deliver personalized content.

1. Review the completed rule and click **Save**.
   ![Review Rule](../assets/use-cases/experiment/web-sdk-rule-review.png)

1. To apply the changes, go to **Publishing Flow**, add the updated rule to a **Library**.  
   ![Publish Tags Library](../assets/use-cases/experiment/web-sdk-rule-publish.png)

1. Finally, promote the library to **Production**. 
   ![Publish Tags to Production](../assets/use-cases/experiment/web-sdk-rule-publish-production.png)

## Verify the A/B Test Implementation on Your AEM Pages

Once the activity is live and the Tags library has been published to production, you can verify the A/B test on your AEM pages.

1. Visit the published site (for example, [WKND Enablement website](https://wknd.enablementadobe.com/us/en.html)) and observe which variation is displayed. Try accessing it from a different browser or mobile device to see alternate variations.
   ![View A/B Test Variations](../assets/use-cases/experiment/view-ab-test-variations.png)

1. Open your browser's developer tools and check the **Network** tab. Filter by `interact` to find the Web SDK request. The request should the Web SDK event details.

   ![Web SDK Network Request](../assets/use-cases/experiment/web-sdk-network-request.png)

  The response should include the personalization decisions made by Adobe Target, indicating which variation was served.  
   ![Web SDK Response](../assets/use-cases/experiment/web-sdk-response.png)

1. Alternatively, you can use the [Adobe Experience Platform Debugger](https://chromewebstore.google.com/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob) Chrome extension to inspect the Web SDK events.
   ![AEP Debugger](../assets/use-cases/experiment/aep-debugger-variation.png)

## Live Demo

To see the A/B test in action, visit the [WKND Enablement website](https://wknd.enablementadobe.com/us/en.html) and observe how different variations of the Experience Fragment are displayed on the homepage.

## Additional Resources

- [A/B Test overview](https://experienceleague.adobe.com/en/docs/target/using/activities/abtest/test-ab)
- [Adobe Experience Platform Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home)
- [Datastreams overview](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/overview)
- [Visual Experience Composer (VEC)](https://experienceleague.adobe.com/en/docs/target/using/experiences/vec/visual-experience-composer)
