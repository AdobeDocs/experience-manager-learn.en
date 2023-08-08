---
title: Add badges to Rich Text Editor (RTE)
description: Learn how to add badges to Rich Text Editor (RTE) in the AEM Content Fragment Editor
feature: Developer Tools, Content Fragments
version: Cloud Service
topic: Development
role: Developer
level: Beginner
jira: KT-13466
thumbnail: KT-13466.jpg
doc-type: article
last-substantial-update: 2023-06-12
---

# Add badges to Rich Text Editor (RTE)

Learn how to add badges to Rich Text Editor (RTE) in the AEM Content Fragment Editor.

>[!VIDEO](https://video.tv.adobe.com/v/3420831?quality=12&learn=on)

[Rich Text Editor badge](https://developer.adobe.com/uix/docs/services/aem-cf-editor/api/rte-badges/)  are extensions that make text in the Rich Text Editor (RTE) non-editable. This means that a badge declared as such can only be completely removed and cannot be partially edited. These badges also support special coloring within the RTE, clearly indicating to content authors that the text is a badge and therefore not editable. Additionally, they provide visual cues regarding the meaning of the badge text.

The most common use case for RTE badges is to use them in conjunction with [RTE widgets](https://developer.adobe.com/uix/docs/services/aem-cf-editor/api/rte-widgets/). This allows content injected into the RTE by the RTE widget to be non-editable.

Typically, the badges in association with the widgets are used to add the dynamic content that has an external system dependency but _content authors cannot modify_ the inserted dynamic content to maintain the integrity. They can only be removed as a whole item.

The **badges** are added to the **RTE** in the Content Fragment Editor using the `rte` extension point. Using `rte` extension point's `getBadges()` method one or many badges are added.

This example shows how to add a widget called _Large Group Bookings Customer Service_ to find, select, and add the WKND adventure-specific customer service details like **Representative Name** and **Phone Number** within an RTE content. Using the badges functionality the **Phone Number** is made **non-editable** but WKND content authors can edit the Representative Name. 

Also, the **Phone Number** is styled differently (blue) which is an extra use case of the badges functionality.

To keep things simple, this example uses the [Adobe React Spectrum](https://react-spectrum.adobe.com/react-spectrum/index.html) framework to develop the widget or dialog UI and hard-coded WKND Customer Service phone numbers. To control the non-editing and different style aspect of the content, the `#` character is used in the `prefix` and `suffix` attribute of the badges definition.

## Extension points

This example extends to extension point `rte` to add a badge to the RTE in the Content Fragment Editor.

| AEM UI extended | Extension points |
| ------------------------ | --------------------- | 
| [Content Fragment Editor](https://developer.adobe.com/uix/docs/services/aem-cf-editor/) | [Rich Text Editor Badges](https://developer.adobe.com/uix/docs/services/aem-cf-editor/api/rte-badges/) and [Rich Text Editor Widgets](https://developer.adobe.com/uix/docs/services/aem-cf-editor/api/rte-widgets/) | 

## Example extension

The following example creates a _Large Group Bookings Customer Service_ widget. By pressing the `{` key within the RTE, the RTE widgets context menu is opened. By selecting the _Large Group Bookings Customer Service_ option from the context menu the custom modal is opened. 

Once the desired customer service number is added from the modal, the badges make the _Phone Number non-editable_ and styles it in blue color.

### Extension registration

`ExtensionRegistration.js`, mapped to the `index.html` route, is the entry point for the AEM extension and defines:

+ The badge's definition is defined in `getBadges()` using the configuration attributes `id`, `prefix`, `suffix`, `backgroundColor` and `textColor`.
+ In this example, the `#` character is used to define this badge's boundaries - meaning any string in the RTE that is surrounded by `#` is treated as an instance of this badge.

Also, see the key details of the RTE widget:

+ The widget definition in `getWidgets()` function with `id`, `label` and `url` attributes.
+ The `url` attribute value, a relative URL path (`/index.html#/largeBookingsCustomerService`) to load the modal.


`src/aem-cf-editor-1/web-src/src/components/ExtensionRegistration.js`

```javascript
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

          // RTE Badges
          getBadges: () => [
            {
              id: "phoneNumber",                    // Provide a unique ID for the badge
              prefix: "#",                          // Provide a Badge starting character
              suffix: "#",                          // Provide a Badge ending character
              backgroundColor: "",                  // Provide HEX or text CSS color code for the background
              textColor: "#071DF8"                  // Provide HEX or text CSS color code for the text
            }
          ],

          // RTE Widgets
          getWidgets: () => [
            {
              id: "largegroup-contact-list-widget",       // Provide a unique ID for the widget
              label: "Large Group Bookings Customer Service",          // Provide a label for the widget
              url: "/index.html#/largeBookingsCustomerService",     // Provide the "relative" URL to the widget content. It will be resolved as `/index.html#/largeBookingsCustomerService`
            },
          ],
      }
    });
  };
  
  init().catch(console.error);

  return <Text>IFrame for integration with Host (AEM)...</Text>;
}
```

### Add `largeBookingsCustomerService` route in `App.js`{#add-widgets-route}

In the main React component `App.js`, add the `largeBookingsCustomerService` route to render the UI for the above relative URL path.

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
  <Route path="/largeBookingsCustomerService" element={<LargeBookingsCustomerService />} />
</Routes>
...
```

### Create `LargeBookingsCustomerService` React component{#create-widget-react-component}

The widget or dialog UI is created using the [Adobe React Spectrum](https://react-spectrum.adobe.com/react-spectrum/index.html) framework. 

The React component code when adding the customer service details, surround the phone number variable with the `#` registered badges character to convert it into badges, like `#${phoneNumber}#`, thus make it non-editable.

Here are key highlights of `LargeBookingsCustomerService` code:

+ The UI is rendered using React Spectrum components, like [ComboBox](https://react-spectrum.adobe.com/react-spectrum/ComboBox.html), [ButtonGroup](https://react-spectrum.adobe.com/react-spectrum/ButtonGroup.html), [Button](https://react-spectrum.adobe.com/react-spectrum/Button.html)
+ The `largeGroupCustomerServiceList` array has hardcoded mapping of representative name and phone number. In real scenario, this data can be retrieved from Adobe AppBuilder action or external systems or home grown or cloud provider-based API gateway.
+ The `guestConnection` is initialized using the `useEffect` [React hook](https://react.dev/reference/react/useEffect) and managed as component state. It is used to communicate with the AEM host.
+ The `handleCustomerServiceChange` function gets representative name and phone number and  updates the component state variables.
+ The `addCustomerServiceDetails` function using `guestConnection` object provides RTE instruction to execute. In this case `insertContent` instruction and HTML code snippet.
+ To make the **phone number non-editable** using badges, the `#` special character is added before and after the `phoneNumber` variable, like `...<div><p>Phone Number: #${phoneNumber}#</strong></p></div>`. 

`src/aem-cf-editor-1/web-src/src/components/LargeBookingsCustomerService.js`

```javascript
import {
  Button,
  ButtonGroup,
  Text,
  Divider,
  ComboBox,
  Content, Flex, Form,
  Item,
  Provider, defaultTheme
} from '@adobe/react-spectrum';
import { attach } from '@adobe/uix-guest';
import React, { useEffect, useState } from 'react';
import { extensionId } from './Constants';


const LargeBookingsCustomerService = () => {

  // The Large Group Bookings Customer Service
  // In this example its hard coded, however you can call an Adobe AppBuilder Action or even make an AJAX call to load it from 3rd party system
  const largeGroupCustomerServiceList = [
    { id: 1, repName: 'Max', phoneNumber: '1-800-235-1000' },
    { id: 2, repName: 'John', phoneNumber: '1-700-235-2000' },
    { id: 3, repName: 'Leah', phoneNumber: '1-600-235-3000' },
    { id: 4, repName: 'Leno', phoneNumber: '1-500-235-4000' }
  ];

  // Set up state used by the React component
  const [guestConnection, setGuestConnection] = useState();

  // State hooks to manage the component state
  const [repName, setRepName] = useState(null);
  const [phoneNumber, setPhoneNumber] = useState(null);

  // Asynchronously attach the extension to AEM, we must wait or the guestConnection to be set before doing anything in the modal
  useEffect(() => {
    (async () => {
      const myGuestConnection = await attach({ id: extensionId });

      setGuestConnection(myGuestConnection);
    })();
  }, []);

  // Handle the `customerService` Dropdown change
  const handleCustomerServiceChange = (id) => {

    if (id) {
      //Get Customer Service RepName and Phone Number values using selected id

      const rep = largeGroupCustomerServiceList.filter((r) => r.id === id)[0];

      //update the `repName` state
      setRepName(rep?.repName);

      //update the `phoneNumber` state
      setPhoneNumber(rep?.phoneNumber);
    }
  };

  // Add the selected Customer Service details into the RTE
  const addCustomerServiceDetails = () => {

    if (repName && phoneNumber) {
      // Use `guestConnection.host.rte.applyInstructions` method and provide RTE instruction to execute.
      // The instructions are passed as an array of object, that has `type` and `value` keys
      guestConnection.host.rte.applyInstructions([{ type: "insertContent", value: `<div><p>Representative Name: <strong>${repName}</strong></p></div><div><p>Phone Number: #${phoneNumber}#</strong></p></div>` }]);
    }
  };


  // Adobe React Spectrum (HTML code) that renders the Customer Service dropdown list, see https://react-spectrum.adobe.com/react-spectrum/index.html
  return (
    <Provider theme={defaultTheme}>
      <Content width="100%">
        <Flex width="100%">

          <Form width="50%">
            <Text>Representative Name: <strong>{repName}</strong></Text>
            <Text>Phone Number: <strong>{phoneNumber}</strong></Text>

            <p />

            <Divider size="M" />


            <ComboBox
              name="customerService"
              label="Type or Select Phone Number"
              defaultItems={largeGroupCustomerServiceList}
              onSelectionChange={handleCustomerServiceChange}>
              {item => <Item>{item.phoneNumber}</Item>}
            </ComboBox>

            <p />

            <ButtonGroup align="right">
              <Button variant="accent" onPress={addCustomerServiceDetails}>Add</Button>
              <Button variant="secondary" onPress={() => {setPhoneNumber(null); setRepName(null);}}>Clear</Button>
            </ButtonGroup>

          </Form>
        </Flex>
      </Content>
    </Provider>
  );

};

export default LargeBookingsCustomerService;

```
