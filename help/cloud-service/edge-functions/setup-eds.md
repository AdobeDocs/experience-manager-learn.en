---
title: Set up AEM Edge Functions on Edge Delivery Services
description: Learn how to set up AEM Edge Functions on Edge Delivery Services, from onboarding your site in Cloud Manager to creating a project from the boilerplate template and deploying a working endpoint.
version: Experience Manager as a Cloud Service
feature: Developing, Edge Delivery Services
topic: Development, Architecture
role: Admin, Developer
level: Intermediate
doc-type: Tutorial
jira: KT-21735
thumbnail: KT-21735.jpeg
last-substantial-update: 2026-06-25
---
# Set up AEM Edge Functions on Edge Delivery Services

Learn how to set up AEM Edge Functions on an Edge Delivery Services site.

This tutorial covers Edge Delivery site onboarding in Cloud Manager, CLI installation, project setup from the boilerplate template, CDN configuration, and deployment of a working endpoint.

This tutorial uses the [Frescopa Site Project](https://github.com/aem-showcase/frescopa) as the demo site. You can follow the same steps with your own Edge Delivery Services site.

## What you'll build

AEM Edge Functions are JavaScript modules that run on Adobe CDN at the edge, not on your Edge Delivery origin. You deploy one AEM Edge Function named `my-edge-function` with two routes:

- `/hello-world` returns a greeting from the edge
- `/weather` detects the visitor's location at the edge, calls the [Open-Meteo API](https://open-meteo.com/en/docs), and returns the current temperature for their city

During development, you test your AEM Edge Function locally with the dev server. Then you deploy `edgeFunctions.yaml` and `cdn.yaml` through the Edge Delivery configuration pipeline, push the AEM Edge Function (JavaScript module) to Adobe CDN, and verify both endpoints on your site domain (for example, `https://myfrescopa.enablementadobe.com/hello-world`).

The high-level steps:

1. Onboard your Edge Delivery site to Cloud Manager
1. Install Adobe CLI and AEM Edge Functions plugin
1. Set up AEM Edge Functions on Edge Delivery Services
1. Create the AEM Edge Functions project from the boilerplate template
1. Clone, review, and run the AEM Edge Functions project locally
1. Review, manage, and deploy CDN configuration
1. Build and deploy AEM Edge Functions to Adobe CDN
1. Verify the endpoint is working

## Prerequisites

Ensure the following are in place before starting.

- [Node.js](https://nodejs.org/) and npm installed locally
- A GitHub account to create a project from the boilerplate template
- An Edge Delivery Services add-on for your Cloud Manager program
- Deployment Manager role in Cloud Manager
- The [Frescopa Site Project](https://github.com/aem-showcase/frescopa) or your own Edge Delivery site project

>[!NOTE]
>
>Edge Delivery Services supports up to **three AEM Edge Functions per program**, intended to support dev, staging, and prod branches of your site(s).

## Step 1: Onboard your Edge Delivery site to Cloud Manager

Before you set up AEM Edge Functions, onboard your Edge Delivery site in Cloud Manager. This step uses Cloud Manager only and does not require the Adobe CLI.

If your site is already onboarded, verify it appears in Cloud Manager and skip to Step 2.

The following steps use the [Frescopa Site Project](https://github.com/SachinMali/frescopa) as the demo site.

1. Log in to [Cloud Manager](https://my.cloudmanager.adobe.com/) and open your program with an Edge Delivery Services add-on. On the program overview, confirm the **Edge Delivery** tab is visible.

1. On the **Edge Delivery** tab, complete the **Edge Delivery to-do list**. Key steps include:

    1. **Add Edge Delivery site**:
        - **Site name**: `Frescopa`
        - **Edge Delivery origin**: `https://main--frescopa--sachinmali.aem.live/`

        The format is `https://<branch>--<site-name>--<organization-name>.aem.live/` where `<branch>`, `<site-name>` and `<organization-name>` are the branch, site name and organization name of the Edge Delivery Services site project respectively. 
        
        Ideally you try to set up the `dev` branch of the Edge Delivery Services site project.However, see below screenshot for our demo site.

        ![Add Edge Delivery site](./assets/setup/eds/cloud-manager-add-edge-delivery-site.png)

    1. **Add domain**:
        - **Domain name**: `myfrescopa.enablementadobe.com`

        You must have a custom domain name set up to deploy the AEM Edge Functions project even if you are trying on dev site mapped to the dev branch of Edge Delivery Services site project.

    1. **Add SSL certificate**:
        - **Certificate type**: Customer managed (OV/EV)
        - **Certificate name**: `enablementadobe.com`
        - **Certificate**: The signed certificate file content between `-----BEGIN CERTIFICATE-----` and `-----END CERTIFICATE-----`
        - **Private key**: The private key file content between `-----BEGIN PRIVATE KEY-----` and `-----END PRIVATE KEY-----`
        - **Certificate chain**: The certificate chain file content between `-----BEGIN CERTIFICATE-----` and `-----END CERTIFICATE-----`

        ![Add SSL certificate](./assets/setup/eds/cloud-manager-add-ssl-certificate.png)

        You can use Adobe managed (DV) certificate as well, for tutorial purpose we are using a customer managed (OV/EV) certificate as an example.

    1. **Add a DNS record** in your DNS hosting service for `myfrescopa.enablementadobe.com`.

    1. **Map the domain** `myfrescopa.enablementadobe.com` to the Adobe managed CDN.

        ![Map domain to Adobe managed CDN](./assets/setup/eds/cloud-manager-map-domain-to-adobe-managed-cdn.png)

1. Verify the site appears in the Edge Delivery Sites table. The demo Frescopa site is reachable at [https://myfrescopa.enablementadobe.com/](https://myfrescopa.enablementadobe.com/).

    ![Edge Delivery site in Cloud Manager](./assets/setup/eds/cloud-manager-edge-delivery-sites-table.png)

For a complete walkthrough, see [Add an Edge Delivery site to Cloud Manager](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/edge-delivery-sites/add-edge-delivery-site).

## Step 2: Install CLI and plugins

Install or update the Adobe `aio` [CLI](https://github.com/adobe/aio-cli) and the AEM Edge Functions plugin.

>[!BEGINTABS]

>[!TAB Fresh install]

For a fresh install, run the following commands:

```bash
# Install the Adobe CLI
$ npm install -g @adobe/aio-cli

# Install the AEM Edge Functions plugin
$ aio plugins install @adobe/aio-cli-plugin-aem-edge-functions
```

>[!TAB Update existing]

Update the Adobe CLI and installed plugins:

```bash
# Update the Adobe CLI
$ aio update

# List installed plugins (confirm the AEM Edge Functions plugin is listed)
$ aio plugins

# Update the installed plugins
$ aio plugins update
```

>[!ENDTABS]

For example, the successful installation of the CLI and AEM Edge Functions plugin should look like the following:

![CLI version output](./assets/setup/eds/cli-version-output-eds.png)

## Step 3: Set up AEM Edge Functions

The AEM Edge Functions must be set up on the Edge Delivery Services site domain. It allows you to deploy code and config files to Adobe CDN so you can invoke the routes supported by AEM Edge Functions from JavaScript code in your site.

To set up AEM Edge Functions, run the following command:

```bash
$ aio aem edge-functions setup
```

If you are not already logged in to Adobe IMS, the command triggers login flow. The setup process prompts for program, site type, Edge Delivery site, and ADC project config details. Select **Edge Delivery Services** as the site type. The setup details are stored in the `.aio` file, it provides the context for the AEM Edge Functions CLI commands hereafter.

![AEM Edge Functions setup prompts](./assets/setup/eds/aem-edge-functions-setup-prompts-eds.png)

Note that setup associates the [Frescopa Edge Delivery site](https://github.com/SachinMali/frescopa) with the domain `myfrescopa.enablementadobe.com`.

>[!IMPORTANT]
>
>The configuration of Adobe Developer Console (ADC) project for API credentials - that includes the AEM Content Delivery Network (CDN) API card - is not done as part of this tutorial. However, it must be done when you want to deploy the AEM Edge Functions projects from your CI/CD system. See [Adobe Developer Console Integration](https://github.com/adobe/aio-cli-plugin-aem-edge-functions#adobe-developer-console-integration) and [CI/CD Setup](https://github.com/adobe/aio-cli-plugin-aem-edge-functions#cicd-setup) for more information.

Use the following command to review the AEM Edge Functions setup details:

```bash
$ aio aem edge-functions info
```

The output should look like the following:

![AEM Edge Functions info output](./assets/setup/eds/aem-edge-functions-info-output-eds.png)

## Step 4: Create AEM Edge Functions project

Create the AEM Edge Functions project from the [aem-edge-functions-boilerplate](https://github.com/adobe/aem-edge-functions-boilerplate) GitHub template. The boilerplate includes the files and configuration you need to get started.

1. Navigate to [aem-edge-functions-boilerplate](https://github.com/adobe/aem-edge-functions-boilerplate) on GitHub.

1. In the top-right corner, select **Use this template** > **Create a new repository**.

    ![AEM Edge Functions use this template option](./assets/setup/eds/github-use-this-template-eds.png)

1. Provide the repository name (for example, `frescopa-edge-functions`), add a description, set visibility to **Private**, and select **Create repository**.

    ![AEM Edge Functions create repository details](./assets/setup/eds/github-create-repository-details-eds.png)

## Step 5: Clone, review, and run AEM Edge Functions project

### Clone the AEM Edge Functions project

Clone the repository you created in Step 4, then open it alongside the Frescopa (or your own) Edge Delivery site project in your IDE. Most editors support workspaces or multi-root views that let you work in both projects at the same time.

```bash
# Clone the repository
$ git clone https://github.com/<your-org>/<your-project-name>.git
```

For example, see the Frescopa Edge Delivery site project and Frescopa AEM Edge Functions project as workspace in IDE:

![Frescopa Edge Delivery site project and Frescopa AEM Edge Functions project as workspace in IDE](./assets/setup/eds/ide-workspace-with-frescopa-projects-eds.png)

### Review the AEM Edge Functions project

Before making changes or deploying the AEM Edge Functions project, review the key files that define the AEM Edge Functions contract.

1. `package.json` contains the project dependencies. Note the `@fastly/js-compute` dependency. For more information, see [JavaScript on the Compute platform](https://www.fastly.com/documentation/guides/compute/developer-guides/javascript/).

1. `src/index.js` is the function entry point and contains the main logic for the project. It uses Fastly Compute's `addEventListener("fetch", ...)` pattern. All incoming requests flow through the `handleRequest` function, where you add route matching logic. For example, the following code is from the boilerplate:

    ```js
    // src/index.js
    addEventListener("fetch", (event) => event.respondWith(handleRequest(event)));

    async function handleRequest(event) {
        const req = event.request;
        const url = new URL(req.url);

        let finalResponse;

        try {
            // Route matching logic
            if (url.pathname === "/" && req.method === "GET") {
                finalResponse = new Response("Hello World from the edge!", { status: 200 });
            } else if (url.pathname === "/hello-world" && req.method === "GET") {
                finalResponse = new Response("Hello World from the edge!", { status: 200 });
            } else if (url.pathname === "/weather" && req.method === "GET") {
                finalResponse = await weatherHandler(req, event.client);
            } else {
                finalResponse = response.notFound();
            }
        } catch (err) {
            finalResponse = new Response("Internal Server Error", { status: 500 });
        }

        return finalResponse;
    }
    ```

    A single AEM Edge Function can handle multiple routes through the `if` statements in `handleRequest`.

1. `fastly.toml` configures the local development server. For more information, see the [Fastly.toml reference](https://www.fastly.com/documentation/reference/compute/fastly-toml/).

1. `config/` contains the config files for the AEM Edge Function service and CDN routing rules. Deploy these files through the Edge Delivery configuration pipeline in Cloud Manager. Step 6 covers that process.

Review the remaining project files such as `test/`, `src/lib/`, and `README.md` to understand the full setup.

### Run the AEM Edge Functions project locally

To iterate quickly, you can run the AEM Edge Functions project locally. From the AEM Edge Functions project directory, install dependencies and start the local development server:

```bash
# Navigate to the project directory (replace with your project name)
$ cd frescopa-edge-functions

# Install dependencies
$ npm install

# Start the local development server
$ aio aem edge-functions serve
```

The server starts at `http://127.0.0.1:7676`.

For example, the output should look like the following screenshot:

![Local development server output](./assets/setup/eds/local-development-server-output-eds.png)

## Step 6: Review and deploy CDN configuration

The AEM Edge Functions project includes CDN configuration files. Review them and deploy using the Edge Delivery configuration pipeline in Cloud Manager.

### Review CDN configuration

Review the CDN configuration files in the `config/` directory of the AEM Edge Functions project.

1. `config/edgeFunctions.yaml` declares the AEM Edge Function service. For example:

```yaml
kind: "EdgeFunctions"
version: "1"
data:
  functions:
    - name: my-edge-function
```

For more information on supported properties, see [edgeFunctions.yaml reference](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/edge-functions#declare-functions).

1. `config/cdn.yaml` declares the CDN routing rules that direct traffic to the AEM Edge Function service. For example:

```yaml
kind: 'CDN'
version: '1'
data:
  originSelectors:
    rules:
      - name: route-weather-to-edge-function
        when: { reqProperty: path, equals: "/weather" }
        action:
          type: selectAemOrigin
          originName: edgefunction-my-edge-function
          skipCache: true
      - name: route-hello-world-to-edge-function
        when: { reqProperty: path, equals: "/hello-world" }
        action:
          type: selectAemOrigin
          originName: edgefunction-my-edge-function
          skipCache: true
```

Key call outs:
    - The `originName` must follow the pattern `edgefunction-<edge-function-name>`, where `<edge-function-name>` is the name of the AEM Edge Function declared in `edgeFunctions.yaml`.
    - The `type` must be `selectAemOrigin`.
    - The `skipCache` is set to `true` to bypass the CDN cache for the request.

For more information, see [Origin selectors](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn-configuring-traffic#origin-selectors).

### Manage CDN configuration

Deploy CDN configuration through the Cloud Manager configuration pipeline. First, make the `config/` files from your AEM Edge Functions project available to Cloud Manager. You have two options:

1. **Adobe repository**: Create a new repository in Cloud Manager for your program.

1. **Private repository**: Link your existing GitHub repository to Cloud Manager.

This tutorial uses the Frescopa AEM Edge Functions project from Step 4 as a private repository.

1. In Cloud Manager, open **Repositories** and select **Add Repository**.

1. In the **Add Repository** dialog, select **Private Repository**, then provide the repository name, URL, and type. Select **Save**.

    ![Add Repository dialog](./assets/setup/eds/cloud-manager-add-repository-dialog-eds.png)

1. Complete the steps in the **Private Repository Ownership Validation** dialog.

    ![Private Repository Ownership Validation dialog](./assets/setup/eds/cloud-manager-private-repository-ownership-validation-dialog-eds.png)

    1. Grant Cloud Manager access to the repository:

        ![Cloud Manager for AEM repository access](./assets/setup/eds/cloud-manager-for-aem-repository-access-eds.png)

    1. Store the validation secret in your AEM Edge Functions project repository:

        ![Secret stored in AEM Edge Functions project repository](./assets/setup/eds/secret-stored-in-edge-functions-project-repository-eds.png)

After validation completes, the private repository appears in the **Repositories** table.

### Deploy CDN configuration

Create and run an Edge Delivery configuration pipeline in Cloud Manager.

1. On the program overview page, open the **Edge Delivery** tab. Under **Pipelines**, select **Add Edge Delivery Pipeline**.

    ![Add Edge Delivery Pipeline button](./assets/setup/eds/cloud-manager-add-edge-delivery-pipeline-button-eds.png)

1. In the **Add Edge Delivery Pipeline** dialog, provide a name and select **Continue**.

    ![Add Edge Delivery Pipeline dialog](./assets/setup/eds/cloud-manager-add-edge-delivery-pipeline-dialog-eds.png)

1. On the **Source Code** step, select the private repository you added, the `main` branch, and `/config` as the code location. Select **Save**.

    ![Source Code step](./assets/setup/eds/cloud-manager-source-code-step-eds.png)

1. Run the pipeline by selecting **...** next to the pipeline name, then **Run**.

    ![Run Edge Delivery pipeline](./assets/setup/eds/cloud-manager-run-edge-delivery-pipeline-eds.png)

The successful run deploys the edgeFunctions.yaml and cdn.yaml files to the Edge Delivery site domain.

Verify the CDN configuration was deployed successfully:

```bash
$ aio aem edge-functions list
```

The output should list `my-edge-function` (or whatever name you declared in `edgeFunctions.yaml`).

![AEM Edge Functions list output](./assets/setup/eds/aem-edge-functions-list-output-eds.png)

## Step 7: Build and deploy AEM Edge Functions project

Build and deploy the AEM Edge Functions project using following commands, the commands use the context stored in the `.aio` file.

```bash
# Navigate to the AEM Edge Functions project directory (replace with your project name)
$ cd frescopa-edge-functions

# Review to make sure you are deploying to the correct Edge Delivery Services site
$ aio aem edge-functions info

# Build the project
$ aio aem edge-functions build

# Deploy to Adobe CDN
$ aio aem edge-functions deploy my-edge-function
```

The name passed to `deploy` must match the `name` declared in `config/edgeFunctions.yaml`. Also you must be part of the _Cloud Manager Deployment Manager_ product profile.

For example, the output should look like the following screenshot:

![AEM Edge Functions build and deploy output](./assets/setup/eds/aem-edge-functions-build-and-deploy-output-eds.png)

>[!IMPORTANT]
>
>To deploy the AEM Edge Functions project from your CI/CD system, you need Adobe Developer Console (ADC) project for API credentials. See [Adobe Developer Console Integration](https://github.com/adobe/aio-cli-plugin-aem-edge-functions#adobe-developer-console-integration) and [CI/CD Setup](https://github.com/adobe/aio-cli-plugin-aem-edge-functions#cicd-setup) for more information.


## Step 8: Verify the endpoint

Verify the deployed endpoints in a browser or with curl:

```bash
$ curl https://myfrescopa.enablementadobe.com/hello-world
$ curl https://myfrescopa.enablementadobe.com/weather
```

Replace the domain with your Edge Delivery site domain from Step 1.

For example, the responses look like the following screenshot:

![Live endpoint responses](./assets/setup/eds/live-endpoint-responses-eds.png)

>[!NOTE]
>
>The `edgefunction-pXXXXX-dYYYYY-<edge-function-name>.adobeaemcloud.com` domain is available for debugging only and is not guaranteed to be stable. In production, requests reach the AEM Edge Function through your site's custom domain via the CDN routing rules in `cdn.yaml`. 

In real-world scenarios, use AEM Edge Functions for server-side logic at the CDN and call them from your site's [block](https://www.aem.live/docs/exploring-blocks) JavaScript. See the [AEM Edge Functions product documentation](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/edge-functions) for advanced configuration.

## Summary

You onboarded the Frescopa Edge Delivery site to Cloud Manager, installed the CLI, set up AEM Edge Functions on Edge Delivery Services, created and ran the project locally, deployed CDN configuration, built and deployed the AEM Edge Function, and verified the endpoint.

## Additional resources

- [AEM Edge Functions product documentation](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/edge-functions)
- [Caching in AEM Edge Functions](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/edge-functions-caching)
- [Traffic Filter and WAF Rules](../security/traffic-filter-and-waf-rules/overview.md)
- [CDN configuration in AEM as a Cloud Service](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn-configuring-traffic)
- [Use config pipelines](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/operations/config-pipeline)
