---
title: AEM Content Fragment console action bar extensions
description: Learn how to create an AEM Content Fragment console action bar extensions.
feature: Developer Tools
version: Cloud Service
topic: Development
role: Developer
level: Beginner
recommendations: noDisplay, noCatalog
kt: 11603
last-substantial-update: 2022-12-01
exl-id: 97d26a1f-f9a7-4e57-a5ef-8bb2f3611088
---
# Action bar extension

![Action bar extension](./assets/action-bar/action-bar.png){align="center"}

Extensions that include a action bar, introduce a button to the action of the AEM Content Fragment Console that displays when __1 or more__ Content Fragments are selected. Because action bar extension buttons only display when at least one Content Fragment is selected, they typically act upon the selected Content Fragments. Examples include:

+ Invoking a business process or workflow on the selected Content Fragments.
+ Updating or changing the data of the select Content Fragments.

## Extension registration

`ExtensionRegistration.js` is the entry point for the AEM extension and defines:

1. The extension type; in the case a action bar button.
1. The extension button's definition, in `getButton()` function.
1. The click handler for the button, in the `onClick()` function.

+ `./src/aem-cf-console-admin-1/web-src/src/components/ExtensionRegistration.js`

```javascript
function ExtensionRegistration() {
  const init = async () => {
    const guestConnection = await register({
      id: extensionId,
      methods: {
        // Configure your Action Bar button here
        actionBar: {
          getButton() {
            return {
              'id': 'example.my-action-bar-button',     // Unique ID for the button
              'label': 'My action bar button',          // Button label 
              'icon': 'Edit'                            // Button icon; get name from: https://spectrum.adobe.com/page/icons/ (Remove spaces, keep uppercase)
            }
          },
          // Click handler for the Action Bar extension button
          onClick(selections) {
            // Action Bar buttons require the selection of at least 1 Content Fragment, 
            // so we can assume the extension will do something with these selections

            // Collect the selected content fragment paths from the selections parameter
            const selectionIds = selections.map(selection => selection.id);
            
            // Do some work with the selected content fragments
            doWork(selectionIds);          
        }
      }
    })
  }
  init().catch(console.error)
```

## Modal

![Modal](./assets/modal/modal.png)

AEM Content Fragment Console action bar extensions may require:

+ Additional input from the user to perform the desired action.
+ The ability to provide the user details information about the result of the action.

To support these requirements, the AEM Content Fragment Console extension allows a custom modal that renders as a React application.

+ `./src/aem-cf-console-admin-1/web-src/src/components/ExtensionRegistration.js`

```javascript
function ExtensionRegistration() {
  ...
  onClick(selections) {
    // Collect the selected content fragment paths 
    const contentFragmentPaths = selections.map(selection => selection.id);

    // Create a URL that maps to the React route to be rendered in the modal 
    const modalURL = "/index.html#" + generatePath(
      "/content-fragment/:selection/my-extension",
      {
        // Set the :selection React route parameter to an encoded, delimited list of paths of the selected content fragments
        selection: encodeURIComponent(contentFragmentPaths.join('|'))
      }
    );

    // Open the modal and display the React route created above
    guestConnection.host.modal.showUrl({
      title: "My modal title",
      url: modalURL
    })     
  } ...     
} ...
```

<div class="column is-8-desktop is-full-mobile is-half-tablet" style="
    border: solid 1px #ccc;
    border-radius: 10px;
    margin: 4rem auto;
">
  <div class="is-flex is-padded-small is-padded-big-mobile">
    <div>
      <p class="has-text-weight-bold is-size-36 is-size-27-touch is-margin-bottom-big has-text-blackest">Skip to creating a modal</p>
      <p class="has-text-blackest">Learn how to create a modal that is displayed when clicking the action bar extension button.</p>
      <div class="has-align-start is-margin-top-big">
        <a href="./modal.md" target="_blank" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM">
          <span class="spectrum-Button-label has-no-wrap has-text-weight-bold" title="Learn to build a modal">Learn to build a modal</span>
        </a>
      </div>
    </div>
  </div>
</div>

## No modal

Occasionally, AEM Content Fragment console Action Bar extensions do not require further interaction with the user, for example:

+ Invoking a back-end process that does not require user input, such as import or export.

In these instances, the AEM Content Fragment console extension does not require a [modal](#modal), and perform the work directly in the action bar button's `onClick` handler.

The AEM Content Fragment console extension allows for a progress indicator to overlay the AEM Content Fragment console while the work is being performed, blocking the user from performing further actions. The use of the the progress indicator is optional, but useful for communicating the progress of synchronous work to the user.

+ `./src/aem-cf-console-admin-1/web-src/src/components/ExtensionRegistration.js`

```javascript
function ExtensionRegistration() {
  guestConnection: { ...
    methods: { ...
      actionBar: { ...
        onClick(selections) {
          // Collect the selected content fragment paths 
          const contentFragmentPaths = selections.map(selection => selection.id);

          // Optionally, show the progress indicator overlay on the AEM Content Fragment console
          guestConnection.host.progressCircle.start();
          // Perform work on the selected Content Fragments
          doWork(contentFragmentPaths);
          // Hide the progress indicator overlay on the AEM Content Fragment console when the work is done
          guestConnection.host.progressCircle.stop();
        }
      }
    }
  }
}
```
