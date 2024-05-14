---
title: Add widgets to Rich Text Editor (RTE)
description: Learn how to add widgets to Rich Text Editor (RTE) in the AEM Content Fragment Editor
feature: Developer Tools, Content Fragments
version: Cloud Service
topic: Development
role: Developer
level: Beginner
jira: KT-13465
thumbnail: KT-13465.jpg
doc-type: article
last-substantial-update: 2023-06-12
exl-id: 167a4b11-1202-4c7a-b022-f3f996348a4e
duration: 476
---
# Add widgets to Rich Text Editor (RTE)

Learn how to add widgets to the Rich Text Editor (RTE) in the AEM Content Fragment Editor.

>[!VIDEO](https://video.tv.adobe.com/v/3420822?quality=12&learn=on)

To add the dynamic content in the Rich Text Editor (RTE), the **widgets** functionality can be used. The widgets help to integrate the simple or complex UI in the RTE and the UI can be created using the JS framework of your choice. They can be thought as dialogs that are opened by pressing `{` special key in the RTE.

Typically, the widgets are used to insert the dynamic content that has an external system dependency or could change based on the current context.

The **widgets** are added to the **RTE** in the Content Fragment Editor using the `rte` extension point. Using `rte` extension point's `getWidgets()` method one or many widgets are added. They are triggered by pressing the `{` special key to open the context menu option, and then select the desired widget to load the custom dialog UI.

This example shows how to add a widget called _Discount Code List_ to find, select, and add the WKND adventure-specific discount code within an RTE content. These discount codes can be managed in external system like Order Management System (OMS), Product Information Management (PIM),  home grown application or an Adobe AppBuilder action.

To keep things simple, this example uses the [Adobe React Spectrum](https://react-spectrum.adobe.com/react-spectrum/index.html) framework to develop the widget or dialog UI and hard-coded WKND adventure name, discount code data.

## Extension point

This example extends to extension point `rte` to add a widget to the RTE in the Content Fragment Editor.

| AEM UI extended | Extension point |
| ------------------------ | --------------------- | 
| [Content Fragment Editor](https://developer.adobe.com/uix/docs/services/aem-cf-editor/) | [Rich Text Editor Widgets](https://developer.adobe.com/uix/docs/services/aem-cf-editor/api/rte-widgets/) | 

## Example extension

The following example creates a _Discount Code List_ widget. By pressing the `{` special key within the RTE, the context menu is opened, then by selecting the _Discount Code List_ option from the context menu the dialog UI is opened.

The WKND content authors can find, select, and add current Adventure-specific discount code, if available.

### Extension registration

`ExtensionRegistration.js`, mapped to the index.html route, is the entry point for the AEM extension and defines:

+ The widget definition in `getWidgets()` function with `id, label and url` attributes.
+ The `url` attribute value, a relative URL path (`/index.html#/discountCodes`) to load the dialog UI.

`src/aem-cf-editor-1/web-src/src/components/ExtensionRegistration.js`

```javascript
import React from "react";
import { Text } from "@adobe/react-spectrum";
import { register } from "@adobe/uix-guest";
import { extensionId } from "./Constants";

// This function is called when the extension is registered with the host and runs in an iframe in the Content Fragment Editor browser window.
function ExtensionRegistration() {
  const init = async () => {
    const guestConnection = await register({
      id: extensionId,
      methods: {
        rte: {
          // RTE Widgets
          getWidgets: () => [
            {
              id: "discountcode-list-widget", // Provide a unique ID for the widget
              label: "Discount Code List", // Provide a label for the widget
              url: "/index.html#/discountCodes", // Provide the "relative" URL to the widget content. It will be resolved as `/index.html#/discountCodes`
            },
          ],
        }, // Add a comma here
      },
    });
  };

  init().catch(console.error);

  return <Text>IFrame for integration with Host (AEM)...</Text>;
}

export default ExtensionRegistration;
```

### Add `discountCodes` route in `App.js`{#add-widgets-route}

In the main React component `App.js`, add the `discountCodes` route to render the UI for the above relative URL path.

`src/aem-cf-editor-1/web-src/src/components/App.js`

```javascript
...

<Routes>
  <Route index element={<ExtensionRegistration />} />
  <Route
    exact path="index.html"
    element={<ExtensionRegistration />}
  />

  {/* Content Fragment RTE routes that support the Discount Codes Widget functionality*/}
  <Route path="/discountCodes" element={<DiscountCodes />} />
</Routes>
...

```

### Create `DiscountCodes` React component{#create-widget-react-component}

The widget or dialog UI is created using the [Adobe React Spectrum](https://react-spectrum.adobe.com/react-spectrum/index.html) framework. The `DiscountCodes` component code is as below, here are key highlights:

+ The UI is rendered using React Spectrum components, like [ComboBox](https://react-spectrum.adobe.com/react-spectrum/ComboBox.html), [ButtonGroup](https://react-spectrum.adobe.com/react-spectrum/ButtonGroup.html), [Button](https://react-spectrum.adobe.com/react-spectrum/Button.html)
+ The `adventureDiscountCodes` array has hardcoded mapping of adventure name and discount code. In real scenario, this data can be retrieved from Adobe AppBuilder action or external systems like PIM, OMS or home grown or cloud provider-based API gateway.
+ The `guestConnection` is initialized using the `useEffect` [React hook](https://react.dev/reference/react/useEffect) and managed as component state. It is used to communicate with the AEM host.
+ The `handleDiscountCodeChange` function gets the discount code for the selected adventure name and updates the state variable.
+ The `addDiscountCode` function using `guestConnection` object provides RTE instruction to execute. In this case `insertContent` instruction and HTML code snippet of actual discount code to be inserted in the RTE.

`src/aem-cf-editor-1/web-src/src/components/DiscountCodes.js`

```javascript
import {
  Button,
  ButtonGroup,
  ComboBox,
  Content,
  Divider,
  Flex, Form,
  Item,
  Provider,
  Text,
  defaultTheme
} from '@adobe/react-spectrum';
import { attach } from '@adobe/uix-guest';
import React, { useEffect, useState } from 'react';
import { extensionId } from './Constants';

const DiscountCodes = () => {

  // The Adventure Discount Code list
  // In this example its hard coded, however you can call an Adobe AppBuilder Action or even make an AJAX call to load it from 3rd party system
  const adventureDiscountCodes = [
    { id: 1, adventureName: 'BALI SURF CAMP', discountCode: 'BALI2023' },
    { id: 2, adventureName: 'BEERVANA IN PORTLAND', discountCode: 'PORTFEST' },
    { id: 3, adventureName: 'NAPA WINE TASTING', discountCode: 'WINEINSPRING' },
    { id: 4, adventureName: 'RIVERSIDE CAMPING', discountCode: 'SUMMERSCAPE' },
    { id: 5, adventureName: 'TAHOE SKIING', discountCode: 'EPICPASS' },
  ];

  // Set up state used by the React component
  const [guestConnection, setGuestConnection] = useState();

  // State hooks to manage the component state
  const [discountCode, setDiscountCode] = useState(null);

  // Asynchronously attach the extension to AEM, we must wait or the guestConnection to be set before doing anything in the modal
  useEffect(() => {
    (async () => {
      const myGuestConnection = await attach({ id: extensionId });

      setGuestConnection(myGuestConnection);
    })();
  }, []);

  // Handle the `discountCodeList` Dropdown change
  const handleDiscountCodeChange = (key) => {

    if (key) {
      //console.log(`DiscountCode Key: ${key}`);
      //console.log(`DiscountCode Value: ${adventureDiscountCodes[key-1].discountCode}`);

      //Get discount code value using selected key/index
      let discountCodeValue = adventureDiscountCodes[key - 1].discountCode;

      //update the `discountCode` state
      setDiscountCode(discountCodeValue);
    }
  };

  // Add the selected Adventure's Discount Code into the RTE
  const addDiscountCode = () => {

    if (discountCode) {
      // Use `guestConnection.host.rte.applyInstructions` method and provide RTE instruction to execute.
      // The instructions are passed as an array of object, that has `type` and `value` keys
      guestConnection.host.rte.applyInstructions([{ type: "insertContent", value: `<strong>Discount Code: ${discountCode}</strong>` }]);
    }

  };

  // Adobe React Spectrum (HTML code) that renders the Discount Code dropdown list, see https://react-spectrum.adobe.com/react-spectrum/index.html
  return (
    <Provider theme={defaultTheme}>
      <Content width="100%">
        <Flex width="100%">

          <Form width="50%">

            <Text>Selected Discount Code: <strong>{discountCode}</strong></Text>

            <p />

            <Divider size="M" />


            <ComboBox
              name="discountCodeList"
              label="Type or Select an Adventure name"
              defaultItems={adventureDiscountCodes}
              onSelectionChange={handleDiscountCodeChange}>
              {item => <Item>{item.adventureName}</Item>}
            </ComboBox>

            <p />

            <ButtonGroup align="right">
              <Button variant="accent" onPress={addDiscountCode} autoFocus>Add</Button>
              <Button variant="secondary" onPress={() => setDiscountCode(null)}>Clear</Button>
            </ButtonGroup>

          </Form>
        </Flex>
      </Content>
    </Provider>
  );
}

export default DiscountCodes;

```
