---
title: How to set up Rapid Development Environment
description: Learn how to set up Rapid Development Environment for AEM as a Cloud Service.
feature: Developer Tools
version: Cloud Service
topic: Development
role: Developer
level: Beginner
jira: KT-11861
thumbnail: KT-11861.png
last-substantial-update: 2023-02-15
exl-id: ab9ee81a-176e-4807-ba39-1ea5bebddeb2
duration: 528
---
# How to set up Rapid Development Environment

Learn **how to set up** Rapid Development Environment (RDE) in AEM as a Cloud Service.

This video shows:

- Adding an RDE to your program using Cloud Manager
- RDE login flow using Adobe IMS, how it is similar to any other AEM as a Cloud Service environment
- Setup of [Adobe I/O Runtime Extensible CLI](https://developer.adobe.com/runtime/docs/guides/tools/cli_install/) also known as the `aio CLI` 
- Setup and configuration of AEM RDE and Cloud Manager `aio CLI` plugin

>[!VIDEO](https://video.tv.adobe.com/v/3415490?quality=12&learn=on)

## Prerequisite 

The following should be installed locally:

- [Node.js](https://nodejs.org/en/) (LTS - Long-Term Support)
- [npm 8+](https://docs.npmjs.com/)

## Local setup

To deploy the [WKND Sites Project's](https://github.com/adobe/aem-guides-wknd#aem-wknd-sites-project) code and content onto the RDE from your local machine, complete the following steps.

### Adobe I/O Runtime Extensible CLI 

Install the Adobe I/O Runtime Extensible CLI, also known as the `aio CLI` by running the following command from the command line. 

```shell
$ npm install -g @adobe/aio-cli
```

### AEM plugins

Install Cloud Manager and AEM RDE plugins by using the `aio cli`'s `plugins:install` command.

```shell
$ aio plugins:install @adobe/aio-cli-plugin-cloudmanager

$ aio plugins:install @adobe/aio-cli-plugin-aem-rde
```

The Cloud Manager plugin, allows developers to interact with Cloud Manager from the command line.

The AEM RDE plugin, allows developers to deploy code and content from the local machine.

Also, to update the plugins use the `aio plugins:update` command.

## Configure AEM plugins

The AEM plugins must be configured to interact with your RDE. First, using the Cloud Manager UI, copy the values of the Organization, Program, and Environment ID.

1.  Organization ID: Copy the value from **Profile Picture > Account info(internal) > Modal Window > Current Org ID**

    ![Organization ID](./assets/Org-ID.png)

1.  Program ID: Copy the value from **Program Overview > Environments > {ProgramName}-rde > Browser URI > numbers between `program/` and `/environment`**

1.  Environment ID: Copy the value from **Program Overview > Environments > {ProgramName}-rde > Browser URI > numbers after `environment/`**

    ![Program and Environment ID](./assets/Program-Environment-Id.png)

1.  Then, by using the `aio cli`'s `config:set` command set these values by running the following command.

    ```shell
    $ aio config:set cloudmanager_orgid <org-id>

    $ aio config:set cloudmanager_programid <program-id>

    $ aio config:set cloudmanager_environmentid <env-id>
    ```

You can verify the current config values by running the following command.

```shell
$ aio config:list
```

Also, to switch or know which organization you are currently logged in to, you can use the below command.

```shell
$ aio where
```

## Verify RDE access

Verify the AEM RDE plugin installation and configuration by running the following command.

```shell
$ aio aem:rde:status
```

The RDE status information is displayed like environment status, the list of _your AEM project_ bundles and configurations on author and publish service.

## Next Step

Learn [how to use](./how-to-use.md) an RDE to deploy code and content from your favorite Integrated Development Environment (IDE) for faster development cycles.


## Additional resources

[Enabling RDE in a program documentation](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/rapid-development-environments.html#enabling-rde-in-a-program)

Setup of [Adobe I/O Runtime Extensible CLI](https://developer.adobe.com/runtime/docs/guides/tools/cli_install/) also known as the `aio CLI` 

[AIO CLI usage and commands](https://github.com/adobe/aio-cli#usage)

[Adobe I/O Runtime CLI Plugin for interactions with AEM Rapid Development Environments](https://github.com/adobe/aio-cli-plugin-aem-rde#aio-cli-plugin-aem-rde)

[Cloud Manager AIO CLI plugin](https://github.com/adobe/aio-cli-plugin-cloudmanager)
