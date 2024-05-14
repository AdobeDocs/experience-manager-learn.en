---
title: Track clicked component with Adobe Analytics
description: Use the event-driven Adobe Client Data layer to track clicks of specific components on an Adobe Experience Manager site. Learn how to use tag rules to listen for these events and send data to an Adobe Analytics report suite using a track link beacon.
version: Cloud Service
topic: Integrations
feature: Adobe Client Data Layer
role: Developer
level: Intermediate
jira: KT-6296
thumbnail: KT-6296.jpg
badgeIntegration: label="Integration" type="positive"
doc-type: Tutorial
exl-id: ab051363-d3e8-4c07-b1fa-3a5d24757496
duration: 394
---
# Track clicked component with Adobe Analytics

Use the event-driven [Adobe Client Data Layer with AEM Core Components](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/data-layer/overview.html) to track clicks of specific components on an Adobe Experience Manager site. Learn how to use rules in the tag property to listen for click events, filter by component and send the data to an Adobe Analytics with a track link beacon.

## What you are going to build {#what-build}

The WKND marketing team is interested in knowing which `Call to Action (CTA)` buttons are performing the best on the home page. In this tutorial, let's add a rule to the tag property that listens for the `cmp:click` events from **Teaser** and **Button** components. Then send the component ID and a new event to Adobe Analytics alongside the track link beacon.

![What you will build track clicks](assets/track-clicked-component/final-click-tracking-cta-analytics.png)

### Objectives {#objective}

1. Create an event-driven rule in the tag property that captures the `cmp:click` event.
1. Filter the different events by component resource type.
1. Set the component id and send an event to Adobe Analytics with the track link beacon.

## Prerequisites

This tutorial is a continuation of [Collect page data with Adobe Analytics](./collect-data-analytics.md) and assumes that you have:

* A **Tag property** with the [Adobe Analytics extension](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/analytics/overview.html) enabled
* **Adobe Analytics** test/dev report suite ID and tracking server. See the following documentation for [creating a report suite](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/manage-report-suites/c-new-report-suite/new-report-suite.html).
* [Experience Platform Debugger](https://experienceleague.adobe.com/docs/platform-learn/data-collection/debugger/overview.html) browser extension configured with your tag property loaded on the [WKND site](https://wknd.site/us/en.html) or an AEM site with the Adobe Data Layer enabled.

## Inspect the Button and Teaser schema

Before creating rules in the tag property, it is useful to review the [schema for the Button and Teaser](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/data-layer/overview.html#item) and inspect them in the data layer implementation.

1. Navigate to [WKND Home page](https://wknd.site/us/en.html)
1. Open the browser's developer tools and navigate to the **Console**. Run the following command:

    ```js
    adobeDataLayer.getState();
    ```

    Above code returns the current state of the Adobe Client Data Layer.

    ![Data Layer state via browser console](assets/track-clicked-component/adobe-data-layer-state-browser.png)

1. Expand the response and find entries prefixed with `button-` and  `teaser-xyz-cta` entry. You should see a data schema like the following:

    Button Schema:

    ```json
    button-2e6d32893a:
        @type: "wknd/components/button"
        dc:title: "View All"
        parentId: "page-2eee4f8914"
        repo:modifyDate: "2020-07-11T22:17:55Z"
        xdm:linkURL: "/content/wknd/us/en/magazine.html"
    ```

    Teaser Schema:

    ```json
    teaser-da32481ec8-cta-adf3c09db9:
        @type: "wknd/components/teaser/cta"
        dc:title: "Surf's Up"
        parentId: "teaser-da32481ec8"
        xdm:linkURL: "/content/wknd/us/en/magazine/san-diego-surf.html"
    ```

    Above data details are based on the [Component/Container Item Schema](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/data-layer/overview.html#item). The new tag rule uses this schema.

## Create a CTA clicked rule

The Adobe Client Data Layer is an **event** driven data layer. Whenever any Core Component is clicked a `cmp:click` event is dispatched via the data layer. To listen for the `cmp:click` event, let's create a rule .

1. Navigate to Experience Platform and into the tag property integrated with the AEM Site.
1. Navigate to the **Rules** section in the Tag Property UI, then click **Add Rule**.
1. Name the rule **CTA Clicked**.
1. Click **Events** > **Add** to open the **Event Configuration** wizard.
1. For **Event Type** field, select **Custom Code**.

   ![Name the rule CTA Clicked and add the custom code event](assets/track-clicked-component/custom-code-event.png)

1. Click **Open Editor** in the main panel and enter the following code snippet:

   ```js
   var componentClickedHandler = function(evt) {
      // defensive coding to avoid a null pointer exception
      if(evt.hasOwnProperty("eventInfo") && evt.eventInfo.hasOwnProperty("path")) {
         //trigger Tag Rule and pass event
         console.debug("cmp:click event: " + evt.eventInfo.path);
         var event = {
            //include the path of the component that triggered the event
            path: evt.eventInfo.path,
            //get the state of the component that triggered the event
            component: window.adobeDataLayer.getState(evt.eventInfo.path)
         };

         //Trigger the Tag Rule, passing in the new `event` object
         // the `event` obj can now be referenced by the reserved name `event` by other Tag Property data elements
         // i.e `event.component['someKey']`
         trigger(event);
      }
   }

   //set the namespace to avoid a potential race condition
   window.adobeDataLayer = window.adobeDataLayer || [];
   //push the event listener for cmp:click into the data layer
   window.adobeDataLayer.push(function (dl) {
      //add event listener for `cmp:click` and callback to the `componentClickedHandler` function
      dl.addEventListener("cmp:click", componentClickedHandler);
   });
   ```

   The above code snippet adds an event listener by [pushing a function](https://github.com/adobe/adobe-client-data-layer/wiki#pushing-a-function) into the data layer. Whenever the `cmp:click` event is triggered the `componentClickedHandler` function is called. In this function, a few sanity checks are added and a new `event` object is constructed with the latest [state of the data layer](https://github.com/adobe/adobe-client-data-layer/wiki#getstate) for the component that triggered the event.

   Finally the `trigger(event)` function is called. The `trigger()` function is a reserved name in the tag property and it **triggers** the rule. The `event` object is passed as a parameter which in turn is exposed by another reserved name in the tag property. Data Elements in the tag property can now reference various properties using code snippet like `event.component['someKey']`.

1. Save the changes.
1. Next under **Actions** click **Add** to open the **Action Configuration** wizard.
1. For **Action Type** field, choose **Custom Code**.

   ![Custom Code Action Type](assets/track-clicked-component/action-custom-code.png)

1. Click **Open Editor** in the main panel and enter the following code snippet:

   ```js
   console.debug("Component Clicked");
   console.debug("Component Path: " + event.path);
   console.debug("Component type: " + event.component['@type']);
   console.debug("Component text: " + event.component['dc:title']);
   ```

   The `event` object is passed from the `trigger()` method called in the custom event. The `component` object is the current state of the component derived from the data layer `getState()` method and is the element that triggered the click.

1. Save the changes and run a [build](https://experienceleague.adobe.com/docs/experience-platform/tags/publish/builds.html) in the tag property to promote the code to the [environment](https://experienceleague.adobe.com/docs/experience-platform/tags/publish/environments/environments.html) used on your AEM Site.

   >[!NOTE]
   >
   > It can be useful to use the [Adobe Experience Platform Debugger](https://experienceleague.adobe.com/docs/platform-learn/data-collection/debugger/overview.html) to switch the embed code to a **Development** environment.

1. Navigate to the [WKND Site](https://wknd.site/us/en.html) and open the developer tools to view the console. Also, select the **Preserve log** checkbox.

1. Click one of the **Teaser** or **Button** CTA buttons to navigate to another page.

    ![CTA Button to click](assets/track-clicked-component/cta-button-to-click.png)

1. Observe in the developer console that the **CTA Clicked** rule has been fired:

    ![CTA Button Clicked](assets/track-clicked-component/cta-button-clicked-log.png)

## Create Data Elements

Next create a Data Elements to capture the component ID and title that was clicked. Recall in the previous exercise the output of `event.path` was something similar to `component.button-b6562c963d` and the value of `event.component['dc:title']` was something like "View Trips".

### Component ID

1. Navigate to Experience Platform and into the tag property integrated with the AEM Site.
1. Navigate to the **Data Elements** section and click **Add New Data Element**.
1. For **Name** field, enter **Component ID**.
1. For **Data Element Type** field, select **Custom Code**.

    ![Component ID Data Element form](assets/track-clicked-component/component-id-data-element.png)

1. Click **Open Editor** button and enter the following in the custom code editor:

    ```js
    if(event && event.path && event.path.includes('.')) {
        // split on the `.` to return just the component ID
        return event.path.split('.')[1];
    }
    ```

1. Save the changes.
    
    >[!NOTE]
    >
    > Recall that the `event` object is made available and scoped based on the event that triggered the **Rule** in tag property. The value of a Data Element is not set until the Data Element is *referenced* within a Rule. Therefore it is safe to use this Data Element inside a Rule like the **Page Loaded** rule created in the previous step *but* would not be safe to use in other contexts.


### Component Title

1. Navigate to the **Data Elements** section and click **Add New Data Element**.
1. For **Name** field, enter **Component Title**.
1. For **Data Element Type** field, select **Custom Code**.
1. Click **Open Editor** button and enter the following in the custom code editor:

    ```js
    if(event && event.component && event.component.hasOwnProperty('dc:title')) {
        return event.component['dc:title'];
    }
    ```

1.  Save the changes.

## Add a condition to the CTA Clicked rule

Next, update the **CTA Clicked** rule to ensure that the rule only fires when the `cmp:click` event is fired for a **Teaser** or a **Button**. Since the Teaser's CTA is considered a separate object in the data layer, it is important to check the parent to verify it came from a Teaser.

1. In the Tag Property UI, navigate to the **CTA Clicked** rule created earlier.
1. Under **Conditions** click **Add** to open the **Condition Configuration** wizard.
1. For **Condition Type** field, select **Custom Code**.

    ![CTA Clicked Condition Custom Code](assets/track-clicked-component/custom-code-condition.png)

1. Click **Open Editor** and enter the following in the custom code editor:

    ```js
    if(event && event.component && event.component.hasOwnProperty('@type')) {
        // console.log("Event Type: " + event.component['@type']);
        //Check for Button Type OR Teaser CTA type
        if(event.component['@type'] === 'wknd/components/button' ||
           event.component['@type'] === 'wknd/components/teaser/cta') {
            return true;
        }
    }

    // none of the conditions are met, return false
    return false;
    ```

    The above code first checks to see if the resource type was from a **Button** or if the resource type was from a CTA within a **Teaser**.

1. Save the changes.

## Set Analytics Variables and trigger Track Link Beacon

Currently the **CTA Clicked** rule simply outputs a console statement. Next, use the data elements and the Analytics extension to set Analytics variables as an **action**. Let's also set an extra action to trigger the **Track Link** and send the collected data to Adobe Analytics.

1. In the **CTA Clicked** rule, **remove** the **Core - Custom Code** action (the console statements):

   ![Remove custom code action](assets/track-clicked-component/remove-console-statements.png)

1. Under Actions, click **Add** to create an action.
1. Set the **Extension** type to **Adobe Analytics** and set the **Action Type** to  **Set Variables**.

1. Set the following values for **eVars**, **Props**, and **Events**:

    * `evar8` - `%Component ID%`
    * `prop8` - `%Component ID%`
    * `event8`

    ![Set eVar Prop and events](assets/track-clicked-component/set-evar-prop-event.png)

    >[!NOTE]
    >
    > Here `%Component ID%` is used since it guarantees a unique identifier for the CTA that was clicked. A potential downside of using `%Component ID%` is that the Analytics report contains values like `button-2e6d32893a`. Using the `%Component Title%` would give a more human friendly name but the value might not be unique.

1. Next, add an extra Action to the right of the **Adobe Analytics - Set Variables** by tapping the **plus** icon:

    ![Add an Extra Action to Tag Rule](assets/track-clicked-component/add-additional-launch-action.png)

1. Set the **Extension** type to **Adobe Analytics** and set the **Action Type** to  **Send Beacon**.
1. Under **Tracking** set the radio button to **`s.tl()`**.
1. For **Link Type** field, choose **Custom Link** and for **Link Name** set the value to: **`%Component Title%: CTA Clicked`**:

    ![Configuraiton for Send Link beacon](assets/track-clicked-component/analytics-send-beacon-link-track.png)

    The above config combines the dynamic variable from the data element **Component Title** and the static string **CTA Clicked**.

1. Save the changes. The **CTA Clicked** rule should now have the following configuration:

   ![Final Tag Rule Configuration](assets/track-clicked-component/final-page-loaded-config.png)

   * **1.** Listen for the `cmp:click` event.
   * **2.** Check that the event was triggered by a **Button** or **Teaser**.
   * **3.** Set Analytics variables to track the **Component ID** as an **eVar**, **prop**, and an **event**.
   * **4.** Send the Analytics Track Link Beacon (and do **not** treat it as a page view).

1. Save all the changes and build your tag library, promoting to the appropriate Environment.

## Validate the Track Link Beacon and Analytics call

Now that the **CTA Clicked** rule sends the Analytics beacon, you should be able to see the Analytics tracking variables using the Experience Platform Debugger.

1. Open the [WKND Site](https://wknd.site/us/en.html) in your browser.
1. Click the Debugger icon ![Experience platform Debugger icon](assets/track-clicked-component/experience-cloud-debugger.png) to open the Experience Platform Debugger.
1. Make sure that the Debugger is mapping the tag property to *your* Development environment, as described earlier and the **Console Logging** is checked.
1. Open the Analytics menu and verify that the report suite is set to *your* report suite.

   ![Analytics tab debugger](assets/track-clicked-component/analytics-tab-debugger.png)

1. In the browser, click one of the **Teaser** or **Button** CTA buttons to navigate to another page.

    ![CTA Button to click](assets/track-clicked-component/cta-button-to-click.png)

1. Return to the Experience Platform Debugger and scroll down and expand **Network Requests** > *Your Report Suite*. You should be able to find the **eVar**, **prop**, and **event** set.

   ![Analytics events, evar, and prop tracked on click](assets/track-clicked-component/evar-prop-link-clicked-tracked-debugger.png)

1. Return to the browser and open up the developer console. Navigate to the footer of the site and click one of the navigation links:

    ![Click Navigation link in the footer](assets/track-clicked-component/click-navigation-link-footer.png)

1. Observe in the browser console the message *"Custom Code" for rule "CTA Clicked" was not met*.

   The above message is because the Navigation component does trigger a `cmp:click` event *but* because of [Condition to the rule](#add-a-condition-to-the-cta-clicked-rule) that checks the resource type no action is taken.

   >[!NOTE]
   >
   > If you don't see any console logs, ensure that **Console Logging** is checked under **Experience Platform Tags** in the Experience Platform Debugger.

## Congratulations!

You just used the event-driven Adobe Client Data Layer and Tag in Experience Platform to track the clicks of specific components on an AEM site.
