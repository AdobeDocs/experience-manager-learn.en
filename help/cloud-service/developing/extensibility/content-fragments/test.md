---
title: Testing a AEM Content Fragment console extension
description: Learn how to test an AEM Content Fragment console extension before deploying to production.
feature: Developer Tools
version: Cloud Service
topic: Development
role: Developer
level: Beginner
recommendations: noDisplay, noCatalog
kt: 11603
last-substantial-update: 2022-12-01
---

# Test an extension

AEM Content Fragment Console extensions can be tested against any AEM as a Cloud Service environment in the Adobe Org the extension belongs to.

Testing an extension is done through a specially crafted URL that instructs the AEM Content Fragment console to load the extension. 

## AEM Content Fragment Console URL

![AEM Content Fragment Console URL](./assets/test/content-fragment-console-url.png){align="center"}

To create a URL that mounts the non-Production extension into an AEM Content Fragment Console, the URL of the desired AEM Content Fragment Console must be collected. Navigate to the AEM as a Cloud Service environment to test the extension on, and copy the URL of it's AEM Content Fragment Console.

1. Log in to the desired AEM as a Cloud Service env.
  
    + Use an AEM Development environment for [testing development builds](#testing-development-builds)
    + Use the AEM Stage or QA Development environment for [testing stage builds](#testing-stage-builds)

1. Select the __Content Fragments__ icon.
1. Wait for the AEM Content Fragment Console to load in the browser.
1. Copy the AEM Content Fragment Console's URL from the browser's address bar, it should resemble:

    ```
    https://experience.adobe.com/?repo=author-p1234-e5678.adobeaemcloud.com#/@wknd/aem/cf/admin
    ```

This URL is used below when crafting the URLs for development and stage testing.

## Test local development builds

1. Open a command line to the root of the extension project.
1. Run the AEM Content Fragment Console extension as a local App Builder app

    ```shell
    $ aio app run
    ...
    No change to package.json was detected. No package manager install will be executed.

    To view your local application:
      -> https://localhost:9080
    To view your deployed application in the Experience Cloud shell:
      -> https://experience.adobe.com/?devMode=true#/custom-apps/?localDevUrl=https://localhost:9080
    ```

  Take note of the local application URL, shown above as `-> https://localhost:9080`

1. Add the following two query params to the [AEM Content Fragment Console's URL](#aem-content-fragment-console-url)
    + `&devMode=true`
    + `&ext=<LOCAL APPLICATION URL>`, usually `&ext=https://localhost:9080`.

    Add the two above query parameters (`devMode` and `ext`) as the __first__ query parameters in the URL, as the Content Fragment Console uses a hash route (`#/@wknd/aem/...`), so incorrectly post-fixing the parameters after the `#` will not work.
    
    The test URL should look like:

      ```
      https://experience.adobe.com/?devMode=true&ext=https://localhost:9080&repo=author-p1234-e5678.adobeaemcloud.com#/@wknd/aem/cf/admin
      ```

1. Copy and paste the test URL into your browser.
  
    + You may have to initially, and then periodically, you must [accept the HTTPS certificate](https://developer.adobe.com/uix/docs/services/aem-cf-console-admin/extension-development/#accepting-the-certificate-first-time-users) for the local application's host (`https://localhost:9080`).

1. The AEM Content Fragment Console loads with the local version of the extension injected into it for testing, and hot-reload changes for as long as the local App Builder app is running.

>[!IMPORTANT]
>
>Remember, when using this approach, the extension under development only impacts your experience, and all other users of the AEM Content Fragment console access it without the injected extension. 


## Test stage builds

1. Open a command line to the root of the extension project.
1. Ensure that the Stage workspace is active (or whatever Workspace is used for testing).
    ```shell
    $ aio app use -w Stage
    ```
    Merge any changes to `.env` and `.aio`.
1. Deploy the updated extension App Builder app. If not logged in, run `aio login` first.
    ```shell
    $ aio app deploy
    ...
    Your deployed actions:
    web actions:
      -> https://98765-123aquarat.adobeio-static.net/api/v1/web/aem-cf-console-admin-1/generic 
    To view your deployed application:
      -> https://98765-123aquarat.adobeio-static.net/index.html
    To view your deployed application in the Experience Cloud shell:
      -> https://experience.adobe.com/?devMode=true#/custom-apps/?localDevUrl=https://98765-123aquarat.adobeio-static.net/index.html
    New Extension Point(s) in Workspace 'Production': 'aem/cf-console-admin/1'
    Successful deployment 🏄
    ```

1. Add the following two query params to the [AEM Content Fragment Console's URL](#aem-content-fragment-console-url)
    + `&devMode=true`
    + `&ext=<DEPLOYED APPLICATION URL>`

    Add the two above query parameters (`devMode` and `ext`) as the __first__ query parameters in the URL, as the Content Fragment Console uses a hash route (`#/@wknd/aem/...`), so incorrectly post-fixing the parameters after the `#` will not work.

    The test URL should look like:

    ```
    https://experience.adobe.com/?devMode=true&ext=https://98765-123aquarat.adobeio-static.net/index.html&repo=author-p1234-e5678.adobeaemcloud.com#/@wknd/aem/cf/admin
    ```

1. Copy and paste the test URL into your browser.
1. The AEM Content Fragment Console injects the version of the extension deployed to Stage workspace in. This Stage URL can be shared to QA or business users for testing.

  Remember, when using this approach, the Staged extension is only injected on AEM Content Fragment Console's when access with the craft Stage URL. 

1. Deployed extensions can be updated by running `aio app deploy` again, and these changes automatically reflect when using the test URL.
1. To remove an extension for testing, run `aio app undeploy`.



