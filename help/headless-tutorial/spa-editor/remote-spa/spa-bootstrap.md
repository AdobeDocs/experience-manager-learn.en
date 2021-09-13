---
title: Bootstrap the Remote SPA for SPA Editor
description: Learn how to bootstrap a remote SPA for AEM SPA Editor compatibility.
topic: Headless, SPA, Development
feature: SPA Editor, Core Components, APIs, Developing
role: Developer, Architect
level: Beginner
kt: 7633
thumbnail: kt-7633.jpeg
exl-id: b8d43e44-014c-4142-b89c-ff4824b89c78
---
# Bootstrap the Remote SPA for SPA Editor

Before the editable areas can be added to the Remote SPA, it must be bootstrapped with the AEM SPA Editor JavaScript SDK, and a few other configurations.


## Download the WKND App source

If you have no already done so, download the WKND App's source code from Github.com, and switch the branch containing the changes to the SPA performed in this tutorial.

```
$ mkdir -p ~/Code/wknd-app
$ cd ~/Code/wknd-app
$ git clone --branch feature/spa-editor https://github.com/adobe/aem-guides-wknd-graphql.git
$ cd aem-guides-wknd-graphql
```

## Add AEM SPA Editor JS SDK npm dependencies

First, add AEM's SPA npm dependencies to the React project.

```
$ cd ~/Code/wknd-app/aem-guides-wknd-graphql/react-app
$ npm install --save \
    @adobe/aem-spa-page-model-manager \
    @adobe/aem-spa-component-mapping \
    @adobe/aem-react-editable-components \
    @adobe/aem-core-components-react-base \
    @adobe/aem-core-components-react-spa
```

+ `@adobe/aem-spa-page-model-manager` provides the API for retrieving content from AEM.
+ `@adobe/aem-spa-component-mapping` provides the API that mapping AEM content to SPA components.
+ ` @adobe/aem-react-editable-components` provides an API for building custom SPA components and provides common-use implementations such as the `AEMPage` React component.
+ `@adobe/aem-core-components-react-base` provides a suite of ready-to-use React components that seamlessly integrate with the AEM 
WCM Core Components and are SPA Editor agnostic. These primarily include content components such as:
  + Title
  + Text
  + Breadcrumbs
  + And so on.
+ `@adobe/aem-core-components-react-spa` provides a suite of ready-to-use React components that seamlessly integrate with the AEM WCM Core Components and but require SPA Editor. These primarily contain components that contain content components from `@adobe/aem-core-components-react-base`, such as:
  + Container
  + Carousel
  + and so forth.

## Review SPA environment variables

Several environment variables must be exposed to the Remote SPA so it knows how to interact with AEM.

1. Open Remote SPA project at `~/Code/wknd-app/aem-guides-wknd-graphql/react-app` in your IDE
1. Open the file `.env.development` 
1. Add the file, paying specific attention to the keys:

    ```
    REACT_APP_HOST_URI=http://localhost:4502
    REACT_APP_AUTHORIZATION=admin:admin
    ```

    ![Remote SPA Environment Variables](./assets/spa-bootstrap/env-variables.png)
    
    *Remember that custom environment variables in React must be prefixed with `REACT_APP_`.*

    + `REACT_APP_AEM_URI`: the scheme and host of the AEM service the Remote SPA connects to.
        + This value change based on if the AEM environment (local, Dev, Stage, or Production), and the AEM Service type (Author vs. Publish)
    + `REACT_APP_AEM_AUTH`: the credentials used by the SPA authenticate to AEM and retrieve content.
        + Required for use with AEM Author
        + Possibly required for use with AEM Publish (if content is protected)
        + Developing against the AEM SDK supports local accounts via Basic Auth. This is the method used in this tutorial.
        + When integrating with AEM as a Cloud Service, use [access tokens](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/overview.html)

## Integrate the ModelManager API

With the AEM SPA npm dependencies available to the app, initialize AEM's `ModelManager` in the project's `index.js` before `ReactDOM.render(...)` is invoked.

The [ModelManager](https://www.npmjs.com/package/@adobe/aem-spa-page-model-manager) is responsible for connecting to AEM to retrieving editable content.

1. Open the Remote SPA project in your IDE
1. Open the file `src/index.js`
1. Add import `ModelManager` and initialize it before the `ReactDOM.render(..)` invocation,

    ```
    ...
    import { ModelManager } from "@adobe/aem-spa-page-model-manager";

    // Initialize the ModelManager before invoking ReactDOM.render(...).
    ModelManager.initializeAsync();

    ReactDOM.render(...);
    ```

The `src/index.js` file should look like:

![src/index.js](./assets/spa-bootstrap/index-js.png)

## Set up an internal SPA proxy

When sourcing editable content from AEM in the SPA, it is best to setup an [internal proxy in the SPA](https://create-react-app.dev/docs/proxying-api-requests-in-development/#configuring-the-proxy-manually), that is configured to route the appropriate requests to AEM. This is done by using [http-proxy-middleware](https://www.npmjs.com/package/http-proxy-middleware) npm module, which is already installed by the base WKND GraphQL App.

1. Open the Remote SPA project in your IDE
1. Create a file at `src/proxy/setupProxy.spa-editor.auth.basic.js`
1. Add the following code to the file:

    ```
    const { createProxyMiddleware } = require('http-proxy-middleware');
    const {REACT_APP_HOST_URI, REACT_APP_AUTHORIZATION } = process.env;

    /*
        Set up a proxy with AEM for local development
        In a production environment this proxy should be set up at the webserver level or absolute URLs should be used.
    */
    module.exports = function(app) {

        /**
        * Filter to check if the request should be re-routed to AEM. The paths to be re-routed at:
        * - Starts with /content (AEM content)
        * - Starts with /graphql (AEM graphQL endpoint)
        * - Ends with .model.json (AEM Content Services)
        * 
        * @param {*} path the path being requested of the SPA
        * @param {*} req the request object
        * @returns true if the SPA request should be re-routed to AEM
        */
        const toAEM = function(path, req) {
            return path.startsWith('/content') || 
                path.startsWith('/graphq') ||
                path.endsWith('.model.json')
        }

        /**
        * Re-writes URLs being proxied to AEM such that they can resolve to real AEM resources
        * - The "root" case of `/.model.json` are rewritten to the SPA's home page in AEM
        * - .model.json requests for /adventure:xxx routes are rewritten to their corresponding adventure page under /content/wknd-app/us/en/home/adventure/ 
        * 
        * @param {*} path the path being requested of the SPA
        * @param {*} req the request object
        * @returns returns a re-written path, or nothing to use the @param path
        */
        const pathRewriteToAEM = function (path, req) { 
            if (path === '/.model.json') {
                return '/content/wknd-app/us/en/home.model.json';
            } else if (path.startsWith('/adventure:') && path.endsWith('.model.json')) {
                return '/content/wknd-app/us/en/home/adventure/' + path.split('/').pop();
            }    
        }
    
        /**
        * Register the proxy middleware using the toAEM filter and pathRewriteToAEM rewriter 
        */
        app.use(
            createProxyMiddleware(
                toAEM, // Only route the configured requests to AEM
                {
                    target: REACT_APP_HOST_URI,
                    changeOrigin: true,
                    // Pass in credentials when developing against an Author environment
                    auth: REACT_APP_AUTHORIZATION,
                    pathRewrite: pathRewriteToAEM // Rewrite SPA paths being sent to AEM
                }
            )
        );
    
        /**
        * Enable CORS on requests from the SPA to AEM
        * 
        * If this rule is not in place, CORS errors will occur when running the SPA on http://localhost:3000
        */
        app.use((req, res, next) => {
            res.header("Access-Control-Allow-Origin", REACT_APP_HOST_URI);
            next();
        });
    };
    ```    

    The `setupProxy.spa-editor.auth.basic.js` file should look like:

    ![src/proxy/setupProxy.spa-editor.auth.basic.js](./assets/spa-bootstrap/setup-proxy-spaeditor-js.png)

    This proxy configuration does two main things:

    1. Proxies-specific requests made to the SPA, `http://localhost:3000` to AEM `http://localhost:4502`
        + It only proxies requests whose paths match patterns that indicate they should be served by AEM, as defined in `toAEM(path, req)`.
        + It rewrites SPA paths to their counterpart AEM pages, as defined in `pathRewriteToAEM(path, req)`
    1. It adds CORS headers to all requests to allow access to AEM content, as defined by `res.header("Access-Control-Allow-Origin", REACT_APP_HOST_URI);` 
        + If this is not added, CORS errors occur when loading AEM content in the SPA.
    
1. Open the file `src/setupProxy.js`
1. Comment out the line `const proxy = require('./proxy/setupProxy.auth.basic')`
1. Add a line, pointing to the new proxy configuration file:

    ```
    // Proxy configuration for SPA Editor (and GraphQL) using Basic Auth
    const proxy = require('./proxy/setupProxy.spa-editor.auth.basic')
    ```

    The `setupProxy.js` file should look like:

    ![src/setupProxy.js](./assets/spa-bootstrap/setup-proxy-js.png)

Note, any changes to the `src/setupProxy.js` or it's referenced files require a restart of the SPA.

## Static SPA resource

Static SPA resources such as the WKND Logo and Loading graphics need to have their src URLs updated to force them load from the Remote SPA's host. If left relative, when the SPA is loaded in SPA Editor for authoring, these URLs default to use AEM's host rather than the SPA, resulting in 404 requests as illustrated in the image below.

![Broken static resources](./assets/spa-bootstrap/broken-static-resource.png)

To resolve this issue, make a static resource hosted by the Remote SPA use absolute paths that include the Remote SPA's origin.

1. Open the SPA project in your IDE
1. Open your SPA's environment variables file `src/.env.development` and add a variable for the SPA's public URI:

    ```
    ...
    # The base URI the SPA is accessed from
    REACT_APP_PUBLIC_URI=http://localhost:3000
    ```

    _When deploying to AEM as a Cloud Service, you need to the same for the corresponding `.env` files._

1. Open the file `src/App.js`
1. Import the SPA's public URI from the SPA's environment variables

    ```
    const {  REACT_APP_PUBLIC_URI } = process.env;

    function App() { ... }
    ```

1. Prefix the WKND logo `<img src=.../>` with `REACT_APP_PUBLIC_URI` to force resolution against the SPA.

    ```
    <img src={REACT_APP_PUBLIC_URI + '/' +  logo} className="logo" alt="WKND Logo"/>
    ```

1. Do the same for loading image in `src/components/Loading.js`

    ```
    const { REACT_APP_PUBLIC_URI } = process.env;

    class Loading extends Component {

        render() {
            return (<div className="loading">
                <img src={REACT_APP_PUBLIC_URI + '/' + loadingIcon} alt="Loading..." />
            </div>);
        }
    }
    ```

1. .. and for the __two instances__ of the back button in `src/components/AdventureDetails.js`

    ```
    const { REACT_APP_PUBLIC_URI } = process.env;

    function AdventureDetail(props) {
        ...
        render() {
            <img className="Backbutton-icon" src={REACT_APP_PUBLIC_URI + '/' + backIcon} alt="Return" />
        }
    }
    ```

The `App.js`, `Loading.js`, and `AdventureDetails.js` files should look like:

![Static resources](./assets/spa-bootstrap/static-resources.png)

## AEM Responsive Grid

To support SPA Editor's layout mode for editable areas in the SPA, we must integrate AEM's Responsive Grid CSS into the SPA. Don't worry - this grid system will only to the editable containers, and you can use your grid system of choice to drive the layout of the rest of your SPA.

Add the AEM Responsive Grid SCSS files to the SPA.

1. Open the SPA project in your IDE
1. Download and copy the following two files into `src/styles`
    + [_grid.scss](./assets/spa-bootstrap/_grid.scss)
        + The AEM Responsive Grid SCSS generator
    + [_grid-init.scss](./assets/spa-bootstrap/_grid-init.scss)
        + Invokes `_grid.scss` using the SPA's specific breakpoints (desktop and mobile) and columns (12).
1. Open `src/App.scss` and import `./styles/grid-init.scss`

    ```
    ...
    @import './styles/grid-init';
    ...
    ```

The `_grid.scss` and `_grid-init.scss` files should look like:

![AEM Responsive Grid SCSS](./assets/spa-bootstrap/aem-responsive-grid.png)

Now the SPA includes the CSS required to support AEM's Layout Mode for components added to an AEM container.

## Start the SPA

Now that the SPA is bootstrapped for integration with AEM, let's run the SPA and see what it looks like!

1. On the command line, navigate to the root of the SPA project
1. Start the SPA using the normal commands (run `npm install` if you have not already)

    ```
    $ cd ~/Code/wknd-app/aem-guides-wknd-graphql/react-app
    $ npm install 
    $ npm run start
    ```

1. Browse the SPA on [http://localhost:3000](http://localhost:3000). Everything should look good!

![SPA running on http://localhost:3000](./assets/spa-bootstrap/localhost-3000.png)

## Open the SPA in AEM SPA Editor

With the SPA running on [http://localhost:3000](http://localhost:3000), let's open it using AEM SPA Editor. Nothing is editable in the SPA yet, this only validates the SPA in AEM.

1. Log in to AEM Author
1. Navigate to __Sites > WKND App > us > en__
1. Select the __WKND App Home Page__ and tap __Edit__, and the SPA will appear.

    ![Edit WKND App Home Page](./assets/spa-bootstrap/edit-home.png)

1. Switch to __Preview__ using the mode switcher in the top right
1. Click around the SPA

    ![SPA running on http://localhost:3000](./assets/spa-bootstrap/spa-editor.png)

## Congratulations!

You've bootstrapped the Remote SPA to be AEM SPA Editor compatible! You now know how to:

+ Add the AEM SPA Editor JS SDK npm dependencies to the SPA project
+ Configure your SPA's environment variables
+ Integrate the ModelManager API with the SPA
+ Setup an internal proxy for the SPA so it routes the appropriate content requests to AEM
+ Address issues with static SPA resources resolving in the context of SPA Editor
+ Add AEM's Responsive Grid CSS to support layout-ing in AEM's editable containers

## Next Steps

Now that we've achieved a baseline of compatibility with AEM SPA Editor, we can start introducing editable areas. We'll first look at how to place a [fixed editable component](./spa-fixed-component.md) in the SPA.
