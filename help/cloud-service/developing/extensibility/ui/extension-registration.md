---
title: AEM UI extension registration
description: Learn how to register an AEM UI extension.
feature: Developer Tools
version: Experience Manager as a Cloud Service
topic: Development
role: Developer
level: Beginner
recommendations: noDisplay, noCatalog
jira: KT-11603
last-substantial-update: 2023-06-02
exl-id: ef2290d9-ba40-429b-b10d-e82d6c1c20f6
duration: 85
---
# Extension registration

AEM UI extensions are specialized App Builder app, based on React and use the [React Spectrum](https://react-spectrum.adobe.com/react-spectrum/) UI framework. 

To define where and how the AEM UI extension appears, two configurations are required in the extension's App Builder app: app routing and the extension registration.

## App routes{#app-routes}

The extension's `App.js` declares the [React router](https://reactrouter.com/en/main) that includes an index route that registers the extension in the AEM UI.

The index route is invoked when the AEM UI initially loads, and target of this route defines how the extension is exposed in the console.

+ `./src/aem-ui-extension/web-src/src/components/App.js`

```javascript
import ExtensionRegistration from "./ExtensionRegistration"
...            
function App(props) {
  return (
    <Router>
      <ErrorBoundary onError={onError} FallbackComponent={fallbackComponent}>
        <Routes>
          {/* The index route maps to the extension registration */}
          <Route index element={<ExtensionRegistration />} />
          ...                                   
        </Routes>
      </ErrorBoundary>
    </Router>
  )
  ...
}
```

## Extension registration

`ExtensionRegistration.js` must be immediately loaded via the index route of the extension, and acts the registration point of the extension.

Based on the AEM UI extension template selected when [initializing the App Builder app extension](./app-initialization.md), different extension points are supported.

+ [Content Fragments UI extension points](./content-fragments/overview.md#extension-points)

## Conditionally include extensions

AEM UI extensions can execute custom logic to limit the AEM environments the extension appears in. This check is performed before the `register` call in the `ExtensionRegistration` component, and immediately returns if the extension should not be displayed.

This check has limited context available:

+ The AEM host that the extension is loading on.
+ The current user's AEM access token.

The most common checks for loading an extension are:

+ Using the AEM host (`new URLSearchParams(window.location.search).get('repo')`) to determine if the extension should load.
  + Only show the extension on AEM environments that are part of a specific program (as shown in the example below).
  + Only show the extension on a specific AEM environment (AEM host).
+ Using an [Adobe I/O Runtime action](./runtime-action.md) to make an HTTP call to AEM to determine if the current user should see the extension.

The example below illustrates limiting the extension to all environments in program `p12345`.

+ `./src/aem-cf-console-admin-1/web-src/src/components/ExtensionRegistration.js`

```javascript
function ExtensionRegistration() {
  const PROGRAM_ID = 'p12345';

  // Get the current AEM Host (author-pXXX-eYYY.adobeaemcloud.com) the extension is loading on
  const aemHost = new URLSearchParams(window.location.search).get('repo');

  // Create a check to determine if the current AEM host matches the AEM program that uses this extension 
  const aemHostRegex = new RegExp(`^author-${PROGRAM_ID}-e[\\d]+\\.adobeaemcloud\\.com$`)

  // Disable the extension if the Cloud Manager Program Id doesn't match the regex.
  if (!aemHostRegex.test(aemHost)) {
    return; // Skip extension registration if the environment is not in program p12345.
  }

  // Else, continue initializing the extension
  const init = async () => { .. };
  
  init().catch(console.error);
}
```
