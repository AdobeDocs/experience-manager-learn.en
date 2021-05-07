---
title: Quick setup SPA Editor and Remote SPA
description: Learn how to get up and running with a remote SPA and AEM SPA Editor in 15 mins!
topic: Headless, SPA, Development
feature: SPA Editor, Core Components, APIs, Developing
role: Developer, Architect
level: Beginner
kt: 7629
thumbnail: 333181.jpeg
---

# Quick Setup

Quick setup is an expedited walk-through illustrating how to install and run the WKND App and as a Remote SPA, and author it using AEM SPA Editor.

Quick setup takes you directly to the end state of this tutorial.

>[!VIDEO](https://video.tv.adobe.com/v/333181/?quality=12&learn=on)

_A video walk-through of the quick setup_

## Prerequisites

This tutorial requires the following:

+ [AEM as a Cloud Service SDK](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/aem-runtime.html?lang=en)
+ [Node.js v14+](https://nodejs.org/en/)
+ [npm v7+](https://www.npmjs.com/)
+ [Java™ 11](https://downloads.experiencecloud.adobe.com/content/software-distribution/en/general.html)
+ [Maven 3.6+](https://maven.apache.org/)
+ [Git](https://git-scm.com/downloads)
+ macOS only prerequisites
    + [Xcode](https://developer.apple.com/xcode/) or [Xcode command line tools](https://developer.apple.com/xcode/resources/)
+ [aem-guides-wknd.all.0.3.0.zip or greater](https://github.com/adobe/aem-guides-wknd/releases)
+ [aem-guides-wknd-graphql source code](https://github.com/adobe/aem-guides-wknd-graphql)


This tutorial assumes:

+ [Microsoft® Visual Studio Code](https://visualstudio.microsoft.com/) as the IDE
+ A working directory of `~/Code/wknd-app`
+ Running the AEM SDK as an Author service on `http://localhost:4502`
+ Running the AEM SDK with the local `admin` account with password `admin`
+ Running the SPA on `http://localhost:3000`

## Start the AEM SDK Quickstart

Download and install the AEM SDK Quickstart on port 4502, with default `admin/admin` credentials.

1. [Download latest AEM SDK](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?fulltext=AEM*+SDK*&orderby=%40jcr%3Acontent%2Fjcr%3AlastModified&orderby.sort=desc&layout=list&p.offset=0&p.limit=1)
1. Unzip the AEM SDK to `~/aem-sdk`
1. Run the AEM SDK Quickstart Jar

   ```
   $ java -jar aem-sdk-quickstart-xxx.jar
   
   # Provide `admin` as the admin user's password
   ```

AEM SDK will start and automatically launch on [http://localhost:4502](http://localhost:4502). Log in using the following credentials:

+ Username: `admin`
+ Password: `admin`

## Download and install WKND Site package

This tutorial has a dependency on __WKND 0.3.0+'s__ project (for content).

1. [Download the latest version of `aem-guides-wknd.all.x.x.x.zip`](https://github.com/adobe/aem-guides-wknd/releases)
1. Log in to AEM SDK's Package Manager at [http://localhost:4502/crx/packmgr](http://localhost:4502/crx/packmgr) with the `admin` credentials.
1. __Upload__ the `aem-guides-wknd.all.x.x.x.zip` downloaded in step 1
1. Tap the __Install__ button for the entry `aem-guides-wknd.all-x.x.x.zip`

## Download and install WKND App SPA packages

To perform a quick setup, AEM packages are provided that contain the tutorial's final  AEM configuration and content.

1. [Download `wknd-app.all.x.x.x.zip`](./assets/quick-setup/wknd-app.all-1.0.0-SNAPSHOT.zip)
1. [Download `wknd-app.ui.content.sample.x.x.x.zip`](./assets/quick-setup/wknd-app.ui.content.sample-1.0.0.zip)
1. Log in to AEM SDK's Package Manager at [http://localhost:4502/crx/packmgr](http://localhost:4502/crx/packmgr) with the `admin` credentials.
1. __Upload__ the `wknd-app.all.x.x.x.zip` downloaded in step 1
1. Tap the __Install__ button for the entry `wknd-app.all.x.x.x.zip`
1. __Upload__ the `wknd-app.ui.content.sample.x.x.x.zip` downloaded in step 2
1. Tap the __Install__ button for the entry `wknd-app.ui.content.sample.x.x.x.zip`

## Download the WKND App source

Download the WKND App's source code by from Github.com, and switch the branch containing the changes to the SPA performed in this tutorial.

```
$ mkdir -p ~/Code/wknd-app
$ cd ~/Code/wknd-app
$ git clone https://github.com/adobe/aem-guides-wknd-graphql.git
$ cd aem-guides-wknd-graphql
$ git checkout -b feature/spa-editor
$ git pull origin feature/spa-editor
```

## Start the SPA application

From the project's root, install the SPA projects npm dependencies and run the application.

```
$ cd ~/Code/wknd-app/aem-guides-wknd-graphql/react-app
$ npm install
$ npm run start
```

If there are errors when running `npm install` try the following steps:

```
$ cd ~/Code/wknd-app/aem-guides-wknd-graphql/react-app
$ rm -f package-lock.json
$ npm install --legacy-peer-deps
$ npm run start
```

Verify that the SPA is running at [http://localhost:3000](http://localhost:3000).

## Author content in AEM SPA Editor

Before authoring content arrange your browser windows such that AEM Author (`http://localhost:4502`) is on the left, and the remote SPA  (`http://localhost:3000`) runs on the right. This arrangement allows you to see how changes to AEM-sourced content are immediately reflected in the SPA.

1. Log in to [AEM SDK Author service](http://localhost:4502) as `admin`
1. Navigate to __Sites > WKND App > us > en__
1. Edit __WKND App Home Page__
1. Switch to __Edit__ mode

### Author the Home view's fixed component

1. Tap on the text __WKND Adventures__ to activate the fixed Title component (hardcoded into the SPA's Home view)
1. Tap the __wrench__ icon on the Title component's action bar
1. Changes the Title component's content and save
1. Refresh the SPA running on `http://localhost:3000` and see that the changes reflected

### Author the Home view's container component

1. While still editing the __WKND App Home Page__...
1. Expand the __SPA Editor's sidebar__ (on the left)
1. Tap the __Components__ icons
1. Add, change, or remove components from the container component that sits beneath the WKND logo and above the fixed Title component
1. Refresh the SPA running on `http://localhost:3000` and see that the changes reflected

### Author a container component on a dynamic route

1. Switch to __Preview__ mode in SPA Editor
1. Tap on the __Bali Surf Camp__ card and navigate to its dynamic route
1. Add, change, or remove components from the container component that sites above the __Itinerary__ heading
1. Refresh the SPA running on `http://localhost:3000` and see that the changes reflected

New AEM pages under the __WKND App Home page > Adventure__ _must_ have an AEM page name that matches the corresponding adventure's Content Fragment's name. This is because the SPA route to AEM Page mapping is based off the last segment of the route, which is the Content Fragment's name.

## Congratulations!

You just got quick taste of how AEM SPA Editor can enhance your SPA with controlled, editable areas! If you're interested - check out the rest of the tutorial, but make sure to start fresh, since in this quick setup your local development environment is now in  end state of the tutorial!
