---
title: AEM Headless quick setup for AEM as a Cloud Service
description: The AEM Headless quick setup gets you hands-on with AEM Headless using content from the WKND Site sample project, and a React App that consumes the content over AEM Headless GraphQL APIs.
version: Cloud Service
feature: Content Fragments, GraphQL API
topic: Headless, Content Management
role: Developer
level: Beginner
kt: 9442
thumbnail: 339073.jpg
exl-id: 62e807b7-b1a4-4344-9b1e-2c626b869e10
---
# AEM Headless quick setup for AEM as a Cloud Service

The AEM Headless quick setup gets you hands-on with AEM Headless using content from the WKND Site sample project, and a sample React App (a SPA) that consumes the content over AEM Headless GraphQL APIs.

## Prerequisites

The following are required to follow this quick setup:

+ AEM as a Cloud Service Sandbox environment (preferably Development)
+ Access to AEM as a Cloud Service and Cloud Manager
  + __AEM Administrator__ access to AEM as a Cloud Service
  + __Cloud Manager - Deployment Manager__ access to Cloud Manager
+ The following tools must be installed locally:
  + [Node.js v10+](https://nodejs.org/en/)
  + [npm 6+](https://www.npmjs.com/)
  + [Git](https://git-scm.com/)
  + An IDE (for example, [Microsoft® Visual Studio Code](https://code.visualstudio.com/))

## 1. Create a Cloud Manager Git repository

First, create a Cloud Manager Git repository which is used to deploy the WKND Site. The WKND Site is a sample AEM website project that contains content (Content Fragments) and a GraphQL AEM endpoint used by the quick setup's React App.

_Screencast of steps_
>[!VIDEO](https://video.tv.adobe.com/v/339073/?quality=12&learn=on)

1. Navigate to [https://my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com)
1. Select the Cloud Manager __Program__ that contains the AEM as a Cloud Service environment to use for this quick setup
1. Create a Git repository for the WKND Site project
    1. Select __Repositories__ in the top navigation
    1. Select __Add Repository__ in the top action bar
    1. Name the new Git repository: `aem-headless-quick-setup`
    1. Select __Save__, and wait for the Git repository to initialize

## 2. Push sample WKND Site project to Cloud Manager Git Repository

With the Cloud Manager Git repository created, clone the WKND Site project's source code from GitHub and push it to Cloud Manager Git repository. Now Cloud Manager to access, and deploy the WKND Site project to the AEM as a Cloud Service environment.

_Screencast of steps_
>[!VIDEO](https://video.tv.adobe.com/v/339074/?quality=12&learn=on)

1. From the command line, clone the sample WKND Site project's source code from GitHub

    ```shell
    $ mkdir -p ~/Code
    $ cd ~/Code
    $ git clone git@github.com:adobe/aem-guides-wknd.git
    ```

1. Add the Cloud Manager Git repository as a remote
    1. Select __Repositories__ in the top navigation
    1. Select __Access Repo Info__ from the top action bar
    1. Execute command found in __Add a remote to your Git repository__ from the command-line

        ```shell
        $ cd aem-guides-wknd
        $ git remote add adobe https://git.cloudmanager.adobe.com/<YOUR ADOBE ORGANIZATION>/aem-headless-quick-setup/
        ```

1. Push the sample project's source code from your local Git repository to the Cloud Manager Git repository

      ```shell
      $ git push adobe master:main
      ```

      When prompted for credentials, provide the __Username__ and __Password__ from Cloud Manager's __Repository Info__ modal. 

## 3. Deploy the WKND Site to AEM as a Cloud Service

With the WKND Site project pushed to the Cloud Manager Git repository, it cannot be deployed to AEM as a Cloud Service using Cloud Manager pipelines.

Keep in mind, the WKND Site project provides sample content that React app consumes over AEM Headless GraphQL APIs.

_Screencast of steps_
>[!VIDEO](https://video.tv.adobe.com/v/339075/?quality=12&learn=on)

1. Attach a __Non-production deployment pipeline__ to the new Git repository
    1. Select __Pipelines__ in the top navigation
    1. Select __Add Pipeline__ from the top action bar
    1. On the __Configuration__ tab
        1. Select __Deployment Pipeline__ option
        1. Set the __Non-Production Pipeline Name__ to `Dev Deployment pipeline`
        1. Select __Deployment Trigger > On Git Changes__ 
        1. Select __Important Metric Failures Behavior > Continue Immediately__ 
        1. Select __Continue__
    1. On the __Source Code__ tab
        1. Select __Full Stack Code__ option
        1. Select the __AEM as a Cloud Service development environment__ from the __Eligible Deployment Environments__ select box
        1. Select `aem-headless-quick-setup` in the __Repository__ select box
        1. Select `main` from the __Git Branch__ select box
        1. Select __Save__
1. Run the __Dev Deployment Pipeline__
    1. Select __Overview__ in the top navigation
    1. Locate the newly created __Dev Deployment pipeline__ in the __Pipelines__ section
    1. Select the __...__ to the right of the pipeline entry
    1. Select __Run__, and confirm in the modal
    1. Select the __...__ to the right of the now-running pipeline
    1. Select __View details__
1. From the pipeline execution's details, monitor progress until it successfully completed. Pipeline execution should take between 45-60 minutes.

## 4. Download and run WKND React app

With AEM as a Cloud Service bootstrapped with the content from the WKND Site project, download, and start the sample WKND React App that consumes the WKND Site's content over AEM Headless GraphQL APIs.

_Screencast of steps_
>[!VIDEO](https://video.tv.adobe.com/v/339076/?quality=12&learn=on)

1. From the command line, clone the React App's source code from GitHub.

    ```shell
    $ cd ~/Code
    $ git clone --branch tutorial/react git@github.com:adobe/aem-guides-wknd-graphql.git
    ```

1. Open the folder `~/Code/aem-guides-wknd-graphql` in your IDE.
1. In the IDE, open the file `react-app/.env.development`.
1. Point to the AEM as a Cloud Service __Publish__ service's host URI from the  `REACT_APP_HOST_URI` property.

    ```plain
    REACT_APP_HOST_URI=https://publish-pXXXX-eYYYY.adobeaemcloud.com/
    ...
    ```

    To find your AEM as a Cloud Service Publish service's host URI:

    1. In Cloud Manager, select __Environments__ in the top navigation
    1. Select __Development__ environment
    1. Locate the __Publish Service (AEM & Dispatcher)__ link __Environment Segments__ table
    1. Copy the link's address, and use it as the AEM as a Cloud Service Publish service's URI

1. In the IDE, save the changes to `.env.development`
1. From the command line, run the React App

    ```shell
    $ cd ~/Code/aem-guides-wknd-graphql/react-app
    $ npm install
    $ npm start
    ```

1. The React App, running locally, starts on [http://localhost:3000](http://localhost:3000) and displays a listing of adventures, which are sourced from AEM as a Cloud Service using AEM Headless' GraphQL APIs.

## 5. Edit content in AEM

With the sample WKND React App connecting to and consuming content from the AEM Headless GraphQL APIs, author content in AEM Author service and see how the React App's experience updates in concert.

_Screencast of steps_
>[!VIDEO](https://video.tv.adobe.com/v/339077/?quality=12&learn=on)

1. Log in to AEM as a Cloud Service Author service
1. Navigate to __Assets > Files > WKND > English > Adventures__
1. Open the __Cycling Southern Utah__ Folder
1. Select the __Cycling Southern Utah__ Content Fragment, and select __Edit__ from the top action bar
1. Update some of the fields of the Content Fragment, for example:
    + Title: `Cycling Utah's National Parks`
    + Trip Length: `6 Days`
    + Difficulty: `Intermediate`
    + Price: `$3500`
    + Primary Image: `/content/dam/wknd/en/activities/cycling/mountain-biking.jpg`
1. Select __Save__ in the top action bar
1. Select __Quick Publish__ from the top action bar's __...__
1. Refresh the React App running on [http://localhost:3000](http://localhost:3000).
1. In the React App, select the now updated and verify the content changes made to the Content Fragment.

1. Using the same approach, in AEM Author service:
    1. Unpublish an existing Adventure Content Fragment, and verify it is removed from the React App experience
    1. Create and publish a new Adventure Content Fragment, and verify it appears in the React App experience

    >[!TIP]
    >
    > If you are unfamiliar with creating and publishing new, or unpublishing existing Content Fragments, watch the screencast above.

## Congratulations!

Congratulations! You've successfully used AEM Headless to power a React App! 

To understand in detail how the React App consumes content from AEM as a Cloud Service, check out [the AEM Headless tutorial](../multi-step/overview.md). The tutorial explores how Content Fragments in AEM as created, and how this React App consumes their content as JSON.

### Next Steps

+ [Start the AEM Headless tutorial](../multi-step/overview.md)
