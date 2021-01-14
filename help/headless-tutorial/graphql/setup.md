---
title: Quick Setup - Getting Started with AEM Headless - GraphQL
description: Get started with Adobe Experience Manager (AEM) and GraphQL. Install the AEM SDK, add sample content and deploy an application that consumes content from AEM using its GraphQL APIs. See how AEM powers omni-channel experiences.
sub-product: sites
topics: headless
version: cloud-service
doc-type: tutorial
activity: develop
audience: developer
mini-toc-levels: 1
kt: 6386
thumbnail: KT-6386.jpg
---

# Quick Setup {#setup}

>[!CAUTION]
>
> The AEM GraphQL API for Content Fragments Delivery is available on request.
> Please reach out to Adobe Support to enable the API for your AEM as a Cloud Service program.

This chapter offers a quick setup of a local environment to see an external application consume content from AEM using AEM's GraphQL APIs. Later chapters in the tutorial will build off of this setup.

## Prerequisites {#prerequisites}

The following tools should be installed locally:

* [JDK 11](https://experience.adobe.com/#/downloads/content/software-distribution/en/general.html?1_group.propertyvalues.property=.%2Fjcr%3Acontent%2Fmetadata%2Fdc%3AsoftwareType&1_group.propertyvalues.operation=equals&1_group.propertyvalues.0_values=software-type%3Atooling&fulltext=Oracle%7E+JDK%7E+11%7E&orderby=%40jcr%3Acontent%2Fjcr%3AlastModified&orderby.sort=desc&layout=list&p.offset=0&p.limit=14)
* [Node.js v10+](https://nodejs.org/en/)
* [npm 6+](https://www.npmjs.com/)
* [Git](https://git-scm.com/)

## Objectives {#objectives}

1. Download and install the AEM SDK.
1. Download and install sample content from the WKND Reference site.
1. Download and install a sample app to consume content using the GraphQL APIs.

## Install the AEM SDK{#aem-sdk}

This tutorial uses the [AEM as a Cloud Service SDK](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=en#aem-as-a-cloud-service-sdk) to explore AEM's GraphQL APIs. This section provides a quick guide to installing the AEM SDK and running it in Author mode. A more detailed guide for setting up a local development environment [can be found here](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html?lang=en#local-development-environment-set-up). 

>[!NOTE]
>
> It is also possible to follow the tutorial with an AEM as a Cloud Service environment. Additional notes for using a Cloud environment are included throughout the tutorial.

1. Navigate to the **[Software Distribution Portal](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)** > **AEM as a Cloud Service** and download the latest version of the **AEM SDK**.

    ![Software Distribution Portal](assets/setup/software-distribution-portal-download.png)

1. Unzip the download and copy the Quickstart jar (`aem-sdk-quickstart-XXX.jar`) to a dedicated folder, i.e `~/aem-sdk/author`.
1. Re-name the jar file to `aem-author-p4502.jar`.
1. Open a new terminal window and navigate to the folder that contains the jar file. Run the following command to install and start the AEM instance:

    ```shell
    $ cd ~/aem-sdk/author
    $ java -jar aem-author-p4502.jar
    ```

1. Provide an admin password as `admin`. Any admin password is acceptable, however its recommend to use the default for local development to reduce the need to re-configure.
1. After a few minutes the AEM instance will finish installing and a new browser window should open at [http://localhost:4502](http://localhost:4502). 
1. Login with the username `admin` and password `admin`.

>[!CAUTION]
>
> To continue the setup, the GraphQL Feature must now be manually enabled on the Quickstart SDK. Reach out to your Adobe contact for further instructions. This manual step is only needed until the feature is released in 2021.

## Install sample content{#wknd-site}

Sample content from the WKND Reference site will be installed to accelerate the tutorial. The WKND is a fictitious life-style brand, often used in conjunction with AEM training. 

1. Download the latest compiled AEM Package for WKND Site: [aem-guides-wknd.all-x.x.x.zip](https://github.com/adobe/aem-guides-wknd/releases/latest). 

    >[!NOTE]
    >
    > Make sure to download the standard version compatible with AEM as a Cloud Service and **not** the `classic` version.

1. From the **AEM Start** menu navigate to **Tools** > **Deployment** > **Packages**.

    ![Navigate to Packages](assets/setup/navigate-to-packages.png)

1. Click **Upload Package** and choose the WKND package downloaded in the prior step. Click **Install** to install the package.

1. From the **AEM Start** menu navigate to **Assets** > **Files**.
1. Click through the folders to navigate to **WKND Site** > **English** > **Adventures**.

    ![Folder view of Adventures](assets/setup/folder-view-adventures.png)

    This is a folder of all the assets that comprise the various Adventures promoted by the WKND brand. This includes traditional media types like images and video, as well as media specific to AEM like **Content Fragments**.

1. Click into the **Downhill Skiing Wyoming** folder and click the **Downhill Skiing Wyoming Content Fragment** card:

    ![Downwhill Skiing Content fragment Card](assets/setup/downhill-skiing-cntent-fragment.png)

1. The Content Fragment Editor UI will open for the Downhill Skiing Wyoming adventure.

    ![Downhill Skiing Content Fragment](assets/setup/down-hillskiing-fragment.png)

    Observe that various fields like **Title**, **Description**, and **Activity** define the fragment.

    **Content Fragments** are one of the ways content can be managed in AEM. Content Fragment are reusable, presentation-agnostic content composed of structured data elements such as text, rich text, dates or references to other Content Fragments. Content Fragments will be explored in greater detail later in the tutorial.

1. Click **Cancel** to close the fragment. Feel free to navigate into some of the other folders and explore the other Adventure content.

>[!NOTE]
>
> If using a Cloud Service environment see the documentation for how to [deploy a code base like the WKND Reference site to a Cloud Service environment](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html?lang=en#deploying).

## Install GraphQL Endpoints{#graphql-endpoint}

GraphQL endpoints need to be configured. This gives project flexibility in determining the exact endpoint that the GraphQL API is exposed. A [CORS](#cors-config) is also needed to grant access to an external application. To expedite the tutorial a package has been pre-created.

1. Download the [aem-guides-wknd-graphql.all-1.0.0-SNAPSHOT.zip](./assets/setup/aem-guides-wknd-graphql.all-1.0.0-SNAPSHOT.zip) package.
1. From the **AEM Start** menu navigate to **Tools** > **Deployment** > **Packages**.
1. Click **Upload Package** and choose the package downloaded in the prior step. Click **Install** to install the package.

The above package also contains the [GraphiQL tool](https://github.com/graphql/graphiql) that will be used in later chapters. More information about the CORS configuration can be [found below](#cors-config).

## Install the sample app{#sample-app}

One of the goals of this tutorial is to show how to consume AEM content from an external application using the GraphQL APIs. This tutorial uses an example React App that has been partially completed to accelerate the tutorial. The same lessons and concepts apply to apps built with iOS, Android or any other platform. The React app is intentionally simple, to avoid unnecessary complexity; it is not meant to be a reference implementation.

1. Open a new terminal window and clone tutorial starter branch using Git:

    ```shell
    $ git clone --branch tutorial/react git@github.com:adobe/aem-guides-wknd-graphql.git
    ```

1. In the IDE of your choice open the file `.env.development` at `aem-guides-wknd-graphql/react-app/.env.development`. Uncomment the `REACT_APP_AUTHORIZATION` line so that the file looks like the following:

    ```plain
    REACT_APP_HOST_URI=http://localhost:4502
    REACT_APP_GRAPHQL_ENDPOINT=/content/graphql/endpoint.gql
    REACT_APP_AUTHORIZATION=admin:admin
    ```

    Ensure that `React_APP_HOST_URI` matches your local AEM instance. In this chapter we will connect the React App directly to the AEM **Author** environment and thus will need to authenticate. This is a common practice during development, since it allows us to quickly make changes on the AEM environment and see them immediately reflected in the app.

    >[!NOTE]
    >
    > In a production scenario the App will connect to an AEM **Publish** environment. This is covered in more detail, later in the tutorial.

1. Navigate into the `aem-guides-wknd-graphql/react-app` folder. Install and start the app:

    ```shell
    $ cd aem-guides-wknd-graphql/react-app
    $ npm install
    $ npm start
    ```

1. A new browser window should automatically launch the app at [http://localhost:3000](http://localhost:3000).

    ![React starter app](assets/setup/react-starter-app.png)

    A list of the current Adventure content from AEM should be displayed.

1. Click one of the adventure images to view the adventure detail. A request is made to AEM to return the detail for an adventure.

    ![Adventure Details view](assets/setup/adventure-details-view.png)

1. Use the browser's developer tools to inspect the **Network** requests. View the **XHR** requests and observe multiple POST requests to `/content/graphql/endpoint.gql`, the GraphQL endpoint configured for AEM.

    ![GraphQL Endpoint XHR request](assets/setup/endpoint-gql.png)

1. You can also view the parameters and JSON response by inspecting the network request. It may be helpful to install a browser extension like [GraphQL Network](https://chrome.google.com/webstore/detail/graphql-network/igbmhmnkobkjalekgiehijefpkdemocm) for Chrome to get a better understanding of the query and response.

    ![GraphQL Network Extension](assets/setup/GraphQL-extension.png)

    *Using the Chrome extension GraphQL Network*

## Modify a Content Fragment

Now that the React app is running, make an update to the content in AEM and see the change reflected in the app.

1. Navigate to AEM [http://localhost:4502](http://localhost:4502).
1. Navigate to **Assets** > **Files** > **WKND Site** > **English** > **Adventures** > **[Bali Surf Camp](http://localhost:4502/assets.html/content/dam/wknd/en/adventures/bali-surf-camp)**.

    ![Bali Surf Camp folder](assets/setup/bali-surf-camp-folder.png)

1. Click into the **Bali Surf Camp** content fragment to open the Content Fragment Editor.
1. Modify the **Title** and the **Description** of the adventure

    ![Modify content fragment](assets/setup/modify-content-fragment-bali.png)

1. Click **Save** to save the changes.
1. Navigate back to the React app at [http://localhost:3000](http://localhost:3000) and refresh to see your changes:

    ![Updated Bali Surf Camp Adventure](assets/setup/overnight-bali-surf-camp-changes.png)

## Congratulations! {#congratulations}

Congratulations, you now have an external application consuming AEM content with GraphQL. Feel free to inspect the code in the React app and continue to experiment with modifying existing Content Fragments.

## Next Steps {#next-steps}

In the next chapter, [Defining Content Fragment Models](content-fragment-models.md), learn how to model content and build a schema with **Content Fragment Models**. You will review existing models and create a new model. You will also learn about the different data types that can be used to define a schema as part of the model.

## (Bonus) CORS Configuration {#cors-config}

AEM, being secure by default, blocks cross-origin requests, preventing unauthorized applications from connecting to and surfacing its content.

To allow this tutorial's React app to interact with AEM's GraphQL API endpoints, a cross-origin resource sharing configuration has been defined in the GraphQL endpoints package.

![Cross-Origin Resource Sharing Configuration](./assets/setup/cross-origin-resource-sharing-configuration.png)

To manually configure this:

1. Navigate to AEM SDK's Web Console at **Tools** > **Operations** > **Web Console**
1. Click on the the row labeled **Adobe Granite Cross-Origin Resource Sharing Policy** to create a new configuration
1. Update the following fields, leaving the others with their default values:
    * Allowed Origins: `localhost:3000`
    * Allowed Origins (Regex): `.* `
    * Allowed Paths: `/content/graphql/endpoint.gql`
    * Allowed Methods: `GET`, `HEAD`, `POST`
        * Only `POST` is required for GraphQL however the other methods can be useful when interacting with AEM in headless manner.
    * Supports Credentials: `Yes`
        * This is required as our React app will communicate with the protected GraphQL end points on AEM Author service.
1. Click **Save**

This configuration allows `POST` HTTP requests originating from `localhost:3000` to the AEM Author service on path `/content/graphql/endpoint.gql`.

This configuration and the GraphQL endpoints are generated from an AEM Project. [View the details here](https://github.com/adobe/aem-guides-wknd-graphql/tree/master/aem-project).
