---
title: Render AEM Adaptive Forms Headlessly with Node.js
description: This code sample demonstrates a Node.js and Express application that retrieves an Adaptive Form definition from AEM Forms as JSON and dynamically renders the form using HTML and JavaScript.
solution: Experience Manager,Experience Manager Forms
type: Documentation
role: Developer
level: Beginner, Intermediate
version: Experience Manager as a Cloud Service
feature: Adaptive Forms
topic: Development
jira: KT-22838
---

# Render AEM Adaptive Forms Headlessly with Node.js

## Introduction

Adobe Experience Manager (AEM) Forms provides APIs that allow Adaptive Forms to be consumed independently of the presentation layer. This makes it possible to author and manage forms in AEM while rendering them in a custom web application.

This code sample demonstrates a **Node.js and Express application** that retrieves an Adaptive Form definition from AEM Forms as JSON and dynamically renders the form using HTML and JavaScript.

The form structure, including panels, fields, labels, and drop-down options, is authored and managed in AEM Forms. The Node.js application acts as a lightweight proxy between the browser and AEM Forms, while the browser dynamically creates the user interface from the Adaptive Form JSON definition.

## Source Code

The complete source code for this sample is available on GitHub:

[View the AEM Headless Adaptive Form sample on GitHub](https://github.com/gbedekar489/aem-headless-adaptive-form)

Clone the repository using:

```bash
git clone https://github.com/gbedekar489/aem-headless-adaptive-form.git
```

## Architecture

The sample uses the following architecture:

```text
AEM Adaptive Form
        |
        v
AEM Forms JSON API
        |
        v
Node.js / Express
        |
        v
Adaptive Form JSON
        |
        v
Custom JavaScript Renderer
        |
        v
Headless Form UI
```

The application does not hard-code the fields defined in the Adaptive Form. Instead, it traverses the form model and dynamically renders supported components.

Users can enter the URL of a published Adaptive Form directly in the application and select **Load Form** to render it.

## Project Structure

```text
aem-headless-form-demo/
├── public/
│   ├── index.html
│   ├── adaptive-form.js
│   └── styles.css
├── routes/
│   └── adaptive-form.js
├── server.js
├── package.json
└── README.md
```

## JavaScript Components

The sample separates the server-side AEM Forms integration from the client-side form rendering.

### `server.js`

The main entry point for the Node.js application.

It:

- Creates and configures the Express application.
- Serves static files from the `public` directory.
- Registers the `/api/adaptive-form` API route.
- Starts the HTTP server.

### `routes/adaptive-form.js`

The server-side integration with AEM Forms.

It:

- Receives the published Adaptive Form URL from the browser.
- Extracts the Adaptive Form repository path.
- Converts the repository path into a Base64-encoded Form ID.
- Constructs the AEM Forms API endpoint.
- Retrieves the Adaptive Form JSON definition.
- Returns the JSON to the browser.

The route acts as a lightweight proxy between the custom application and AEM Forms.

For example, the following repository path:

```text
/content/forms/af/bankingforms/registrationform
```

is converted into a Base64-encoded identifier and used to construct the API URL:

```text
https://<aem-publish-host>/adobe/forms/af/<encodedFormId>
```

### `public/adaptive-form.js`

The client-side Adaptive Form renderer.

It:

- Calls the Node.js `/api/adaptive-form` endpoint.
- Reads the `afModelDefinition` returned by AEM Forms.
- Traverses the form's `:items` and `:itemsOrder` structure.
- Detects panels and recursively renders their contents.
- Maps supported Adaptive Form field types to standard HTML controls.
- Uses properties from the AEM form model, such as labels, names, visibility, enabled state, and drop-down values.

For example, an AEM field defined as:

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

The renderer does not contain knowledge of the fields in a specific form. Adding another supported field to the Adaptive Form in AEM allows the client to discover and render it without adding field-specific code.

## Supported Components

The sample currently supports the following Adaptive Form components:

- Panels
- Text inputs
- Email inputs
- Telephone inputs
- Date inputs
- Drop-down lists

Additional Adaptive Form components can be supported by extending the `renderField()` function in `public/adaptive-form.js`.

## Finding the Adaptive Form URL

The application requires the URL of a **published AEM Adaptive Form**.

Users can provide the standard Adaptive Form URL using the following format:

```text
https://<aem-publish-host>/content/forms/af/<folder>/<form-name>
```

For example:

```text
https://publish-<program>-<environment>.adobeaemcloud.com/content/forms/af/bankingforms/registrationform
```

The Node.js application automatically extracts the Adaptive Form repository path, converts it into a Base64-encoded Form ID, and constructs the appropriate AEM Forms API endpoint.

**No manual encoding or Form ID lookup is required.**

### How the URL is processed

```text
Published Adaptive Form URL
          |
          v
Extract repository path
/content/forms/af/bankingforms/registrationform
          |
          v
Convert path to Base64
          |
          v
Construct AEM Forms API URL
/adobe/forms/af/{encodedFormId}
          |
          v
Retrieve Adaptive Form JSON
          |
          v
Render the form dynamically
```

The sample also accepts an already-encoded AEM Forms API URL using the `/adobe/forms/af/{FORM_ID}` format.

> **Note:** The Adaptive Form must be published and accessible from the AEM Publish instance.

## Running the Sample

Install the dependencies:

```bash
npm install
```

Start the Node.js application:

```bash
node server.js
```

Open the application in your browser:

```text
http://localhost:3000
```

Enter the URL of a published AEM Adaptive Form in the **AEM Adaptive Form URL** field and select **Load Form**.

The application retrieves the Adaptive Form definition from AEM Forms and dynamically renders the supported components.

## How It Works

When the user selects **Load Form**, the application performs the following operations:

1. The browser sends the published Adaptive Form URL to the Node.js application.
2. Node.js extracts the repository path and generates the encoded Form ID.
3. Node.js retrieves the Adaptive Form JSON using the AEM Forms API.
4. The browser receives the `afModelDefinition`.
5. The JavaScript renderer traverses the form model.
6. Supported Adaptive Form components are converted into standard HTML controls.

The resulting form is rendered dynamically without hard-coding the field definitions in the application.

## Extending the Renderer

Support for additional Adaptive Form field types can be added to the `renderField()` function in `public/adaptive-form.js`.

For example:

```javascript
if (field.fieldType === "radio-group") {
  // Implement rendering of radio buttons
}
```

This allows developers to control how each Adaptive Form component is represented in their custom user interface.

Unsupported field types can be logged or displayed as placeholders until the corresponding rendering logic is implemented.

## Scope and Limitations

This sample intentionally focuses on **retrieving and rendering an Adaptive Form headlessly**.

It does not attempt to implement the complete AEM Adaptive Forms runtime, including:

- Advanced rules and expressions
- Complete form validation
- Repeatable panels
- Submission actions
- All available Adaptive Form components

The sample demonstrates the separation between **form authoring and management in AEM Forms** and **form presentation in a custom application**.

It provides a lightweight foundation that can be extended to support additional components and application-specific functionality.

