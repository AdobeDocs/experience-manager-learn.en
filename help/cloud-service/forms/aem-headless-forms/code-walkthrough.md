---
title: Render AEM Adaptive Forms Headlessly Using Node.js
description: Adobe Experience Manager (AEM) Forms provides APIs that allow Adaptive Forms to be consumed independently of the presentation layer. This makes it possible to author and manage forms in AEM while rendering them in a custom web application
solution: Experience Manager,Experience Manager Forms
type: Documentation
role: Developer
level: Beginner, Intermediate
version: Experience Manager as a Cloud Service
feature: Adaptive Forms
topic: Development
jira: KT-22838
---
## JavaScript Components

The sample separates the server-side AEM Forms integration from the client-side form rendering.

### `server.js`

The main entry point for the Node.js application.

It:

- Creates and configures the Express application.
- Serves static files from the `public` directory.
- Registers the `/api/adaptive-form` API route.
- Starts the HTTP server.

`server.js` does not contain AEM-specific form rendering logic. It primarily connects the server-side route with the browser application.



### `routes/adaptive-form.js`

The server-side integration with AEM Forms.

It:

- Receives requests from the browser at `/api/adaptive-form`.
- Reads the Adaptive Form URL from the `AEM_FORM_URL` environment variable.
- Calls the AEM Forms endpoint to retrieve the Adaptive Form definition.
- Returns the Adaptive Form JSON to the browser.

This route acts as a lightweight proxy between the custom application and AEM Forms.

```text
Browser
   |
   | GET /api/adaptive-form
   v
Node.js
   |
   | GET /adobe/forms/af/{FORM_ID}
   v
AEM Forms
```

Keeping this communication on the server also provides a natural place to add authentication, logging, caching, or other integration logic if required.



### `public/adaptive-form.js`

The client-side Adaptive Form renderer.

It:

- Calls the Node.js `/api/adaptive-form` endpoint.
- Reads the `afModelDefinition` returned by AEM Forms.
- Traverses the form's `:items` and `:itemsOrder` structure.
- Detects panels and recursively renders their contents.
- Maps supported Adaptive Form field types to standard HTML controls.
- Uses properties from the AEM form model such as labels, names, visibility, enabled state, and drop-down values.

For example, an AEM field such as:

```json
{
  "fieldType": "email",
  "name": "email",
  "label": {
    "value": "Your Email Address"
  }
}
```

is dynamically rendered as an HTML email input.

The renderer currently supports:

- Panels
- Text inputs
- Email inputs
- Telephone inputs
- Date inputs
- Drop-down lists

The renderer does not contain knowledge of the specific fields in the Adaptive Form. Adding another supported field to the form in AEM allows the client to discover and render it without adding field-specific code.



### Application Flow

The responsibilities of the JavaScript files can be summarized as:

```text
server.js
   |
   +-- Application and Express configuration
   |
   v
routes/adaptive-form.js
   |
   +-- Retrieves the Adaptive Form definition from AEM
   |
   v
public/adaptive-form.js
   |
   +-- Converts the Adaptive Form JSON into HTML controls
   |
   v
Headless Form UI
```