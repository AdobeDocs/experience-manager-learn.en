---
title: Set up a local development environment for Edge Delivery Services
description: How to setup a local development environment for Edge Delivery Services.
version: 6.5, Cloud Service
feature: Edge Delivery Services
topic: Development
role: Developer
level: Beginner
doc-type: Technical Video
last-substantial-update: 2023-11-15
jira: KT-14483
thumbnail: 3425717.jpeg
duration: 181
exl-id: 0f3e50f0-88d8-46be-be8b-0f547c3633a6
---
# Set up a local development environment

How to setup a local development environment for development for Edge Delivery Services.

>[!VIDEO](https://video.tv.adobe.com/v/3425717/?learn=on)


## Steps outlined in video

1. Install the AEM CLI

    ```
    $ sudo npm install -g @adobe/aem-cli
    ```

1. Change directory to your project directory that is a git repository made from the [AEM boilerplate](https://github.com/adobe/aem-boilerplate) template.

    ```
    $ git clone git@github.com:my-org/my-project.git
    $ cd my-project
    ```

1. Run the AEM CLI to start the local AEM instance.

    ```
    $ pwd
      /Users/my-user/my-project

    $ aem up
        ___    ________  ___                          __      __ 
       /   |  / ____/  |/  /  _____(_)___ ___  __  __/ /___ _/ /_____  _____
      / /| | / __/ / /|_/ /  / ___/ / __ `__ \/ / / / / __ `/ __/ __ \/ ___/
     / ___ |/ /___/ /  / /  (__  ) / / / / / / /_/ / / /_/ / /_/ /_/ / /
    /_/  |_/_____/_/  /_/  /____/_/_/ /_/ /_/\__,_/_/\__,_/\__/\____/_/

    info: Starting AEM dev server vx.x.x
    info: Local AEM dev server up and running: http://localhost:3000/
    info: Enabled reverse proxy to https://main--my-project--my-org.hlx.page
    opening default browser: http://localhost:3000/
    ```    

1. Open http://localhost:3000/ your web browser to see your AEM web site.
