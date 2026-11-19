---
title: Integrate the component into your local AEM project
description: Learn how to integrate and configure a reusable AEM component to display dynamically generated PDF documents directly within AEM pages using the Adobe PDF Embed API. 
type: Documentation
role: Developer
level: Beginner, Intermediate
version: Experience Manager as a Cloud Service
feature: Adaptive Forms
topic: Development
jira: KT-23158
---
# Integrate the component into your local AEM project

This [repository](https://github.com/gbedekar489/aem-forms-pdf-embed) provides reusable source code, not a standalone AEM Maven project. Developers must integrate the relevant files into their existing AEM project and deploy using their own Cloud Manager pipeline.

## Prerequisites

Before beginning, ensure you have:

- An existing AEM as a Cloud Service Maven project.

- Access to the project's core, ui.apps, and ui.config modules.

- Access to the project's Cloud Manager Git repository and deployment pipeline.

- An Adobe PDF Embed API Client ID.

- AEM Forms capabilities enabled for the desired PDF-generation workflow.

- Appropriate access to configure OSGi services and Dispatcher rules.

For Interactive Communications, you also need Adobe IMS OAuth Server-to-Server credentials and the required AEM Forms permissions.

For PDF Data Merge, you need an XDP template available in AEM and the AEM Forms Output Service APIs.

## Clone the GitHub Repository

The complete source code for the Embed PDF component and its supporting AEM Forms services is available in the following GitHub repository:

**[aem-forms-pdf-embed](https://github.com/gbedekar489/aem-forms-pdf-embed)**

To download the source code to your local development environment, follow these steps.

### Step 1: Open a terminal

Open a terminal or command prompt and navigate to the directory where you want to clone the repository.

### Step 2: Clone the repository

Run the following command:

```bash
git clone https://github.com/gbedekar489/aem-forms-pdf-embed.git
```

### Step 3: Navigate to the repository

```bash
cd aem-forms-pdf-embed
```

The repository contains the following directories:

| Directory | Description |
|---|---|
| `ui.apps` | Embed PDF component, authoring dialog, and client library |
| `ui.frontend` | JavaScript and SCSS source files |
| `core` | IC PDF Generation Servlet, PDF Data Merge Servlet, and OAuth Token Service |
| `ui.config` | OSGi configurations for the supporting services |

### Next Steps

After cloning the repository, integrate the required source files into your existing AEM project.

Update the Java package names, servlet paths, and environment-specific configurations to match your AEM environment.

Build and deploy the updated AEM project using your existing Adobe Cloud Manager pipeline.

## Configure OAuth Authentication for Interactive Communications

If you plan to use the Embed PDF component to display PDFs generated through **AEM Forms Interactive Communications (IC)**, you must configure OAuth Server-to-Server authentication.

The sample implementation includes an `OAuthTokenService` that automatically obtains, caches, and renews OAuth access tokens required to invoke the AEM Communications API.

### Step 1: Obtain OAuth Credentials

1. Open the [Adobe Developer Console](https://developer.adobe.com/console).
2. Select the project containing your AEM OAuth Server-to-Server credentials.
3. Locate the following values:
   - **Client ID**
   - **Client Secret**
   - **OAuth Scopes**

### Step 2: Configure Cloud Manager Environment Variables

1. Sign in to Adobe Cloud Manager.
2. Open your AEM program.
3. Navigate to **Environments** and select the target environment.
4. Open **Environment Variables**.
5. Create the following variables:

| Variable Name | Type | Service |
|---|---|---|
| `IC_OAUTH_CLIENT_ID` | Standard | Publish |
| `IC_OAUTH_SCOPES` | Standard | Publish |
| `IC_OAUTH_CLIENT_SECRET` | Secret | Publish |

Use the OAuth credentials obtained from Adobe Developer Console.

> **Note:** If your IC generation servlet runs on Author instead of Publish, configure these variables for the Author service.

### Step 3: Verify the OSGi Configuration

The GitHub repository includes an example `OAuthTokenService.cfg.json` containing:

```json
{
  "tokenUrl": "https://ims-na1.adobelogin.com/ims/token/v3",
  "clientId": "$[env:IC_OAUTH_CLIENT_ID]",
  "clientSecret": "$[secret:IC_OAUTH_CLIENT_SECRET]",
  "scopes": "$[env:IC_OAUTH_SCOPES]"
}
```

AEM resolves these values from the Cloud Manager environment configuration at runtime.

The `OAuthTokenService` uses these credentials to obtain access tokens from Adobe IMS. Tokens are cached and renewed automatically before expiration.

### Step 4: Allowlist the OAuth Client ID

The OAuth Client ID must be allowlisted in AEM as a Cloud Service before it can invoke the Interactive Communications API.

This configuration is deployed using an **Adobe Cloud Manager Configuration Pipeline**.

#### Create the API Allowlist Configuration

In your existing AEM project's Git repository, create a directory named `config` at the repository root.

Create a file named `api.yaml` inside this directory.

**File location:**

```text
<your-aem-project>/
└── config/
    └── api.yaml
```

Add the following configuration to `api.yaml`:

```yaml
kind: "API"
version: "1"
metadata:
  envTypes:
    - dev
data:
  allowedClientIDs:
    author:
      - "YOUR_OAUTH_CLIENT_ID"
    publish:
      - "YOUR_OAUTH_CLIENT_ID"
```

Replace `YOUR_OAUTH_CLIENT_ID` with the OAuth Client ID from Adobe Developer Console.

The example configuration applies to Development environments and allowlists the Client ID for both Author and Publish.

Adjust `envTypes` and the Author/Publish entries according to your deployment requirements.

#### Deploy the Configuration

1. Commit `config/api.yaml` to your AEM project's Git repository.
2. Open Adobe Cloud Manager.
3. Navigate to **Pipelines**.
4. Create or edit a Configuration Pipeline.
5. Configure the pipeline with the following settings:

6. | Setting | Value |
|---|---|
| Deployment Type | Targeted Deployment |
| Include | Config |
| Environment | Your target AEM environment |
| Git Repository | Your AEM project repository |
| Git Branch | Branch containing `api.yaml` |
| Code Location | `/config` |


7. Save and run the Configuration Pipeline.
8. Verify that the pipeline completes successfully.

>[!NOTE]
>
>The `api.yaml` file must be placed in the directory specified by the Configuration Pipeline's **Code Location**. If the file is stored at the repository root under `config/api.yaml`, set Code Location to `/config`.

After successful deployment, the configured OAuth Client ID is allowlisted for the specified AEM service tiers.

The technical account associated with the OAuth credentials must also have the permissions required to invoke the AEM Communications API.

>[!NOTE]
>
>The API allowlist configuration is separate from the OSGi configuration files under `ui.config`. It is deployed through a Configuration Pipeline rather than the Full Stack pipeline.


### Step 5: Configure the AEM Communications API Endpoint

Update `IcPdfGenerationServlet.cfg.json` with the URL of your AEM environment:

```json
{
  "apiBaseUrl": "https://YOUR_AEM_PUBLISH_HOST"
}
```

Replace `YOUR_AEM_PUBLISH_HOST` with the hostname of your AEM Publish environment.

Ensure that the servlet's outbound hostname validation permits only your explicitly trusted AEM environment.

## Configure Dispatcher for PDF Generation Endpoints

If the Embed PDF component is used on a published AEM page or Adaptive Form, ensure that the Dispatcher configuration permits HTTP POST requests to the PDF-generation servlet endpoints.

The sample implementation uses the following endpoints:

```text
/bin/aem-forms-pdf-embed/generate-ic-pdf
/bin/aem-forms-pdf-embed/merge-pdf
```

Add narrowly scoped allow rules to the appropriate Dispatcher filter configuration if these endpoints are not already permitted.

For example:

```apache
/0205 {
    /type "allow"
    /method "POST"
    /url "/bin/aem-forms-pdf-embed/generate-ic-pdf"
}

/0206 {
    /type "allow"
    /method "POST"
    /url "/bin/aem-forms-pdf-embed/merge-pdf"
}
```

Use rule identifiers appropriate to your existing Dispatcher configuration.

Deploy the Dispatcher changes through your AEM Cloud Manager pipeline.

> **Security:** Dispatcher rules control whether requests can reach the servlet. They do not provide user authentication or document-level authorization. Ensure that the PDF-generation servlets enforce the required access controls before allowing requests from publicly accessible pages.

### Important Considerations

- Never store OAuth Client Secrets or access tokens directly in Java source code or GitHub.
- Store sensitive credentials using Cloud Manager secrets.
- Ensure the OAuth Client ID matches the credentials configured in Adobe Developer Console and the deployed API allowlist.
- The `OAuthTokenService` handles access-token acquisition, caching, and proactive renewal automatically.
- Ensure the technical account has the required AEM Forms permissions.
- Protect the IC generation servlet with appropriate authorization controls, particularly when serving customer-specific documents on anonymous Publish pages.

>[!NOTE]
>
>OAuth configuration is required only for the Interactive Communications integration included in this sample. It is not required for the PDF Data Merge example that uses AEM Forms Output Service.
