---
title: Set up AEM Edge Functions on AEM as a Cloud Service
description: Learn how to set up AEM Edge Functions on AEM as a Cloud Service, from installing the CLI and creating a project from the boilerplate template to deploying a working endpoint.
version: Experience Manager as a Cloud Service
feature: Developing
topic: Development, Architecture
role: Developer
level: Intermediate
doc-type: Tutorial
jira: KT-XXXXX
thumbnail: KT-XXXXX.jpeg
last-substantial-update: 2026-06-12
duration: 0
exl-id: TODO-REPLACE-WITH-GENERATED-EXLID
---
# Set up AEM Edge Functions on AEM as a Cloud Service

>[!IMPORTANT]
>
>AEM Edge Functions is currently in beta. Features and documentation may change. For feedback, contact [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com).

Learn how to set up [AEM Edge Functions](overview.md) on AEM as a Cloud Service.  

This tutorial walks through the steps from installing the Adobe CLI and AEM Edge Functions plugin, to creating a project from the boilerplate template, to deploying a working endpoint.

This tutorial uses the [WKND Sites project](https://github.com/adobe/aem-guides-wknd) as the demo site and Rapid Development Environment (RDE) for deployment. You can follow the same steps with your own site and environment.

The high-level steps:

1. Install Adobe CLI and AEM Edge Functions plugin
1. Set up AEM Edge Functions on your AEM as a Cloud Service environment
1. Create the AEM Edge Functions project from the boilerplate template
1. Clone, review, and run the AEM Edge Functions project locally
1. Review, manage, and deploy CDN configuration
1. Build and deploy AEM Edge Functions to Adobe CDN
1. Verify the endpoint is working

## Before you begin

This tutorial assumes the WKND site (or your own site) is already deployed to an RDE or Development environment.

>[!BEGINTABS]

>[!TAB RDE]

For RDE environments, run the following commands to set up and deploy the site to the RDE:

- From the root of the WKND or your own site project, run the following commands to set up and deploy the site to the RDE:

```bash
# Set up the RDE 
$ aio aem:rde:setup

# Build the site
$ mvn clean install
$ aio aem:rde:install all/target/aem-guides-wknd.all-X.Y.Z-SNAPSHOT.zip
$ aio aem:rde:install dispatcher/target/aem-guides-wknd.dispatcher.cloud-X.Y.Z-SNAPSHOT.zip

# Verify the RDE and site are deployed
$ aio aem:rde:status
```

- In the browser, verify the site is accessible at `https://publish-pXXXXX-eYYYYY.adobeaemcloud.com/`.

For a complete walkthrough, see [Rapid Development Environment](../developing/rde/overview.md).

>[!TAB Dev environment]

- Deploy WKND or your own site to the Dev environment using the Full Stack pipeline in Cloud Manager.

- In the browser, verify the site is accessible at `https://publish-pXXXXX-eYYYYY.adobeaemcloud.com/`.

For a complete walkthrough, see [Full-stack pipelines](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/cicd-pipelines/introduction-ci-cd-pipelines#full-stack-pipeline).

>[!ENDTABS]

## Prerequisites

Ensure the following are in place before starting.

- [Node.js](https://nodejs.org/) and npm installed locally
- A GitHub account to create a project from the boilerplate template
- Access to an AEM as a Cloud Service environment with **Cloud Manager** Deployment Manager role, or **AEM Administrator** Product Profile on the author instance

>[!NOTE]
>
>AEM as a Cloud Service supports **one AEM Edge Function per environment**. Plan accordingly if you intend to use multiple services.

## Step 1: Install Adobe CLI and AEM Edge Functions plugin

Install or update the Adobe `aio` [CLI](https://github.com/adobe/aio-cli), the AEM Edge Functions and RDE plugins.

>[!BEGINTABS]

>[!TAB Fresh install]

For a fresh install, run the following commands:

```bash
# Install the Adobe CLI
$ npm install -g @adobe/aio-cli

# Install the AEM Edge Functions plugin
$ aio plugins install @adobe/aio-cli-plugin-aem-edge-functions

# Install the RDE plugin if you are using an RDE environment
$ aio plugins install @adobe/aio-cli-plugin-aem-rde
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

For example, the output should look like the following screenshot:

![CLI version output](./assets/setup/aemcs/aio-cli-version.png)

## Step 2: Set up AEM Edge Functions on your AEM as a Cloud Service environment

Run the following command from the root of the WKND (or your own) AEM project:

```bash
$ aio aem edge-functions setup
```

If you are not already logged in, the command opens an IMS browser login first.

The command prompts for program, environment, site type, and ADC project config details.

![AEM Edge Functions setup prompts](./assets/setup/aemcs/aio-aem-edge-functions-setup-prompts.png)

Use the following command to view the AEM Edge Functions setup details:

```bash
$ aio aem edge-functions info
```

The output should look like the following screenshot:

![AEM Edge Functions info output](./assets/setup/aemcs/aio-aem-edge-functions-info-output.png)

## Step 3: Create the AEM Edge Functions project from the boilerplate template

Create the AEM Edge Functions project from the [aem-edge-functions-boilerplate](https://github.com/adobe/aem-edge-functions-boilerplate) GitHub template. The boilerplate includes the files and configuration you need to get started.

1. Navigate to [aem-edge-functions-boilerplate](https://github.com/adobe/aem-edge-functions-boilerplate) on GitHub.

1. In the top-right corner, select **Use this template** > **Create a new repository**.

    ![AEM Edge Functions use this template option](./assets/setup/aemcs/github-use-this-template.png)

1. Provide the repository name (for example, `wknd-edge-functions`), add a description, set visibility to **Private**, and select **Create repository**.

    ![AEM Edge Functions create repository details](./assets/setup/aemcs/github-create-repository-details.png)

## Step 4: Clone, review, and run the AEM Edge Functions project locally

### Clone the AEM Edge Functions project

Clone the repository you created in Step 3, then open it alongside the WKND (or your own) project in your IDE. Most editors support workspaces or multi-root views that let you work in both projects at the same time.

```bash
# Clone the repository
$ git clone https://github.com/<your-org>/<your-project-name>.git
```

For example, open the WKND and WKND Edge Functions projects in a single IDE workspace:

![Both WKND and WKND Edge Functions projects as workspace in IDE](./assets/setup/aemcs/ide-workspace-with-both-projects.png)

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

1. `fastly.toml` configures the local development server. For more information, see the [Fastly.toml reference](https://www.fastly.com/documentation/reference/compute/fastly-toml/).

1. `config/` contains the config files for the AEM Edge Function service and CDN routing rules. Deploy these files to your AEM as a Cloud Service environment using the Cloud Manager config pipeline. Step 5 covers that process.

Review the remaining project files to understand the full setup.

### Run the AEM Edge Functions project locally

From the Edge Functions project directory, install dependencies and start the local development server:

```bash
# Navigate to the project directory (replace with your project name)
$ cd wknd-edge-functions

# Install dependencies
$ npm install

# Start the local development server
$ aio aem edge-functions serve
```

The server starts at `http://127.0.0.1:7676`. 

For example, the output should look like the following screenshot:

![Local development server output](./assets/setup/aemcs/local-development-server-output.png)

## Step 5: Review, manage, and deploy CDN configuration

### Review CDN configuration

Review the config files in the `config/` directory of the WKND (or your own) AEM Edge Functions project.

1. `config/edgeFunctions.yaml` declares the AEM Edge Function service. For example, the following code is from the WKND Edge Functions project:

```yaml
kind: "EdgeFunctions"
version: "1"
data:
  functions:
    - name: my-edge-function
```

For more information on supported properties, see [edgeFunctions.yaml reference](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/edge-functions#declare-functions).

1. `config/cdn.yaml` declares the CDN routing rules that direct traffic to the AEM Edge Function service. For example, the following code is from the WKND Edge Functions project:

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

For more information, see [Origin selectors](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn-configuring-traffic#origin-selectors).

The `cdn.yaml` file also supports traffic filter rules, request and response transformation, and other CDN features. For more information, see [Configuring traffic at the CDN](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn-configuring-traffic#initial-setup).

### Manage CDN configuration

Copy the CDN configuration from your Edge Functions project into your AEM site project. Without this configuration, you cannot deploy AEM Edge Functions code to Adobe CDN.

Do not deploy the configuration from the Edge Functions project directly. Instead, copy the files into the **WKND (or your own) AEM project's** `config/` directory. This keeps all CDN configuration, including any existing WAF or traffic filter rules, in one place.

Copy the `edgeFunctions.yaml` from the **Edge Functions** project to the **WKND (or your own) AEM project's** `config/` directory. 

Then merge the `originSelectors` section from the **Edge Functions** project's `cdn.yaml` file into the **WKND (or your own) AEM project's** `cdn.yaml` file.

For example, the CDN config files in the WKND project look like this:

![CDN config files in WKND project](./assets/setup/aemcs/wknd-cdn-config-files.png)

### Deploy CDN configuration

Finally, deploy the CDN configuration to your AEM as a Cloud Service environment.

>[!BEGINTABS]

>[!TAB RDE]

For RDE environments, run the following command from the root of the WKND (or your own) AEM project:

```bash
# Navigate to the AEM project directory (replace with your project name)
$ cd aem-guides-wknd

# Deploy the CDN configuration
$ aio aem:rde:install -t env-config ./config
```

>[!TAB Dev environment]

For Dev environments, commit the config files and run the config pipeline in Cloud Manager:

- Commit and push the config files to the Cloud Manager Git repository.

- Navigate to **Pipelines** in Cloud Manager and run the config pipeline for your environment.

![Cloud Manager config pipeline run](./assets/setup/aemcs/cloud-manager-config-pipeline-run.png)

>[!ENDTABS]

Verify the configuration was deployed successfully:

```bash
$ aio aem edge-functions list
```

The output should list `my-edge-function` (or whatever name you declared in `edgeFunctions.yaml`).

![AEM Edge Functions list output](./assets/setup/aemcs/aio-aem-edge-functions-list.png)

## Step 6: Build and deploy AEM Edge Functions to Adobe CDN

Build and deploy the Edge Functions project from the project root:

```bash
# Navigate to the Edge Functions project directory (replace with your project name)
$ cd wknd-edge-functions

# Build the project
$ aio aem edge-functions build

# Deploy to Adobe CDN
$ aio aem edge-functions deploy my-edge-function
```

The name passed to `deploy` must match the `name` declared in `config/edgeFunctions.yaml`.

For example, the output should look like the following screenshot:

![AEM Edge Functions build and deploy output](./assets/setup/aemcs/aio-aem-edge-functions-build-and-deploy.png)

## Step 7: Verify the endpoint is working

Verify the deployed endpoints in a browser or with curl:

```bash
curl https://edgefunction-pXXXXX-eYYYYY-my-edge-function.adobeaemcloud.com/hello-world
curl https://edgefunction-pXXXXX-eYYYYY-my-edge-function.adobeaemcloud.com/weather
```

Replace `pXXXXX` and `eYYYYY` with your Cloud Manager program and environment IDs.

For example, the responses look like the following screenshot:

![Live endpoint responses](./assets/setup/aemcs/live-endpoint-responses.png)

>[!NOTE]
>
>The `edgefunction-pXXXXX-eYYYYY-<edge-function-name>.adobeaemcloud.com` domain is available for debugging only and is not guaranteed to be stable. In production, requests reach the AEM Edge Function through your site's domain via the CDN routing rules in `cdn.yaml`.

## Next steps

With AEM Edge Functions deployed and routing confirmed, proceed to the use cases:

<!-- 
CARDS
{target = _self}

* ./use-cases/geolocation-based-personalization.md
  {title = Geolocation-based personalization}
  {description = Serve locale-specific content at the edge using CDN geo signals.}
  {image = ./assets/use-cases/use-case.png}
  {cta = Learn more}
* ./use-cases/api-aggregation-with-secrets.md
  {title = API aggregation with secrets}
  {description = Fan out to multiple backends using server-side secrets and return a combined response.}
  {image = ./assets/use-cases/use-case.png}
  {cta = Learn more}
* ./use-cases/kv-store-feature-flags.md
  {title = Feature flags with KV store}
  {description = Toggle feature flags at the edge using the runtime KV store.}
  {image = ./assets/use-cases/use-case.png}
  {cta = Learn more}
-->
<!-- START CARDS HTML - DO NOT MODIFY BY HAND -->
<div class="columns">
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Geolocation-based personalization">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="./use-cases/geolocation-based-personalization.md" title="Geolocation-based personalization" target="_self" rel="referrer">
                        <img class="is-bordered-r-small" src="./assets/use-cases/use-case.png" alt="Geolocation-based personalization"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="./use-cases/geolocation-based-personalization.md" target="_self" rel="referrer" title="Geolocation-based personalization">Geolocation-based personalization</a>
                    </p>
                    <p class="is-size-6">Serve locale-specific content at the edge using CDN geo signals.</p>
                </div>
                <a href="./use-cases/geolocation-based-personalization.md" target="_self" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Learn more</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="API aggregation with secrets">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="./use-cases/api-aggregation-with-secrets.md" title="API aggregation with secrets" target="_self" rel="referrer">
                        <img class="is-bordered-r-small" src="./assets/use-cases/use-case.png" alt="API aggregation with secrets"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="./use-cases/api-aggregation-with-secrets.md" target="_self" rel="referrer" title="API aggregation with secrets">API aggregation with secrets</a>
                    </p>
                    <p class="is-size-6">Fan out to multiple backends using server-side secrets and return a combined response.</p>
                </div>
                <a href="./use-cases/api-aggregation-with-secrets.md" target="_self" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Learn more</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Feature flags with KV store">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="./use-cases/kv-store-feature-flags.md" title="Feature flags with KV store" target="_self" rel="referrer">
                        <img class="is-bordered-r-small" src="./assets/use-cases/use-case.png" alt="Feature flags with KV store"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="./use-cases/kv-store-feature-flags.md" target="_self" rel="referrer" title="Feature flags with KV store">Feature flags with KV store</a>
                    </p>
                    <p class="is-size-6">Toggle feature flags at the edge using the runtime KV store.</p>
                </div>
                <a href="./use-cases/kv-store-feature-flags.md" target="_self" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Learn more</span>
                </a>
            </div>
        </div>
    </div>
</div>
<!-- END CARDS HTML - DO NOT MODIFY BY HAND -->
