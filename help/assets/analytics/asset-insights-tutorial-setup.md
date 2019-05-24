---
title: Set up Asset Insights with AEM Assets
seo-title: Set up Asset Insights with AEM Assets
description: In this 3 part video series, we walk through the setup and configuration of Asset Insights for Experience Manager deployed via Adobe Activation (DTM).
seo-description: In this 3 part video series, we walk through the setup and configuration of Asset Insights for Experience Manager deployed via Adobe Activation (DTM).
uuid: 9c7d4055-205e-4cd0-b35b-b9540601f427
products: SG_EXPERIENCEMANAGER/6.3/ASSETS
products: SG_EXPERIENCEMANAGER/6.4/ASSETS
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: asset-insights
topic-tags: images
discoiquuid: 184e5b87-e029-4878-9902-fc1851f546f7
targetaudience: target-audience advanced
---

# Set up Asset Insights with AEM Assets{#set-up-asset-insights-with-aem-assets}

In this 3 part video series, we walk through the setup and configuration of Asset Insights for Experience Manager deployed via Adobe Activation (DTM).

>[!NOTE]
>
>The below videos are recorded using AEM 6.3. The setup for Asset Insights with AEM 6.4 are largely the same. These differences between AEM 6.3 and 6.4 are called out in the surrounding text below.

Below are a series of videos to set up Asset Insights with DTM. A written version of the steps can be found here: [Enabling Asset Insights through DTM](https://helpx.adobe.com/experience-manager/6-4/assets/using/touch-ui-using-dtm-for-asset-insights.html)

## Part 1: Overview and Configuration of Analytics and DTM {#configure-analytics-dtm}

Asset Insights Overview. Adobe Analytic and DTM solutions are configured to enable AEM Asset Insights.

>[!VIDEO](https://video.tv.adobe.com/v/16419?quality=9)

*Part 1 gives a high-level overview of Asset Insights architecture. This video walks through the necessary configuration of Adobe Analytics and DTM solutions.*

Below snippet is mentioned at 7:40 of the above video. JavaScript snippet to be added to the **DTM Web Property** -&gt; **Adobe Analytics** -&gt; **Customize Page Code entry**:

```javascript
var sObj;
  
if (arguments.length > 0) {
  sObj = arguments[0];
} else {
  sObj = _satellite.getToolsByType('sc')[0].getS();
}
_satellite.notify('in assetAnalytics customInit');
(function initializeAssetAnalytics() {
  if ((!!window.assetAnalytics) && (!!assetAnalytics.dispatcher)) {
    _satellite.notify('assetAnalytics ready');
    /** NOTE:
        Copy over the call to 'assetAnalytics.dispatcher.init()' from Assets Pagetracker
        Be mindful about changing the AppMeasurement object as retrieved above.
    */
    assetAnalytics.dispatcher.init(
          "",  /** RSID to send tracking-call to */
          "",  /** Tracking Server to send tracking-call to */
          "",  /** Visitor Namespace to send tracking-call to */
          "",  /** listVar to put comma-separated-list of Asset IDs for Asset Impression Events in tracking-call, e.g. 'listVar1' */
          "",  /** eVar to put Asset ID for Asset Click Events in, e.g. 'eVar3' */
          "",  /** event to include in tracking-calls for Asset Impression Events, e.g. 'event8' */
          "",  /** event to include in tracking-calls for Asset Click Events, e.g. 'event7' */
          sObj  /** [OPTIONAL] if the webpage already has an AppMeasurement object, please include the object here. If unspecified, Pagetracker Core shall create its own AppMeasurement object */
          );
    sObj.usePlugins = true;
    sObj.doPlugins = assetAnalytics.core.updateContextData;
    assetAnalytics.core.optimizedAssetInsights();
  }
  else {
    _satellite.notify('assetAnalytics not available. Consider updating the Custom Page Code', 4);
  }
})();

```

Below snippet is mentioned at 9:15 of the above video. Note where the sample code references "http://localhost:4503" should be replaced with the hostname of your public site. **DTM Web Property** -&gt; **Rules** -&gt; **Page Load Rules** -&gt; **Javascript / Third Party Tags** -&gt; **Sequential HTML**:

>[!CAUTION]
>
>The location of `pagetracker.js` is different in AEM 6.4 and AEM 6.3. The code sample below shows both versions. Copy only the line for the version of AEM being deployed.

```
//For AEM 6.3
<script type="text/javascript" src="http://localhost:4503/etc/clientlibs/foundation/assetinsights/pagetracker.js"></script>

//For AEM 6.4
<script type="text/javascript" src="http://localhost:4503/etc.clientlibs/dam/clientlibs/assetinsights/pagetracker.js"></script>
```

## Part 2: Connecting AEM and Embedding Insights Code {#part-2-connect-aem}

Connect Analytics and DTM to AEM. Review HTML+JS for Insight tracking

>[!VIDEO](https://video.tv.adobe.com/v/16425/?quality=9)

*Part two details the cloud service configs to connect Adobe Analytics and DTM to AEM. This video also highlights the HTML+JS (embed code) necessary for using with AEM Sites or 3rd Party Site.*

In the above video an extension of the ootb Sites Image Component is used to add images to a page. The sample component automatically includes the Asset Insight tracking HTML attributes including the ***aem-asset-id***. The package can be downloaded below. In addition two examples of extending the Core Image component and Foundation Image component can be found on GitHub: **Note this is a sample component for development use only and will install Core Components v1.0.4**
[ ](https://github.com/Adobe-Marketing-Cloud/aem-guides/tree/master/asset-insights-guide)
Image Insights Components (Foundation and Core)

Download [Asset Insights Guide Apps](assets/asset-insights-guideuiapps-001-snapshot.zip)

## Part 3: Testing Analytic Tracking and Syncing Insight Data {#part-3-testing-and-syncing}

>[!VIDEO](https://video.tv.adobe.com/v/16426/?quality=9)

*The final video shows asset clicks+impressions tracked, synced and displayed in the AEM Author environment. Techniques of verifying and debugging analytic tracking from the browser are highlighted.*

Two Google Chrome browser extensions are referenced in the video as ways to debug Analytics. Similar extensions are available for other browsers as well.

* [Adobe Analytics Debugger](https://chrome.google.com/webstore/detail/adobe-analytics-debugger/bdingoflfadhnjohjaplginnpjeclmof?hl=en)
* [ObservePoint Tag Debugger](https://chrome.google.com/webstore/detail/observepoint-tag-debugger/daejfbkjipkgidckemjjafiomfeabemo?hl=en-US)

It is also possible to switch DTM into debug mode with the following Chrome Extension: [Adobe DTM Switch](https://chrome.google.com/webstore/detail/adobe-dtm-switch/nlgdemkdapolikbjimjajpmonpbpmipk?hl=en). This makes it easier to see if there are any errors related to DTM deployment. In addition, you can manually switch DTM to debug mode via any browsers' **developer tools -&gt; JS Console** by adding the following snippet:

```javascript
//switch DTM to debug mode
//if _satellite JS object is undefined then DTM is not being included properly

_satellite.setDebug(true);
```

## Supporting materials {#supporting-materials}

* [Adobe Analytics Debugger Chrome Plug-in](https://chrome.google.com/webstore/detail/observepoint-tag-debugger/daejfbkjipkgidckemjjafiomfeabemo?hl=en-US)
* [Adobe DTM Switch Chrome Plug-in](https://chrome.google.com/webstore/detail/adobe-dtm-switch/nlgdemkdapolikbjimjajpmonpbpmipk?hl=en)
* [ObservePoint Tag Debugger Chrome Plug-in](https://chrome.google.com/webstore/detail/observepoint-tag-debugger/daejfbkjipkgidckemjjafiomfeabemo?hl=en-US)

* [Adobe Analytics Web site](https://sc.omniture.com)
* [Adobe DTM (Activation) Web site](https://dtm.adobe.com)

