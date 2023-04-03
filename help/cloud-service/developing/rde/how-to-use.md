---
title: How to use Rapid Development Environment
description: Learn how to use up Rapid Development Environment to deploy code and content from your local machine.
feature: Developer Tools
version: Cloud Service
topic: Development
role: Developer
level: Beginner
jira: KT-11862
thumbnail: KT-11862.png
last-substantial-update: 2023-02-15
---

# How to use Rapid Development Environment

Learn **how to use** Rapid Development Environment (RDE) in AEM as a Cloud Service. Deploy code and content for faster development cycles of your near-final code to the RDE, from your favorite Integrated Development Environment (IDE).

Using [AEM WKND Sites Project](https://github.com/adobe/aem-guides-wknd#aem-wknd-sites-project) you learn how to deploy various AEM artifacts to the RDE by running AEM-RDE's `install` command from your favorite IDE.

- AEM code & content package (all, ui.apps) deployment
- OSGi bundle and config file deployment
- Apache and Dispatcher configs deployment as a zip file
- Individual files like HTL, `.content.xml` (dialog XML) deployment
- Review other RDE commands like `status, reset and delete`

>[!VIDEO](https://video.tv.adobe.com/v/3415491?quality=12&learn=on)

## Prerequisite 

Clone the [WKND Sites](https://github.com/adobe/aem-guides-wknd#aem-wknd-sites-project) project and open it in your favorite IDE to deploy the AEM artifacts onto the RDE.

```shell
$ git clone git@github.com:adobe/aem-guides-wknd.git
```

Then, build and deploy it to the local AEM-SDK by running the following maven command.

```
$ cd aem-guides-wknd/
$ mvn clean install -PautoInstallSinglePackage
```

## Deploy AEM artifacts using the AEM-RDE plugin

Using the `aem:rde:install` command, let's deploy various AEM artifacts. 

### Deploy `all` and `dispatcher` packages

A common starting point is to first deploy the `all` and `dispatcher` packages by running the following commands.

```shell
# Install the 'all' package
$ aio aem:rde:install all/target/aem-guides-wknd.all-2.1.3-SNAPSHOT.zip

# Install the 'dispatcher' zip
$ aio aem:rde:install dispatcher/target/aem-guides-wknd.dispatcher.cloud-2.1.3-SNAPSHOT.zip
```

Upon successful deployments, verify the WKND site on both the author and publish services. You should be able to add, and edit the content on the WKND site pages and publish it.

### Enhance and deploy a component

Let's enhance the `Hello World Component` and deploy it to the RDE.

1.  Open the dialog XML (`.content.xml`) file from `ui.apps/src/main/content/jcr_root/apps/wknd/components/helloworld/_cq_dialog/` folder
1.  Add the `Description` text field after the existing `Text` dialog field

    ```xml
    ...
    <description
        jcr:primaryType="nt:unstructured"
        sling:resourceType="granite/ui/components/coral/foundation/form/textfield"
        fieldLabel="Description"
        name="./description"/>       
    ...
    ```

1.  Open the `helloworld.html` file from `ui.apps/src/main/content/jcr_root/apps/wknd/components/helloworld` folder
1.  Render the `Description` property after the existing `<div>` element of the `Text` property.
    
    ```html
    ...
    <div class="cmp-helloworld__item" data-sly-test="${properties.description}">
        <p class="cmp-helloworld__item-label">Description property:</p>
        <pre class="cmp-helloworld__item-output" data-cmp-hook-helloworld="property">${properties.description}</pre>
    </div>              
    ...
    ```

1.  Verify the changes on local AEM-SDK by performing the maven build or syncing individual files.

1.  Deploy the changes to the RDE via `ui.apps` package or by deploying the individual Dialog and HTL files.

    ```shell
    # Using 'ui.apps' package
    $ cd ui.apps
    $ mvn clean package
    $ aio aem:rde:install target/aem-guides-wknd.ui.apps-2.1.3-SNAPSHOT.zip

    # Or by deploying the individual HTL and Dialog XML
    
    # HTL file
    $ aio aem:rde:install ui.apps/src/main/content/jcr_root/apps/wknd/components/helloworld/helloworld.html -t content-file -p /apps/wknd/components/helloworld/helloworld.html

    # Dialog XML
    $ aio aem:rde:install ui.apps/src/main/content/jcr_root/apps/wknd/components/helloworld/_cq_dialog/.content.xml -t content-xml -p /apps/wknd/components/helloworld/_cq_dialog/.content.xml
    ```

1.  Verify changes on the RDE by adding or editing the `Hello World Component` on a WKND site page.

### Review the `install` command options

In the above individual file deployment command example, the `-t` and `-p` flags are used to indicate the type and destination of the JCR path respectively. Let's review the available `install` command options by running the following command.

```shell
$ aio aem:rde:install --help
```

The flags are self-explanatory, the `-s` flag is useful to target the deployment just to the author or publish services. Use the `-t` flag when deploying the **content-file or content-xml** files along with the `-p` flag to specify the destination JCR path in the AEM RDE environment.

### Deploy OSGi bundle

To learn how to deploy the OSGi bundle, let's enhance the `HelloWorldModel` Java&trade; class and deploy it to the RDE.

1.  Open the `HelloWorldModel.java` file from `core/src/main/java/com/adobe/aem/guides/wknd/core/models` folder
1.  Update the `init()` method as below:

    ```java
    ...
    message = "Hello World!\n"
        + "Resource type is: " + resourceType + "\n"
        + "Current page is:  " + currentPagePath + "\n"
        + "Changes deployed via RDE, lets try faster dev cycles";
    ...
    ```

1.  Verify the changes on local AEM-SDK by deploying the `core` bundle via maven command
1.  Deploy the changes to the RDE by running the following command

    ```shell
    $ cd core
    $ mvn clean package
    $ aio aem:rde:install target/aem-guides-wknd.core-2.1.3-SNAPSHOT.jar
    ```

1.  Verify changes on the RDE by adding or editing the `Hello World Component` on a WKND site page.

### Deploy OSGi configuration

You can deploy the individual config files or complete config package, for example:

```shell
# Deploy individual config file
$ aio aem:rde:install ui.config/src/main/content/jcr_root/apps/wknd/osgiconfig/config/org.apache.sling.commons.log.LogManager.factory.config~wknd.cfg.json

# Or deploy the complete config package
$ cd ui.config
$ mvn clean package
$ aio aem:rde:install target/aem-guides-wknd.ui.config-2.1.3-SNAPSHOT.zip
```

>[!TIP]
>
>To install an OSGi configuration only on an author or publish instance, use the `-s` flag.


### Deploy Apache or Dispatcher configuration

The Apache or Dispatcher config files **cannot be deployed individually**, but the entire Dispatcher folder structure needs to be deployed in the form of a ZIP file.

1.  Make a desired change in the config file of the `dispatcher` module, for demo purposes, update the `dispatcher/src/conf.d/available_vhosts/wknd.vhost` to cache the `html` files only for 60 seconds.
    
    ```
    ...
    <LocationMatch "^/content/.*\.html$">
        Header unset Cache-Control
        Header always set Cache-Control "max-age=60,stale-while-revalidate=60" "expr=%{REQUEST_STATUS} < 400"
        Header always set Surrogate-Control "stale-while-revalidate=43200,stale-if-error=43200" "expr=%{REQUEST_STATUS} < 400"
        Header set Age 0
    </LocationMatch>
    ...
    ```
    
1.  Verify the changes locally, see [Run Dispatcher locally](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/dispatcher-tools.html#run-dispatcher-locally) for more details.
1.  Deploy the changes to the RDE by running the following command:

    ```shell
    $ cd dispatcher
    $ mvn clean install
    $ aio aem:rde:install target/aem-guides-wknd.dispatcher.cloud-2.1.3-SNAPSHOT.zip
    ```
    
1.  Verify changes on the RDE 

## Additional AEM RDE plugin commands

Let's review the additional AEM RDE plugin commands to manage, and interact with the RDE from your local machine.

```shell
$ aio aem:rde --help
Interact with RapidDev Environments.

USAGE
$ aio aem rde COMMAND

COMMANDS
aem rde delete   Delete bundles and configs from the current rde.
aem rde history  Get a list of the updates done to the current rde.
aem rde install  Install/update bundles, configs, and content-packages.
aem rde reset    Reset the RDE
aem rde restart  Restart the author and publish of an RDE
aem rde status   Get a list of the bundles and configs deployed to the current rde.
```

Using the above commands your RDE can be managed from your favorite IDE for faster development/deployment life cycle.

## Next Step

Learn about the [development/deployment life cycle using RDE](./development-life-cycle.md) to deliver features with speed.


## Additional resources

[RDE commands documentation](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/rapid-development-environments.html#rde-cli-commands)

[Adobe I/O Runtime CLI Plugin for interactions with AEM Rapid Development Environments](https://github.com/adobe/aio-cli-plugin-aem-rde#aio-cli-plugin-aem-rde)

[AEM Project setup](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/project-archetype/project-setup.html)
