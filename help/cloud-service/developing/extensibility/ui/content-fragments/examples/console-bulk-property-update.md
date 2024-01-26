---
title: Bulk property update example AEM Content Fragment Console extension
description: An example AEM Content Fragments Console extension that bulk updates a property of Content Fragments.
feature: Developer Tools, Content Fragments
version: Cloud Service
topic: Development
role: Developer
level: Beginner
jira: KT-11604
thumbnail: KT-11604.png
doc-type: article
last-substantial-update: 2024-01-26
exl-id: fbfb5c10-95f8-4875-88dd-9a941d7a16fd
duration: 1319
---
# Bulk property update example extension

>[!VIDEO](https://video.tv.adobe.com/v/3412296?quality=12&learn=on)

This example AEM Content Fragment Console extension is an [action bar](https://developer.adobe.com/uix/docs/services/aem-cf-console-admin/api/action-bar/) extension that bulk updates a Content Fragment property to a common value.

The functional flow of the example extension is as follows:

![Adobe I/O Runtime action flow](./assets/bulk-property-update/flow.png){align="center"}

1. Select Content Fragments and clicking the extension's button in the [action bar](#extension-registration) opens the [modal](#modal).
2. The [modal](#modal) displays a custom input form built with [React Spectrum](https://react-spectrum.adobe.com/react-spectrum/).
3. Submitting the form sends the list of selected Content Fragments, and the AEM host to the [custom Adobe I/O Runtime action](#adobe-io-runtime-action).
4. The [Adobe I/O Runtime action](#adobe-io-runtime-action) validates the inputs and makes HTTP PUT requests to AEM to update the selected Content Fragments.
5. A series of HTTP PUTs for each Content Fragment to update the specified property.
6. AEM as a Cloud Service persists the property updates to the Content Fragment and returns success or failure responses to the Adobe I/O Runtime action.
7. The modal received the response from the Adobe I/O Runtime action, and displays a list of successful bulk updates.

## Extension point

This example extends to extension point `actionBar` to add custom button to the Content Fragment Console.

| AEM UI extended | Extension point |
| ------------------------ | --------------------- | 
| [Content Fragment Console](https://developer.adobe.com/uix/docs/services/aem-cf-console-admin/) | [Action Bar](https://developer.adobe.com/uix/docs/services/aem-cf-console-admin/api/action-bar/) | 


## Example extension

The example uses an existing Adobe Developer Console project, and uses the following options when initializing the App Builder app, via `aio app init`.

+ What templates do you want to search for?: `All Extension Points`
+ Choose the template(s) to install:` @adobe/aem-cf-admin-ui-ext-tpl`
+ What do you want to name your extension?: `Bulk property update`
+ Please provide a short description of your extension: `An example action bar extension that bulk updates a single property one or more content fragments.`
+ What version would you like to start with?: `0.0.1`
+ What would you like to do next?
  + `Add a custom button to Action Bar`
    + Please provide label name for the button: `Bulk property update`
    + Do you need to show a modal for the button? `y`
  + `Add server-side handler`
    + Adobe I/O Runtime lets you invoke serverless code on demand. How would you like to name this action?: `generic`

The generated App Builder extension app is updated as described below.

### App routes{#app-routes}

The `src/aem-cf-console-admin-1/web-src/src/components/App.js` contains the [React router](https://reactrouter.com/en/main). 

There are two logical sets of routes:

1. The first route maps requests to the `index.html`, which invokes the React component responsible for the [extension registration](#extension-registration).

    ```javascript
    <Route index element={<ExtensionRegistration />} />
    ```

1. The second set of routes maps URLs to React components that render the contents of the extension's modal. The `:selection` param represents a delimited list content fragment path. 

    If the extension has multiple buttons to invoke discrete actions, each [extension registration](#extension-registration) maps to a route defined here.

    ```javascript
    <Route
        exact path="content-fragment/:selection/bulk-property-update"
        element={<BulkPropertyUpdateModal />}
        />
    ```

### Extension registration

`ExtensionRegistration.js`, mapped to the `index.html` route, is the entry point for the AEM extension and defines:

1. The location of the extension button appears in the AEM authoring experience (`actionBar` or `headerMenu`)
1. The extension button's definition in `getButtons()` function
1. The click handler for the button, in the `onClick()` function

+ `src/aem-cf-console-admin-1/web-src/src/components/ExtensionRegistration.js`

```javascript
import React from "react";
import { generatePath } from "react-router";
import { Text } from "@adobe/react-spectrum";
import { register } from "@adobe/uix-guest";
import { extensionId } from "./Constants";

function ExtensionRegistration() {
  const init = async () => {
    const guestConnection = await register({
      id: extensionId, // Some unique ID for the extension used to facilitate communication between the extension and Content Fragment Console
      methods: {
        // Configure your Action Bar button here
        actionBar: {
          getButtons() {
            return [
              {
                id: "examples.action-bar.bulk-property-update", // Unique ID for the button
                label: "Bulk property update", // Button label
                icon: "OpenIn", // Button icon; get name from: https://spectrum.adobe.com/page/icons/ (Remove spaces, keep uppercase)
                // Click handler for the extension button
                onClick(selections) {
                  // Collect the selected content fragment paths
                  const selectionIds = selections.map(
                    (selection) => selection.id
                  );

                  // Create a URL that maps to the
                  const modalURL =
                    "/index.html#" +
                    generatePath(
                      "/content-fragment/:selection/bulk-property-update",
                      {
                        // Set the :selection React route parameter to an encoded, delimited list of paths of the selected content fragments
                        selection: encodeURIComponent(selectionIds.join("|")),
                      }
                    );

                  // Open the route in the extension modal using the constructed URL
                  guestConnection.host.modal.showUrl({
                    // The modal title
                    title: "Bulk property update",
                    url: modalURL,
                  });
                },
              },
            ];
          },
        },
      },
    });
  };

  init().catch(console.error);

  return <Text>IFrame for integration with Host (AEM)...</Text>;
}

export default ExtensionRegistration;
```

### Modal

Each route of the extension, as defined in [`App.js`](#app-routes), maps to a React component that renders in the extension's modal. 

In this example app, there is a modal React component (`BulkPropertyUpdateModal.js`) that has three states:

1. Loading, indicating the user must wait
1. The Bulk Property Update form that allows the user to specify the property name and value to update
1. The response of the bulk property update operation, listing the content fragments that were updated, and those that could not be updated

Importantly, any interaction with AEM from the extension should be delegated to an [AppBuilder Adobe I/O Runtime action](https://developer.adobe.com/runtime/docs/guides/using/creating_actions/), which is a separate serverless process running in [Adobe I/O Runtime](https://developer.adobe.com/runtime/docs/).
The use of Adobe I/O Runtime actions to communicate with AEM is to avoid Cross-Origin Resource Sharing (CORS) connectivity issues.

When the Bulk Property Update form is submitted, a custom `onSubmitHandler()` invokes the Adobe I/O Runtime action, passing the current AEM host (domain) and user's AEM access token, which in turn calls the [AEM Content Fragment API](https://experienceleague.adobe.com/docs/experience-manager-65/assets/extending/assets-api-content-fragments.html) to update the content fragments.

When the response from the Adobe I/O Runtime action is received, the modal is updated to display the results of the bulk property update operation.

+ `src/aem-cf-console-admin-1/web-src/src/components/BulkPropertyUpdateModal.js`

```javascript
import React, { useState, useEffect } from 'react'
import { attach } from "@adobe/uix-guest"
import {
  Flex,
  Form,
  Provider,
  Content,
  defaultTheme,
  ContextualHelp,
  Text,
  TextField,
  ButtonGroup,
  Button,
  Heading,
  ListView,
  Item,
} from '@adobe/react-spectrum'

import Spinner from "./Spinner"

import { useParams } from "react-router-dom"

import allActions from '../config.json'
import actionWebInvoke from '../utils'

import { extensionId } from "./Constants"

export default function BulkPropertyUpdateModal() {
  // Set up state used by the React component
  const [guestConnection, setGuestConnection] = useState()
  
  const [actionInvokeInProgress, setActionInvokeInProgress] = useState(false);
  const [actionResponse, setActionResponse] = useState();

  const [propertyName, setPropertyName] = useState(null);
  const [propertyValue, setPropertyValue] = useState(null);
  const [validationState, setValidationState] = useState({});

  // Get the selected content fragment paths from the route parameter `:selection`
  let { selection } = useParams();
  let fragmentIds = selection?.split('|') || [];
  
  console.log('Content Fragment Ids', fragmentIds);

  if (!fragmentIds || fragmentIds.length === 0) {
    console.error("Unable to locate a list of Content Fragments to update.")
    return;
  }

  // Asynchronously attach the extension to AEM, we must wait or the guestConnection to be set before doing anything in the modal
  useEffect(() => {
    (async () => {
       // extensionId is the unique id of this extension (you can make this up as long as its unique) .. in this case its `bulk-property-update` pulled out into Constants.js as it is also referenced in ExtensionRegistration.js
      const guestConnection = await attach({ id: extensionId })
      setGuestConnection(guestConnection);
    })()
  }, [])


  // Determine view to display in the modal
  if (!guestConnection) {
    // If the guestConnection is not initialized, display a loading spinner
    return <Spinner />
  } else if (actionInvokeInProgress) {
    // If the bulk property action has been invoked but not completed, display a loading spinner
    return <Spinner />
  } else if (actionResponse) {
    // If the bulk property action has completed, display the response
    return renderResponse();
  } else {
    // Else display the bulk property update form
    return renderForm();
  }

  /**
   * Renders the Bulk Property Update form. 
   * This form has two fields:
   * - Property Name: The name of the Content Fragment property name to update
   * - Property Value: the value the Content Fragment property, specified by the Property Name, will be updated to
   * 
   * @returns the Bulk Property Update form
   */
  function renderForm() {
    return (
      // Use React Spectrum components to render the form
      <Provider theme={defaultTheme} colorScheme='light'>
        <Content width="100%">
          <Flex width="100%">
            <Form 
              width="100%">
              <TextField label="Property name"
                          isRequired={true}
                          validationState={validationState?.propertyName}
                onChange={setPropertyName}
                contextualHelp={
                  <ContextualHelp>
                    <Heading>Need help?</Heading>
                    <Content>
                      <Text>The <strong>Property name</strong> must be a valid for the Content Fragment model(s) the selected Content Fragments implement.</Text>
                    </Content>
                  </ContextualHelp>
                } />

              <TextField
                label="Property value"
                validationState={validationState?.propertyValue}
                onChange={setPropertyValue} />

              <ButtonGroup align="start" marginTop="size-200">
                <Button variant="cta" onPress={onSubmitHandler}>Update {fragmentIds.length} Content Fragments</Button>
              </ButtonGroup>
            </Form>
          </Flex>

          {/* Render the close button so the user can close the modal */}
          {renderCloseButton()}
        </Content>
      </Provider>
    )
  }
  /**
   * Display the response from the Adobe I/O Runtime action in the modal.
   * This includes:
   * - A list of content fragments that were updated successfully
   * - A list a content fragments that failed to update
   * 
   * @returns the response view
   */
  function renderResponse() {
    // Separate the successful and failed content fragments updates
    const successes = actionResponse.filter(item => item.status === 200);
    const failures = actionResponse.filter(item => item.status !== 200);

    return (
      <Provider theme={defaultTheme} colorScheme='light'>
        <Content width="100%">

          <Text>Bulk updated property <strong>{propertyName}</strong> with value <strong>{propertyValue}</strong></Text>

          {/* Render the list of content fragments that were updated successfully */}
          {successes.length > 0 &&
            <><Heading level="4">{successes.length} Content Fragments successfully updated</Heading>
              <ListView
                items={successes}
                selectionMode="none"
                aria-label="Successful updates"
              >
                {(item) => (
                  <Item key={item.fragmentId} textValue={item.fragmentId.split('/').pop()}>
                    {item.fragmentId.split('/').pop()}
                  </Item>
                )}
              </ListView></>}

          {/* Render the list of content fragments that failed to update */}
          {failures.length > 0 &&
            <><Heading level="4">{failures.length} Content Fragments failed to update</Heading><ListView
              items={failures}
              selectionMode="none"
              aria-label="Failed updates"
            >
              {(item) => (
                <Item key={item.fragmentId} textValue={item.fragmentId.split('/').pop()}>
                  {item.fragmentId.split('/').pop()}
                </Item>
              )}
            </ListView></>}

          {/* Render the close button so the user can close the modal */}
          {renderCloseButton()}
        </Content>
      </Provider>);
  }

  /**
   * Provide a close button for the modal, else it cannot be closed (without refreshing the browser window)
   * 
   * @returns a button that closes the modal.
   */
   function renderCloseButton() {
    return (
      <Flex width="100%" justifyContent="end" alignItems="center" marginTop="size-400">
        <ButtonGroup align="end">
          <Button variant="primary" onPress={() => guestConnection.host.modal.close()}>Close</Button>
        </ButtonGroup>
      </Flex>
    );
  }

  /**
   * Handle the Bulk Property Update form submission.
   * This function calls the supporting Adobe I/O Runtime action to update the selected Content Fragments, and then returns the response for display in the modal
   * When invoking the Adobe I/O Runtime action, the following parameters are passed as they're used by the action to connect to AEM:
   * - AEM Host to connect to
   * - AEM access token to connect to AEM with
   * - The list of Content Fragment paths to update
   * - The Content Fragment property name to update
   * - The value to update the Content Fragment property to
   * 
   * @returns a list of content fragment update successes and failures
   */
  async function onSubmitHandler() {
    // Validate the form input fields
    if (propertyName?.length > 1) {
      setValidationState({propertyName: 'valid', propertyValue: 'valid'});
    } else {
      setValidationState({propertyName: 'invalid', propertyValue: 'valid'});
      return;
    }

    // Mark the extension as invoking the action, so the loading spinner is displayed
    setActionInvokeInProgress(true);

    // Set the HTTP headers to access the Adobe I/O runtime action
    const headers = {
      'Authorization': 'Bearer ' + guestConnection.sharedContext.get('auth').imsToken,
      'x-gw-ims-org-id': guestConnection.sharedContext.get('auth').imsOrg
    };

    console.log('headers', headers);

    // Set the parameters to pass to the Adobe I/O Runtime action
    const params = {
      aemHost: `https://${guestConnection.sharedContext.get('aemHost')}`,

      fragmentIds: fragmentIds,
      propertyName: propertyName,
      propertyValue: propertyValue
    };

    // Invoke the Adobe I/O Runtime action named `generic`. This name defined in the `ext.config.yaml` file.
    const action = 'generic';

    try {
      // Invoke Adobe I/O Runtime action with the configured headers and parameters
      const actionResponse = await actionWebInvoke(allActions[action], headers, params);

      // Set the response from the Adobe I/O Runtime action
      setActionResponse(actionResponse);

      console.log(`Response from ${action}:`, actionResponse)
    } catch (e) {
      // Log and store any errors
      console.error(e)
    }

    // Set the action as no longer being invoked, so the loading spinner is hidden
    setActionInvokeInProgress(false);
  }
}
```


### Adobe I/O Runtime action

An AEM extension App Builder app can define or use 0 or many Adobe I/O Runtime actions. 
Adobe Runtime actions should be responsible work that requires interacting with AEM, or other Adobe web services.

In this example app, the Adobe I/O Runtime action - which uses the default name `generic` - is responsible for:

1. Making a series of HTTP requests to the AEM Content Fragment API to update the content fragments.
1. Collecting the responses of these HTTP requests, collating them into successes and failures
1. Returning the list of successes and failure for display by the modal (`BulkPropertyUpdateModal.js`)

+ `src/aem-cf-console-admin-1/actions/generic/index.js`


```javascript

const fetch = require('node-fetch')
const { Core } = require('@adobe/aio-sdk')
const { errorResponse, getBearerToken, stringParameters, checkMissingRequestInputs } = require('../utils')

// main function that will be executed by Adobe I/O Runtime
async function main (params) {
  // create a Logger
  const logger = Core.Logger('main', { level: params.LOG_LEVEL || 'info' })

  try {
    // 'info' is the default level if not set
    logger.info('Calling the main action')

    // log parameters, only if params.LOG_LEVEL === 'debug'
    logger.debug(stringParameters(params))

    // check for missing request input parameters and headers
    const requiredParams = [ 'aemHost', 'fragmentIds', 'propertyName', 'propertyValue' ]
    const requiredHeaders = ['Authorization']
    const errorMessage = checkMissingRequestInputs(params, requiredParams, requiredHeaders)
    if (errorMessage) {
      // return and log client errors
      return errorResponse(400, errorMessage, logger)
    }
      
    const body = {
      "properties": {
        "elements": {
          [params.propertyName]: {
            "value": params.propertyValue
          }
        }
      }
    };

    // Extract the user Bearer token from the Authorization header used to authenticate the request to AEM
    const accessToken = getBearerToken(params);

    let results = await Promise.all(params.fragmentIds.map(async (fragmentId) => {

      logger.info(`Updating fragment ${fragmentId} with property ${params.propertyName} and value ${params.propertyValue}`);

      const res = await fetch(`${params.aemHost}${fragmentId.replace('/content/dam/', '/api/assets/')}.json`, { 
        method: 'put',
        body: JSON.stringify(body),
        headers: {
          'Authorization': `Bearer ${accessToken}`,
          'Content-Type': 'application/json'
        }
      });

      if (res.ok) {
        logger.info(`Successfully updated ${fragmentId}`);
        return { fragmentId, status: res.status, statusText: res.statusText, body: await res.json() };
      } else {
        logger.info(`Failed to update ${fragmentId}`);
        return { fragmentId, status: res.status, statusText: res.statusText, body: await res.text() };
      }
    }));

    const response = {
      statusCode: 200,
      body: results
    };

    logger.info('Adobe I/O Runtime action response', response);

    // Return the response to the A
     return response;

  } catch (error) {
    // log any server errors
    logger.error(error)
    // return with 500
    return errorResponse(500, 'server error', logger)
  }
}

exports.main = main

```
