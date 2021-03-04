---
title: Create an Asset Compute project for Asset Compute extensibility
description: Asset Compute projects are Node.js projects, generated using the Adobe I/O CLI, that adhere to a certain structure allowing them to be deployed to Adobe I/O Runtime and integrated with AEM as a Cloud Service.
feature: Asset Compute Microservices
topics: renditions, development
version: cloud-service
activity: develop
audience: developer
doc-type: tutorial
kt: 6269
thumbnail: 40197.jpg
topic: Integrations, Development
role: Developer
level: Intermediate, Experienced
---

# Create an Asset Compute project

Asset Compute projects are Node.js projects, generated using the Adobe I/O CLI, that adhere to a certain structure that allow them to be deployed to Adobe I/O Runtime and integrated with AEM as a Cloud Service. A single Asset Compute project can contain one or more Asset Compute workers, with each having a discrete HTTP end-point referenceable from an AEM as a Cloud Service Processing Profile.

## Generate a project

>[!VIDEO](https://video.tv.adobe.com/v/40197/?quality=12&learn=on)

_Click-through of generating an Asset Compute project (No audio)_

Use the [Adobe I/O CLI Asset Compute plug-in](../set-up/development-environment.md#aio-cli) to generate a new, empty Asset Compute project.

1. From the command line, navigate to the folder to contain the project.
1. From the command line, execute `aio app init` to begin the interactive project generation CLI.
    + This command may spawn a Web browser prompting for authentication to Adobe I/O. If it does, provide your Adobe credentials associated with the [required Adobe services and products](../set-up/accounts-and-services.md). If you are unable to log in, follow [these instructions on how to generate a project](https://github.com/AdobeDocs/project-firefly/blob/master/getting_started/first_app.md#42-developer-is-not-logged-in-as-enterprise-organization-user). 
1. __Select Org__
    + Select the Adobe Org that has AEM as a Cloud Service, Project Firefly are registered with
1. __Select Project__
    + Locate and select the Project. This is the [Project title](../set-up/firefly.md) created from the Firefly project template, in this case `WKND AEM Asset Compute`
1. __Select Workspace__
    +  Select the `Development` workspace
1. __Which Adobe I/O App features do you want to enable for this project? Select components to include__
    + Select `Actions: Deploy runtime actions`
    + Use the arrows keys to select and space to unselect/select, and Enter to confirm selection
1. __Select type of actions to generate__
    + Select `Adobe Asset Compute Worker`
    + Use the arrows keys to select, space to unselect/select, and Enter to confirm selection
1. __How would you like to name this action?__
    + Use the default name `worker`. 
    + If your project contains multiple workers that perform different asset computations, name them semantically

## Generate console.json

The developer tool requires a file named `console.json` that contains the necessary credentials to connect to Adobe I/O. This file is downloaded from the Adobe I/O console. 

1. Open the Asset Compute worker's [Adobe I/O](https://console.adobe.io) project
1. Select the project workspace to download the `console.json` credentials for, in this case select `Development`
1. Go to the root of the Adobe I/O project and tap __Download All__ in the upper-right corner. 
1. A file is downloaded as a `.json` file prefixed with the project and workspace, for example: `wkndAemAssetCompute-81368-Development.json`
1. You can either
    + Rename the file as `config.json` and move it in the root of your Asset Compute worker project. This is the approach in this tutorial.
    + Move it into an arbitrary folder AND reference that folder from your `.env` file with a configuration entry `ASSET_COMPUTE_INTEGRATION_FILE_PATH`. The file path can be absolute or relative to the root of your project. For example:
        + `ASSET_COMPUTE_INTEGRATION_FILE_PATH=/Users/example-user/secrets/wkndAemAssetCompute-81368-Development.json`

        Or
        + `ASSET_COMPUTE_INTEGRATION_FILE_PATH=../../secrets/wkndAemAssetCompute-81368-Development.json.json`

> NOTE
> The file contains credentials. If you store the file within your project, make sure to add it to your `.gitignore` file to prevent from being shared. The same applies to the `.env` file -- These credentials files must not be shared, or stored in Git.

## Review the anatomy of the project

The generated Asset Compute project is a Node.js project for use as a specialized Adobe Project Firefly project. The following structural elements are idiosyncratic to Asset Compute project:

+ `/actions` contains subfolders, and each subfolder defines an Asset Compute worker. 
    + `/actions/<worker-name>/index.js` defines the JavaScript used to perform the work of this worker. 
        + The folder name `worker` is a default, and can be anything, as long as it is registered in the `manifest.yml`.
        + More than one worker folder can be defined under `/actions` as needed, however they must be registered in the `manifest.yml`.
+ `/test/asset-compute` contains the test suites for each worker. Similar to the `/actions` folder, `/test/asset-compute` can contain multiple subfolders, each corresponding to the worker it tests.
    + `/test/asset-compute/worker`, representing a test suite for a specific worker, contains subfolders representing a specific test-case, along with the test input, parameters, and expected output.
+ `/build` contains the output, logs, and artifacts of Asset Compute test case executions.
+ `/manifest.yml` defines what Asset Compute workers the project provides. Each worker implementation must be enumerated in this file to make them available to AEM as a Cloud Service.
+ `/console.json` defines Adobe I/O configurations
    + This file can be generated/updated using the `aio app use` command.
+ `/.aio` contains configurations used by the aio CLI tool. 
    + This file can be generated/updated using the `aio app use` command.
+ `/.env` defines environment variables in a `key=value` syntax and contains secrets that should not be shared. To protect these secrets, this file should NOT be checked into Git and is ignored via the project's default `.gitignore` file. 
    + This file can be generated/updated using the `aio app use` command.
    + Variables defined in this file can be overridden by [exporting variables](../deploy/runtime.md) on the command line.

For more details on project structure review, review the [Anatomy of an Adobe Project Firefly project](https://github.com/AdobeDocs/project-firefly/blob/master/getting_started/first_app.md#5-anatomy-of-a-project-firefly-application).

The bulk of the development takes place in the `/actions` folder developing worker implementations, and in `/test/asset-compute` writing tests for the custom Asset Compute workers.

## Asset Compute project on GitHub

The final Asset Compute project is available on GitHub at:

+ [aem-guides-wknd-asset-compute](https://github.com/adobe/aem-guides-wknd-asset-compute)

_GitHub contains the final state of the project, fully populated with the worker and test cases, but does not contain any credentials, that is, `.env`, `console.json` or `.aio`._

