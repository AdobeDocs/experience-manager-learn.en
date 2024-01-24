---
title: Install the required adaptive form react libraries
description: Add the required dependencies to your react project
feature: Adaptive Forms
version: 6.5
jira: KT-13285
topic: Development
role: User
level: Intermediate
exl-id: 0ed44016-d52a-4980-a0b1-06da149c3cb1
duration: 54
---
# Installing the required dependencies

To start using headless adaptive forms in your react project, install the following dependencies in your react project

* @aemforms/af-react-components
* @aemforms/af-react-renderer

Update the package.json to include the following dependencies. At the time of writing 0.22.41 was the current version

```json
"@aemforms/af-react-components": "^0.22.41",
"@aemforms/af-react-renderer": "^0.22.41",

```

>[!NOTE]
>
>The drop-down list and the card layout in this tutorial were created using [Material UI library](https://mui.com/). You will need to download the appropriate Material UI packages to get the code working on your system.

## Setup Proxy

Cross-Origin Resource Sharing (CORS) is a security mechanism that restricts web browsers from making requests to a different domain than the one the app is hosted on. CORS errors can occur when you try to fetch data from an API hosted on a different domain. By setting up a proxy, you can bypass CORS restrictions and make requests to the API from your React app. I have used the following code in a file called setUpProxy.js in the src folder. **Make sure you change the target to point to your publish instance.**

```
const { createProxyMiddleware } = require('http-proxy-middleware');
const proxy = {
    target: 'https://mypublishinstance:4503/',
    changeOrigin: true
}
module.exports = function(app) {
  app.use(
    '/adobe',
    createProxyMiddleware(proxy)
  ),
  app.use(
    '/content',
    createProxyMiddleware(proxy)
  );
};
```

You will also need to install and add the **http-proxy-middleware** module to your project.

## Next Steps

[Fetch the form to embed](./fetch-the-form.md)
