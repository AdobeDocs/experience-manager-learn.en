---
title: Add custom button to Rich Text Editor (RTE) toolbar
description: Learn how to add a custom button to Rich Text Editor (RTE) toolbar in the AEM Content Fragment Editor
feature: Developer Tools, Content Fragments
version: Cloud Service
topic: Development
role: Developer
level: Beginner
jira: KT-13464
thumbnail: KT-13464.jpg
doc-type: article
last-substantial-update: 2023-06-12
---

# Add custom button to Rich Text Editor (RTE) toolbar

![Content Fragment Editor toolbar extension example](./assets/rte/rte-toolbar-hero.png){align="center"}

Custom buttons can be added to the **RTE toolbar** in the Content Fragment Editor using the `rte` extension point. This example shows how to add a custom button called _Add Tip_ to the RTE toolbar and modify the content within the RTE.

Using `rte` extension point's `getCustomButtons()` method one or many custom buttons can be added to the **RTE toolbar**. It is also possible to add or remove standard RTE buttons like _Copy, Paste, Bold, and Italic_ using `getCoreButtons()` and `removeButtons)` methods respectively.

This example shows how to insert a highlighted note or tip using custom _Add Tip_ toolbar button. The highlighted note or tip content has a special formatting applied via HTML elements, and the associated CSS classes. The placeholder content and HTML code are inserted using the `onClick()` callback method of the `getCustomButtons()`.

## Extension point

This example extends to extension point `rte` to add custom button to RTE toolbar in the Content Fragment Editor.

| AEM UI extended | Extension point |
| ------------------------ | --------------------- | 
| [Content Fragment Editor](https://developer.adobe.com/uix/docs/services/aem-cf-editor/) | [Rich Text Editor Toolbar](https://developer.adobe.com/uix/docs/services/aem-cf-editor/api/rte-toolbar/) | 

## Example extension

The following example creates an _Add Tip_ custom button in the RTE toolbar. The click action inserts the placeholder text at the current caret position in the RTE.

The code shows how to add the custom button with an icon and register the click handler function.

### Extension registration

`ExtensionRegistration.js`, mapped to the index.html route, is the entry point for the AEM extension and defines:

+ The RTE toolbar button's definition in `getCustomButtons()` function with `id, tooltip and icon` attributes.
+ The click handler for the button, in the `onClick()` function. 
+ The click handler function receives the `state` object as an argument to get the RTE's content in HTML or text format. However in this example it's not used.
+ The click handler function returns an instructions array. This array has an object with `type` and `value` attributes. To insert the content, the `value` attributes HTML code snippet, the `type` attribute uses the `insertContent`. If there is a use case to replace the content, use case the `replaceContent` instruction type.

The `insertContent` value is a HTML string, `<div class=\"cmp-contentfragment__element-tip\"><div>TIP</div><div>Add your tip text here...</div></div>`. The CSS classes `cmp-contentfragment__element-tip` used to display the value are not defined in the widget, but rather implemented on the web experience this Content Fragment field is displayed on.


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

          // RTE Toolbar custom button
          getCustomButtons: () => ([
            {
              id: "wknd-cf-tip",       // Provide a unique ID for the custom button
              tooltip: "Add Tip",      // Provide a label for the custom button
              icon: 'Note',            // Provide an icon for the button (see https://spectrum.adobe.com/page/icons/ for a list of available icons)
              onClick: (state) => {    // Provide a click handler function that returns the instructions array with type and value. This example inserts the HTML snippet for TIP content.
                return [{
                  type: "insertContent",
                  value: "<div class=\"cmp-contentfragment__element-tip\"><div>TIP</div><div>Add your tip text here...</div></div>"
                }];
              },
            },
          ]),
      }
    });
  };
  
  init().catch(console.error);

  return <Text>IFrame for integration with Host (AEM)...</Text>;
}
```
