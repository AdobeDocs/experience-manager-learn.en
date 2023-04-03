---
title: Set up Dispatcher Tools for AEM as a Cloud Service Development
description: AEM SDK's Dispatcher Tools facilitates the local development of Adobe Experience Manager (AEM) projects by making it easy to install, run, and troubleshoot Dispatcher locally.
version: Cloud Service
topic: Development
feature: Dispatcher, Developer Tools
role: Developer
level: Beginner
kt: 4679
thumbnail: 30603.jpg
last-substantial-update: 2023-03-14
exl-id: 9320e07f-be5c-42dc-a4e3-aab80089c8f7
---
# Set up local Dispatcher Tools {#set-up-local-dispatcher-tools}

>[!CONTEXTUALHELP]
>id="aemcloud_localdev_dispatcher"
>title="Local Dispatcher Tools"
>abstract="Dispatcher is an integral part of the overall Experience Manager architecture and should be part of local development setup. The AEM as a Cloud Service SDK includes the recommended Dispatcher Tools version, that facilitates configuring, validating, and simulating Dispatcher locally."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/disp-overview.html" text="Dispatcher in the Cloud"
>additional-url="https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html" text="Download AEM as a Cloud Service SDK"

Adobe Experience Manager (AEM)'s Dispatcher is an Apache HTTP Web server module that provides a security and performance layer between the CDN and AEM Publish tier. Dispatcher is an integral part of the overall Experience Manager architecture and should be part of local development setup.

The AEM as a Cloud Service SDK includes the recommended Dispatcher Tools version, that facilitates configuring, validating, and simulating Dispatcher locally. Dispatcher Tools is comprised of:

+ a baseline set of Apache HTTP Web server and Dispatcher configuration files, located at `.../dispatcher-sdk-x.x.x/src`
+ a configuration validator CLI tool, located at `.../dispatcher-sdk-x.x.x/bin/validate` 
+ a configuration generation CLI tool, located at `.../dispatcher-sdk-x.x.x/bin/validator`
+ a configuration deployment CLI tool, located at `.../dispatcher-sdk-x.x.x/bin/docker_run`
+ an immutable configuration files overwriting CLI tool, located at `.../dispatcher-sdk-x.x.x/bin/update_maven`
+ a Docker image that runs Apache HTTP Web server with the Dispatcher module

Note that `~` is used as shorthand for the User's Directory. In Windows, this is the equivalent of `%HOMEPATH%`.

>[!NOTE]
>
> The videos in this page were recorded on macOS. Windows users can follow along, but use the equivalent Dispatcher Tools Windows commands, provided with each video.

## Prerequisites

1. Windows users must use Windows 10 Professional (or a version that supports Docker)
1. Install [Experience Manager Publish Quickstart Jar](./aem-runtime.md) on the local develop machine.

+ Optionally, install the  latest [AEM reference web site](https://github.com/adobe/aem-guides-wknd/releases) on the local AEM Publish service. This web site is used in this tutorial to visualize a working Dispatcher.

1. Install and start the latest version of [Docker](https://www.docker.com/) (Docker Desktop 2.2.0.5+ / Docker Engine v19.03.9+) on the local development machine.

## Download the Dispatcher Tools (as part of the AEM SDK)

The AEM as a Cloud Service SDK, or AEM SDK, contains the Dispatcher Tools used to run Apache HTTP Web server with the Dispatcher module locally for development, and the compatible QuickStart Jar.

If the AEM as a Cloud Service SDK has already been downloaded to [setup the local AEM runtime](./aem-runtime.md), it does not need to be redownloaded.

1.  Log in to [experience.adobe.com/#/downloads](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?fulltext=AEM*+SDK*&1_group.propertyvalues.property=.%2Fjcr%3Acontent%2Fmetadata%2Fdc%3AsoftwareType&1_group.propertyvalues.operation=equals&1_group.propertyvalues.0_values=software-type%3Atooling&orderby=%40jcr%3Acontent%2Fjcr%3AlastModified&orderby.sort=desc&layout=list&p.offset=0&p.limit=1) with your Adobe ID
    + Your Adobe Organization __must__ be provisioned for AEM as a Cloud Service to download the AEM as a Cloud Service SDK
1.  Click on the latest __AEM SDK__ result row to download

## Extract the Dispatcher Tools from the AEM SDK zip

>[!TIP]
>
> Windows users cannot have any spaces or special characters in the path to the folder containing the Local Dispatcher Tools. If spaces exist in the path, the `docker_run.cmd` fails.

The version of Dispatcher Tools is different from that of the AEM SDK. Ensure that the version of Dispatcher Tools is provided via the AEM SDK version matching the AEM as a Cloud Service version.

1. Unzip the downloaded `aem-sdk-xxx.zip` file
1. Unpack the Dispatcher Tools into `~/aem-sdk/dispatcher`

+   Windows: Unzip `aem-sdk-dispatcher-tools-x.x.x-windows.zip` into `C:\Users\<My User>\aem-sdk\dispatcher` (creating missing folders as needed)
+   macOS Linux&reg;: Execute the accompanying shell script `aem-sdk-dispatcher-tools-x.x.x-unix.sh` to unpack the Dispatcher Tools
    + `chmod a+x aem-sdk-dispatcher-tools-x.x.x-unix.sh && ./aem-sdk-dispatcher-tools-x.x.x-unix.sh`

All commands issued below assume that the current working directory contains the expanding Dispatcher Tools contents.

>[!VIDEO](https://video.tv.adobe.com/v/30601?quality=12&learn=on)

*This video uses macOS for illustrative purposes. The equivalent Windows/Linux commands can be used to achieve similar results.*

## Understand the Dispatcher configuration files

>[!TIP]
> Experience Manager projects created from the [AEM Project Maven Archetype](https://github.com/adobe/aem-project-archetype) are pre-populated this set of Dispatcher configuration files, thus there is no need to copy over from the Dispatcher Tools src folder.

The Dispatcher Tools provides a set of Apache HTTP Web server and Dispatcher configuration files that define behavior for all environments, including local development.

These files are intended to be copied into an Experience Manager Maven project to the `dispatcher/src` folder, if they do not already exist in the Experience Manager Maven project.

A complete description of the configuration files is available in the unpacked Dispatcher Tools as `dispatcher-sdk-x.x.x/docs/Config.html`.

## Validate configurations

Optionally, the Dispatcher and Apache Web server configurations (via `httpd -t`) can be validated using the `validate` script (not to be confused with the `validator` executable). The `validate` script provides a convenient way of running the [three phases](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/validation-debug.html?lang=en) of the `validator`.

+   Usage:
    + Windows: `bin\validate src`
    + macOS Linux&reg;: `./bin/validate.sh ./src`

## Run Dispatcher locally

AEM Dispatcher is run locally using Docker against the `src` Dispatcher and Apache Web server configuration files.

+   Usage:
    + Windows: `bin\docker_run <src-folder> <aem-publish-host>:<aem-publish-port> <dispatcher-port>`
    + macOS Linux&reg;: `./bin/docker_run.sh <src-folder> <aem-publish-host>:<aem-publish-port> <dispatcher-port>`

The `<aem-publish-host>` can be set to `host.docker.internal`, a special DNS name Docker provides in the container that resolves to the host machine's IP. If the `host.docker.internal` does not resolve, please see the [troubleshooting](#troubleshooting-host-docker-internal) section below.

For example to start the Dispatcher Docker container using the default configuration files provided by the Dispatcher Tools:

Start Dispatcher Docker container providing the path to the Dispatcher configuration src folder:

+ Windows: `bin\docker_run src host.docker.internal:4503 8080`
+ macOS Linux&reg;: `./bin/docker_run.sh ./src host.docker.internal:4503 8080`

The AEM as a Cloud Service SDK 's Publish Service, running locally on port 4503 is available through Dispatcher at `http://localhost:8080`.

To run Dispatcher Tools against an Experience Manager project's Dispatcher configuration, point to your project's `dispatcher/src` folder.

+   Windows:

    ```shell
    $ bin\docker_run <User Directory>/code/my-project/dispatcher/src host.docker.internal:4503 8080
    ```

+   macOS Linux&reg;:

    ```shell
    $ ./bin/docker_run.sh ~/code/my-project/dispatcher/src host.docker.internal:4503 8080
    ```

## Dispatcher Tools logs

Dispatcher logs are helpful during local development to understand if and why HTTP Requests are blocked. Log level can be set by prefixing the execution of `docker_run` with environment parameters.

Dispatcher Tools logs are emitted to the standard out when `docker_run` is run.

Useful parameters for debugging Dispatcher include:

+   `DISP_LOG_LEVEL=Debug` sets Dispatcher module logging to Debug level
    + Default value is: `Warn`
+   `REWRITE_LOG_LEVEL=Debug` sets Apache HTTP Web server rewrite module logging to Debug level
    + Default value is: `Warn`
+   `DISP_RUN_MODE` sets the "run mode" of the Dispatcher environment, loading the corresponding run modes Dispatcher configuration files.
    + Defaults to `dev`
+   Valid values: `dev`, `stage`, or `prod`

One or many parameters, can be passed to `docker_run`

+   Windows:

  ```shell
  $ DISP_LOG_LEVEL=Debug REWRITE_LOG_LEVEL=Debug bin\docker_run <User Directory>/code/my-project/dispatcher/src host.docker.internal:4503 8080
  ```

+   macOS Linux&reg;:

  ```shell
  $ DISP_LOG_LEVEL=Debug REWRITE_LOG_LEVEL=Debug ./bin/docker_run.sh ~/code/my-project/dispatcher/src host.docker.internal:4503 8080
  ```

### Log file access

Apache web server and AEM Dispatcher logs can be directly accessed in the Docker container:

+ [Accessing logs in the Docker container](../debugging/aem-sdk-local-quickstart/logs.md#dispatcher-tools-access-logs)
+ [Copying the Docker logs to the local filesystem](../debugging/aem-sdk-local-quickstart/logs.md#dispatcher-tools-copy-logs)

## When to update Dispatcher Tools{#dispatcher-tools-version}

Dispatcher Tools versions increment less frequently than the Experience Manager, and thus Dispatcher Tools require fewer updates in the local development environment.

The recommended Dispatcher Tools version is that which is bundled with the AEM as a Cloud Service SDK that matches the Experience Manager as a Cloud Service version. The version of AEM as a Cloud Service can be found via [Cloud Manager](https://my.cloudmanager.adobe.com/).

+ __Cloud Manager > Environments__, per environment specified by the __AEM Release__ label

![Experience Manager Version](./assets/dispatcher-tools/aem-version.png)

*Note that Dispatcher Tools version does not match the Experience Manager version.*

## How to update the baseline set of Apache and Dispatcher configurations

The baseline set of Apache and Dispatcher configuration is enhanced regularly and released with the AEM as a Cloud Service SDK version. It is best practice to incorporate the baseline configuration enhancements into your AEM project and avoid [local validation](#validate-configurations) and Cloud Manager pipeline failures. Update them using the `update_maven.sh` script from the `.../dispatcher-sdk-x.x.x/bin` folder.

>[!VIDEO](https://video.tv.adobe.com/v/3416744?quality=12&learn=on)

*This video uses macOS for illustrative purposes. The equivalent Windows/Linux commands can be used to achieve similar results.*


Let's assume you created an AEM project in the past using [AEM Project Archetype](https://github.com/adobe/aem-project-archetype), the baseline Apache and Dispatcher configurations were current. Using these baseline configurations your project-specific configurations were created by reusing, and copying the files like `*.vhost`, `*.conf`, `*.farm` and `*.any` from the `dispatcher/src/conf.d` and `dispatcher/src/conf.dispatcher.d` folders. Your local Dispatcher validation and Cloud Manager pipelines were working fine.

Meanwhile, baseline Apache and Dispatcher configurations were enhanced for various reasons like new features, security fixes and optimization. They are released via a newer version of Dispatcher Tools as part of the AEM as a Cloud Service release.

Now, when validating your project-specific Dispatcher configurations against the latest Dispatcher Tools version they start failing. To resolve this, the baseline configurations need to be updated by using below steps:

+ Verify that validation is failing against the latest Dispatcher Tools version

  ```shell
  $ ./bin/validate.sh ${YOUR-AEM-PROJECT}/dispatcher/src

  ...
  Phase 3: Immutability check
  empty mode param, assuming mode = 'check'
  ...
  ** error: immutable file 'conf.d/available_vhosts/default.vhost' has been changed!

  ```

+ Update the immutable files using the `update_maven.sh` script

  ```shell
  $ ./bin/update_maven.sh ${YOUR-AEM-PROJECT}/dispatcher/src

  ...
  Updating dispatcher configuration at folder 
  running in 'extract' mode
  running in 'extract' mode
  reading immutable file list from /etc/httpd/immutable.files.txt
  preparing 'conf.d/available_vhosts/default.vhost' immutable file extraction
  ...
  immutable files extraction COMPLETE
  fd72f4521fa838daaaf006bb8c9c96ed33a142a2d63cc963ba4cc3dd228948fe
  Cloud manager validator 2.0.53
  ```

+   Verify the updated immutable files like `dispatcher_vhost.conf`, `default.vhost`, and `default.farm` and if needed make relevant changes in your custom files which are derived from these files.

+   Revalidate the configurations, it should pass

  ```shell
  $ ./bin/validate.sh ${YOUR-AEM-PROJECT}/dispatcher/src

  ...
  checking 'conf.dispatcher.d/renders/default_renders.any' immutability (if present)
  checking existing 'conf.dispatcher.d/renders/default_renders.any' for changes
  checking 'conf.dispatcher.d/virtualhosts/default_virtualhosts.any' immutability (if present)
  checking existing 'conf.dispatcher.d/virtualhosts/default_virtualhosts.any' for changes
  no immutable file has been changed - check is SUCCESSFUL
  Phase 3 finished
  ```

+ After local verification of changes, commit the updated configurations files

## Troubleshooting

### docker_run results in 'Waiting until host.docker.internal is available' message{#troubleshooting-host-docker-internal}

The `host.docker.internal` is a hostname provided to the Docker contain that resolves to the host. Per docs.docker.com ([macOS](https://docs.docker.com/desktop/networking/), [Windows](https://docs.docker.com/desktop/networking/)):

> From Docker 18.03 onwards the recommendation is to connect to the special DNS name host.docker.internal, which resolves to the internal IP address used by the host

When `bin/docker_run src host.docker.internal:4503 8080` results in the message __Waiting until host.docker.internal is available__, then:

1.  Ensure that the installed version of Docker is 18.03 or greater
2.  You may have a local machine set up that is preventing the registration/resolution of the `host.docker.internal` name. Instead use your local IP.
    +   Windows:
      +   From the Command Prompt, execute `ipconfig`, and record the host's __IPv4 Address__ of the host machine.
      +   Then, execute `docker_run` using this IP address:
    `bin\docker_run src <HOST IP>:4503 8080`
    +   macOS Linux&reg;: 
      +   From Terminal, execute `ifconfig` and record the Host __inet__ IP address, usually the __en0__ device.
      +   Then execute `docker_run` using the host IP address:
    `bin/docker_run.sh src <HOST IP>:4503 8080`

#### Example error

```shell
$ docker_run src host.docker.internal:4503 8080

Running script /docker_entrypoint.d/10-check-environment.sh
Running script /docker_entrypoint.d/20-create-docroots.sh
Running script /docker_entrypoint.d/30-wait-for-backend.sh
Waiting until host.docker.internal is available
```

## Additional Resources

+ [Download AEM SDK](https://experience.adobe.com/#/downloads)
+ [Adobe Cloud Manager](https://my.cloudmanager.adobe.com/)
+ [Download Docker](https://www.docker.com/)
+ [Download the AEM Reference Website (WKND)](https://github.com/adobe/aem-guides-wknd/releases)
+ [Experience Manager Dispatcher Documentation](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html)
