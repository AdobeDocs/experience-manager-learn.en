---
title: AEM Content Fragment console extensions
description: Learn how to build and deploy AEM as a Cloud Service Content Fragment console extensions
feature: Developer Tools
version: Cloud Service
topic: Development
role: Developer
level: Beginner
recommendations: noDisplay
kt: 11603
thumbnail: KT-11603.png
last-substantial-update: 2022-12-09
---

# AEM Content Fragments Console extension

[AEM Content Fragments Console](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/content-fragments/content-fragments-console.html) extensions can be added through two extension points: a button in the [Content Fragment Console's](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/content-fragments/content-fragments-console.html) header menu or action bar. The extensions are written in JavaScript that run as App Builder apps - and can implement a custom web UI and serverless Adobe I/O Runtime actions to perform more intensive, long-running work.

![AEM Content Fragments Console extension](./assets/overview/example.png){align="center"}

| Extension type | Description | Parameter(s) |
| :--- | :--- | :--- |
| Header menu | Adds a button to the header that displays when __zero__ Content Fragments are selected. | None. |
| Action bar | Adds a button to the action bar that displays when __one or more__ Content Fragments are selected. | An array of the selected Content Fragments' paths. |

A single AEM Content Fragments Console extension can include zero or one Header menu, and zero or one Action bar extension type. If multiple extension types of the same type are required, multiple AEM Content Fragments Console extensions must be created.

AEM Content Fragments Console extensions, require an [Adobe Developer Console project](https://developer.adobe.com/uix/docs/services/aem-cf-console-admin/extension-development/#create-a-project-in-adobe-developer-console) and an [App Builder app](https://developer.adobe.com/uix/docs/services/aem-cf-console-admin/code-generation) using the `@adobe/aem-cf-admin-ui-ext-tpl` template, associated with the Adobe Developer Console project.

Select from the following capabilities when generating the App Builder app, based on what the extension does. Any combinations of options can be used in an extension.

|                                            | Add button to [Header menu](./header-menu.md) | Add button to [Action Bar](./action-bar.md) | Show [Modal](./modal.md) | Add [server-side handler](./runtime-action.md) |  
| ------------------------------------------ | :-----------------------: | :----------------------: | :--------: | :--------------------:  |
| Available when Content Fragments are not selected | ✔                         |                          |            |                         |
| Available when one or more Content Fragments are selected |                           | ✔                        |            |                         |   
| Collects custom input from user                   |                           |                          | ✔️          |                         |
| Displays custom feedback to user           |                           |                          | ✔️          |                         |
| Invokes HTTP requests to AEM                       |                           |                          |            | ✔                       |
| Invokes HTTP requests to Adobe/3rd party services  |                           |                          |            | ✔                       |


## Adobe Developer documentation

Adobe Developer contains developer details on AEM Content Fragment Console extensions. Please review the [Adobe Developer content for further technical details](https://developer.adobe.com/uix/docs/).

## Develop an extension

Follow the steps outlined below to learn how to generate, develop, and deploy an AEM Content Fragment Console extension for AEM as a Cloud Service.

<div class="columns is-multiline">
    <!-- Create Adobe Developer Project -->
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Create Adobe Developer Project">
        <div class="card">
            <div class="card-image">
                <figure class="image is-16by9">
                    <a href="./adobe-developer-console-project.md" title="Create Adobe Developer Project" tabindex="-1">
                        <img class="is-bordered-r-small" src="./assets/project/card.png" alt="Create Adobe Developer Project">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small">
                <div class="content">
                    <p class="headline is-size-5 has-text-weight-bold">1. Create a project</p>
                    <p class="is-size-6">Create an Adobe Developer Console project that defines it's access to other Adobe services, and manages its deployments.</p>
                    <a href="./adobe-developer-console-project.md" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM">
                        <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Create an Adobe Developer Project</span>
                    </a>
                </div>
            </div>
        </div>
    </div>
    <!-- Generate an Extension app -->
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Generate an Extension app">
        <div class="card">
            <div class="card-image">
                <figure class="image is-16by9">
                    <a href="./app-initialization.md" title="Generate an Extension app" tabindex="-1">
                        <img class="is-bordered-r-small" src="./assets/initialize-app/card.png" alt="Initialize an extension app">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small">
                <div class="content">
                    <p class="headline is-size-5 has-text-weight-bold">2. Initialize an extension app</p>
                    <p class="is-size-6">Initialize an AEM Content Fragment Console extension App Builder app that defines where the extension appears, and the work it performs.</p>
                    <a href="./app-initialization.md" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM">
                        <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Initialize an extension app</span>
                    </a>
                </div>
            </div>
        </div>
    </div>
    <!-- Extension registration -->
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Extension registration">
        <div class="card">
            <div class="card-image">
                <figure class="image is-16by9">
                    <a href="./extension-registration.md" title="Extension registration" tabindex="-1">
                        <img class="is-bordered-r-small" src="./assets/extension-registration/card.png" alt="Extension registration">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small">
                <div class="content">
                    <p class="headline is-size-5 has-text-weight-bold">3. Extension registration</p>
                    <p class="is-size-6">Register the extension in the AEM Content Fragment Console as a header menu or action bar extension type.</p>
                    <a href="./extension-registration.md" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM">
                        <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Register the extension</span>
                    </a>
                </div>
            </div>
        </div>
    </div>
    <!-- Header Menu -->
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Header menu">
        <div class="card">
            <div class="card-image">
                <figure class="image is-16by9">
                    <a href="./header-menu.md" title="Header menu" tabindex="-1">
                        <img class="is-bordered-r-small" src="./assets/header-menu/card.png" alt="Header menu">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small">
                <div class="content">
                    <p class="headline is-size-5 has-text-weight-bold">4a. Header Menu</p>
                    <p class="is-size-6">Learn how to create an AEM Content Fragment Console header menu extension.</p>
                    <a href="./header-menu.md" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM">
                        <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Extend the header menu</span>
                    </a>
                </div>
            </div>
        </div>
    </div>
    <!-- Action Bar -->
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Action Bar">
        <div class="card">
            <div class="card-image">
                <figure class="image is-16by9">
                    <a href="./action-bar.md" title="Action Bar" tabindex="-1">
                        <img class="is-bordered-r-small" src="./assets/action-bar/card.png" alt="Action Bar">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small">
                <div class="content">
                    <p class="headline is-size-5 has-text-weight-bold">4b. Action Bar</p>
                    <p class="is-size-6">Learn how to create an AEM Content Fragment Console action bar extension.</p>
                    <a href="./action-bar.md" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM">
                        <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Extend the action bar</span>
                    </a>
                </div>
            </div>
        </div>
    </div>
    <!-- Modal -->
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Modal">
        <div class="card">
            <div class="card-image">
                <figure class="image is-16by9">
                    <a href="./modal.md" title="Modal" tabindex="-1">
                        <img class="is-bordered-r-small" src="./assets/modal/card.png" alt="Modal">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small">
                <div class="content">
                    <p class="headline is-size-5 has-text-weight-bold">5. Modal</p>
                    <p class="is-size-6">Add a custom modal to the extension that can be used to create bespoke experiences for users. Modals often collect input from users, and display the results of an operation.</p>
                    <a href="./modal.md" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM">
                        <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Add a modal</span>
                    </a>
                </div>
            </div>
        </div>
    </div>
    <!-- Adobe I/O Runtime action -->
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Adobe I/O Runtime action">
        <div class="card">
            <div class="card-image">
                <figure class="image is-16by9">
                    <a href="./runtime-action.md" title="Adobe I/O Runtime action" tabindex="-1">
                        <img class="is-bordered-r-small" src="./assets/runtime-action/card.png" alt="Adobe I/O Runtime action">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small">
                <div class="content">
                    <p class="headline is-size-5 has-text-weight-bold">6. Adobe I/O Runtime action</p>
                    <p class="is-size-6">Add a serverless Adobe I/O Runtime action that the extension can invoke to interact with Content Fragments and AEM to perform custom business operations.</p>
                    <a href="./runtime-action.md" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM">
                        <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Add an Adobe I/O Runtime action</span>
                    </a>
                </div>
            </div>
        </div>
    </div>
    <!-- Test -->
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Test">
        <div class="card">
            <div class="card-image">
                <figure class="image is-16by9">
                    <a href="./test.md" title="Test" tabindex="-1">
                        <img class="is-bordered-r-small" src="./assets/test/card.png" alt="Test">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small">
                <div class="content">
                    <p class="headline is-size-5 has-text-weight-bold">7. Test</p>
                    <p class="is-size-6">Test the extensions during development, and sharing completed extensions to  QA or UAT testers using a special URL.</p>
                    <a href="./test.md" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM">
                        <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Test the extension</span>
                    </a>
                </div>
            </div>
        </div>
    </div>
    <!-- Extension deployment -->
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Extension deployment">
        <div class="card">
            <div class="card-image">
                <figure class="image is-16by9">
                    <a href="./deploy.md" title="Extension deployment" tabindex="-1">
                        <img class="is-bordered-r-small" src="./assets/deploy/card.png" alt="Extension deployment">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small">
                <div class="content">
                    <p class="headline is-size-5 has-text-weight-bold">8. Production deployment</p>
                    <p class="is-size-6">Deploy the extension to Adobe I/O making it available to AEM users. Extensions can be updated, and removed as well.</p>
                    <a href="./deploy.md" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM">
                        <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Deploy to production</span>
                    </a>
                </div>
            </div>
        </div>
    </div>
</div>

## Example extensions

Example AEM Content Fragment Console extensions.

<div class="columns is-multiline">
    <!-- Bulk property update extension -->
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Bulk property update extension">
        <div class="card">
            <div class="card-image">
                <figure class="image is-16by9">
                    <a href="./example-extensions/bulk-property-update.md" title="Bulk property update extension" tabindex="-1">
                        <img class="is-bordered-r-small" src="./example-extensions/assets/bulk-property-update/card.png" alt="Bulk property update extension">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small">
                <div class="content">
                    <p class="headline is-size-5 has-text-weight-bold">Bulk property update extension</p>
                    <p class="is-size-6">Explore an example action bar extension that bulk updates a property on selected Content Fragments.</p>
                    <a href="./example-extensions/bulk-property-update.md" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM">
                        <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Explore the example extension</span>
                    </a>
                </div>
            </div>
        </div>
    </div>
    <!-- Image Generartion update extension -->
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="OpenAI-based image generation and upload to AEM extension">
        <div class="card">
            <div class="card-image">
                <figure class="image is-16by9">
                    <a href="./example-extensions/image-generation-and-image-upload.md" title="OpenAI-based image generation and upload to AEM extension" tabindex="-1">
                        <img class="is-bordered-r-small" src="./example-extensions/assets/digital-image-generation/screenshot.png" alt="OpenAI-based image generation and upload to AEM extension">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small">
                <div class="content">
                    <p class="headline is-size-5 has-text-weight-bold">OpenAI-based image generation and upload to AEM extension</p>
                    <p class="is-size-6">Explore an example action bar extension that generates an image using OpenAI, uploads it to AEM and updates image property on the selected Content Fragment.</p>
                    <a href="./example-extensions/image-generation-and-image-upload.md" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM">
                        <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Explore the example extension</span>
                    </a>
                </div>
            </div>
        </div>
    </div>    

    

</div>
