---
title: Generate access token in App Builder action
description: Learn how to generate an access token using JWT credentials for use in an App Builder action.
feature: Developer Tools
version: Cloud Service
topic: Development
role: Developer
level: Intermediate
jira: KT-11743
last-substantial-update: 2023-01-17
exl-id: 9a3fed96-c99b-43d1-9dba-a4311c65e5b9
duration: 194
---
# Generate access token in App Builder action

App Builder actions may need to interact with Adobe APIs associated with Adobe Developer Console projects the App Builder app is deployed too.

This may require the App Builder action to generate its own access token associated with the desired Adobe Developer Console project.

>[!IMPORTANT]
>
> Review [App Builder security documentation](https://developer.adobe.com/app-builder/docs/guides/security/) to understand when it is appropriate to generate access tokens versus using provided access tokens. 
>
> The custom action may need to provide its own security checks to ensure that only allowed consumers can access the App Builder action, and the Adobe services behind it.


## .env file

In the App Builder project's `.env` file, append custom keys for each of Adobe Developer Console project's JWT credentials. The JWT credential values can be obtained from the Adobe Developer Console project's __Credentials__ > __Service Account (JWT)__ for a given workspace.

![Adobe Developer Console JWT Service Credentials](./assets/jwt-auth/jwt-credentials.png)

```
...
JWT_CLIENT_ID=58b23182d80a40fea8b12bc236d71167
JWT_CLIENT_SECRET=p8e-EIRF6kY6EHLBSdw2b-pLUWKodDqJqSz3
JWT_TECHNICAL_ACCOUNT_ID=1F072B8A63C6E0230A495EE1@techacct.adobe.com
JWT_IMS_ORG=7ABB3E6A5A7491460A495D61@AdobeOrg
JWT_METASCOPES=https://ims-na1.adobelogin.com/s/ent_analytics_bulk_ingest_sdk,https://ims-na1.adobelogin.com/s/event_receiver_api
JWT_PRIVATE_KEY=LS0tLS1C..kQgUFJJVkFURSBLRVktLS0tLQ==
```

The values for `JWT_CLIENT_ID`, `JWT_CLIENT_SECRET`, `JWT_TECHNICAL_ACCOUNT_ID`, `JWT_IMS_ORG` can be directly copied from the Adobe Developer Console project's JWT Credentials screen.

### Metascopes

Determine the Adobe APIs and their metascopes the App Builder action interacts with. List metascopes with comma delimiters in the `JWT_METASCOPES` key. Valid metascopes are listed in [Adobe's JWT Metascope documentation](https://developer.adobe.com/developer-console/docs/guides/authentication/JWT/Scopes/).


For example, the following value might be added to the `JWT_METASCOPES` key in the `.env`:

```
...
JWT_METASCOPES=https://ims-na1.adobelogin.com/s/ent_analytics_bulk_ingest_sdk,https://ims-na1.adobelogin.com/s/event_receiver_api
...
```

### Private key

The `JWT_PRIVATE_KEY` must be specially formatted as it is natively a multi-line value, which is not supported in `.env` files. The easiest way is to base64 encode the private key. Base64 encoding the private key (`-----BEGIN PRIVATE KEY-----\n...\n-----END PRIVATE KEY-----`) can be done using native tools provided by your operating system.

>[!BEGINTABS]

>[!TAB macOS]

1. Open `Terminal`
1. Run the comamnd `base64 -i /path/to/private.key | pbcopy`
1. The base64 output is automatically copied the clipboard
1. Paste into `.env` as value to corresponding key

>[!TAB Windows]

1. Open `Command Prompt`
1. Run the comamnd `certutil -encode C:\path\to\private.key C:\path\to\encoded-private.key`
1. Run the comamnd `findstr /v CERTIFICATE C:\path\to\encoded-private.key`
1. Copy the base64 output to the clipboard
1. Paste into `.env` as value to corresponding key

>[!TAB Linux&reg;]

1. Open terminal
1. Run the comamnd `base64 private.key`
1. Copy the base64 output to the clipboard
1. Paste into `.env` as value to corresponding key

>[!ENDTABS]

For example, the following base64-encoded private key might be added to the `JWT_PRIVATE_KEY` key in the `.env`:

```
...
JWT_PRIVATE_KEY=LS0tLS1C..kQgUFJJVkFURSBLRVktLS0tLQ==
```

## Inputs mapping

With the JWT credential value set in the `.env` file, they must be mapped to AppBuilder action inputs to they can be read in the action itself. To do this, add entries for each variable in the `ext.config.yaml` action `inputs` in the format: `PARAMS_INPUT_NAME: $ENV_KEY`.

For example:

```yaml
operations:
  view:
    - type: web
      impl: index.html
actions: actions
runtimeManifest:
  packages:
    dx-excshell-1:
      license: Apache-2.0
      actions:
        generic:
          function: actions/generic/index.js
          web: 'yes'
          runtime: nodejs:16
          inputs:
            LOG_LEVEL: debug
            JWT_CLIENT_ID: $JWT_CLIENT_ID
            JWT_TECHNICAL_ACCOUNT_ID: $JWT_TECHNICAL_ACCOUNT_ID
            JWT_IMS_ORG: $JWT_IMS_ORG
            JWT_METASCOPES: $JWT_METASCOPES
            JWT_PRIVATE_KEY: $JWT_PRIVATE_KEY
          annotations:
            require-adobe-auth: false
            final: true

```

The keys defined under `inputs` are available on the `params` object provided to the App Builder action.


## JWT credentials to access token

In the App Builder action, the JWT credentials are available in the `params` object, and useable by [`@adobe/jwt-auth`](https://www.npmjs.com/package/@adobe/jwt-auth) to generate an access token, which in turn can access other Adobe APIs and services.

```javascript
const fetch = require("node-fetch");
const { Core } = require("@adobe/aio-sdk");
const { errorResponse, stringParameters, checkMissingRequestInputs } = require("../utils");
const auth = require("@adobe/jwt-auth");

async function main(params) {
  const logger = Core.Logger("main", { level: params.LOG_LEVEL || "info" });

  try {
    // Perform any necessary input error checking
    const systemErrorMessage = checkMissingRequestInputs(params, [
            "JWT_CLIENT_ID", "JWT_TECHNICAL_ACCOUNT_ID", "JWT_IMS_ORG", "JWT_CLIENT_SECRET", "JWT_METASCOPES", "JWT_PRIVATE_KEY"], []);

    // Split the metascopes into an array (they are comma delimited in the .env file)
    const metascopes = params.JWT_METASCOPES?.split(',') || [];

    // Base64 decode the private key value
    const privateKey = Buffer.from(params.JWT_PRIVATE_KEY, 'base64').toString('utf-8');

    // Exchange the JWT credentials for an 24-hour Access Token
    let { accessToken } = await auth({
      clientId: params.JWT_CLIENT_ID,                          // Client Id
      technicalAccountId: params.JWT_TECHNICAL_ACCOUNT_ID,     // Technical Account Id
      orgId: params.JWT_IMS_ORG,                               // Adobe IMS Org Id
      clientSecret: params.JWT_CLIENT_SECRET,                  // Client Secret
      metaScopes: metascopes,                                  // Metadcopes defining level of access the access token should provide
      privateKey: privateKey,                                  // Private Key to sign the JWT
    });

    // The 24-hour IMS Access Token is used to call the Analytics APIs
    // Can look at caching this token for 24 hours to reduce calls
    const accessToken = await getAccessToken(params);

    // Invoke an exmaple Adobe API endpoint using the generated accessToken
    const res = await fetch('https://analytics.adobe.io/api/example/reports', {
      headers: {
        "Accept": "application/json",
        "Content-Type": "application/json",
        "X-Proxy-Global-Company-Id": 'example',
        "Authorization": `Bearer ${accessToken}`,
        "x-Api-Key": params.JWT_CLIENT_ID,
      },
      method: "POST",
      body: JSON.stringify({... An Analytics query ... }),
    });

    if (!res.ok) { throw new Error("Request to API failed with status code " + res.status);}

    // Analytics API data
    let data = await res.json();

    const response = {
      statusCode: 200,
      body: data,
    };

    return response;
  } catch (error) {
    logger.error(error);
    return errorResponse(500, "server error", logger);
  }
}

exports.main = main;
```
