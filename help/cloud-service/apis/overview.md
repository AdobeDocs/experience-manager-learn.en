---
title: AEM APIs overview
description: Learn about the different types of APIs in Adobe Experience Manager (AEM) and get an overview of OpenAPI Specification based APIs, commonly known as OpenAPI-based AEM APIs.
version: Cloud Service
feature: Developing
topic: Development, Architecture, Content Management
role: Architect, Developer, Leader
level: Beginner
doc-type: Article
jira: KT-16515
thumbnail: KT-16515.jpeg
last-substantial-update: 2024-11-20
duration: 0
exl-id: 23b2be0d-a8d4-4521-96ba-78b70f4e9cba
---
# AEM APIs overview{#aem-apis-overview}

Learn about the different types of APIs in Adobe Experience Manager (AEM) as a Cloud Service and get an overview of [OpenAPI Specification (OAS)](https://swagger.io/specification/) based AEM APIs, commonly known as OpenAPI-based AEM APIs.

AEM as a Cloud Service provides a wide range of APIs for creating, reading, updating, and deleting content, assets, and forms. These APIs enable developers to create custom applications that interact with AEM. 

Let's explore the different types of APIs in AEM and understand the key concepts of accessing Adobe APIs.

## Types of AEM APIs{#types-of-aem-apis}

AEM offers both legacy and modern APIs for interacting with its author and publish service types.

- **Legacy APIs**: Introduced in earlier AEM versions, legacy APIs are still supported for backward compatibility.

- **Modern APIs**: Based on the REST, OpenAPI Specification, these APIs follow current API design best practices and are recommended for new integrations.


| AEM API Type | Specifications | Availability |Use Case | Example |
| --- | --- | --- | --- | --- |
| Traditional (Non-RESTful) APIs | Sling Servlets | AEM 6.X, AEM as a Cloud Service | Legacy integrations, backward compatibility | [Query Builder API](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/full-stack/search/query-builder-api) and others |
| RESTful APIs | HTTP, JSON     | AEM 6.X, AEM as a Cloud Service | CRUD operations, modern applications |  [Assets HTTP API](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/admin/mac-api-assets), [Workflow REST API](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/implementing/developing/extending-aem/extending-workflows/workflows-program-interaction#using-the-workflow-rest-api), [JSON Exporter for Content Services](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/full-stack/components-templates/json-exporter) and others |
| GraphQL APIs  |  GraphQL | AEM 6.X, AEM as a Cloud Service | Headless CMS, SPAs, mobile apps | [GraphQL API](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/headless/graphql-api/content-fragments) |
| OpenAPI-based AEM APIs | REST, OpenAPI | **AEM as a Cloud Service only** | API-first development, modern applications | [Assets Author API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/assets/author/), [Folders API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/folders/), [AEM Sites API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/sites/delivery/), [Forms Acrobat Services](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/) and others |

>[!IMPORTANT]
>
>The OpenAPI-based AEM APIs are only available in AEM as a Cloud Service and are not compatible with AEM 6.X. 

For more details on AEM APIs, see the [Adobe Experience Manager as a Cloud Service APIs](https://developer.adobe.com/experience-cloud/experience-manager-apis/).

Let's have a closer look at the OpenAPI-based AEM APIs and the important concepts of accessing Adobe APIs.

## OpenAPI-based AEM APIs{#openapi-based-aem-apis}

>[!AVAILABILITY]
>
>OpenAPI-based AEM APIs are available as part of an early access program. If you are interested in accessing them, we encourage you to email [aem-apis@adobe.com](mailto:aem-apis@adobe.com) with a description of your use case.

The [OpenAPI Specification](https://swagger.io/specification/) (formerly known as Swagger) is a widely used standard for defining RESTful APIs. AEM as a Cloud Service provides several OpenAPI Specification based APIs (or simply OpenAPI-based AEM APIs), making it easier to create custom applications that interact with AEM's author or publish service types. Below are some examples:

**Sites**

- [Sites API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/sites/delivery/): APIs for working with Content Fragments.

**Assets**

- [Folders API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/folders/): APIs for working with folders such as create, list and delete folders.

- [Assets Author API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/assets/author/): APIs for working with assets and its metadata.

**Forms**

- [Forms Acrobat Services](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/): APIs for working with forms and documents.

In future releases, more OpenAPI-based AEM APIs will be added to support additional use cases.

## Authentication support{#authentication-support}

The OpenAPI-based AEM APIs supports the following authentication methods:

- **OAuth Server-to-Server Credential**: Ideal for backend services needing API access without user interaction. It uses the _client_credentials_ grant type, enabling secure access management at the server level. For more information, see [OAuth Server-to-Server credential](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/#oauth-server-to-server-credential).

- **OAuth Web App credential**: Suitable for web applications with frontend and _backend_ components accessing AEM APIs on behalf of users. It uses the _authorization_code_ grant type, where the backend server securely manages secrets and tokens. For more information, see [OAuth Web App credential](https://developer.adobe.com/developer-console/docs/guides/authentication/UserAuthentication/implementation/#oauth-web-app-credential).

- **OAuth Single Page App credential**: Designed for SPAs running in the browser, which needs to access APIs on behalf of a user without a backend server. It uses the _authorization_code_ grant type and relies on client-side security mechanisms using PKCE (Proof Key for Code Exchange) to secure the authorization code flow. For more information, see [OAuth Single Page App credential](https://developer.adobe.com/developer-console/docs/guides/authentication/UserAuthentication/implementation/#oauth-single-page-app-credential).

## Accessing Adobe APIs and related concepts{#accessing-adobe-apis-and-related-concepts}

Before accessing Adobe APIs, it's essential to understand these key concepts:

- **[Adobe Developer Console](https://developer.adobe.com/)**: The developer hub for accessing Adobe APIs, SDKs, real-time events, serverless functions, and more. Note that this is different from the _AEM_ Developer Console, which is used for debugging AEM applications.

- **[Adobe Developer Console Project](https://developer.adobe.com/developer-console/docs/guides/projects/)**: Central place for managing API integrations, events, and runtime functions. Here, you configure APIs, set authentication, and generate required credentials.

- **[Product Profiles](https://helpx.adobe.com/enterprise/using/manage-product-profiles.html)**: Product Profiles provide a permission preset that allows you to control user or application access to Adobe products such as AEM, Adobe Target, Adobe Analytics, and others. Every Adobe product has predefined product profiles associated with it.

- **Services**: Services define the actual permissions and are associated with the Product Profile. To reduce or increase the permissions preset, you can deselect or select the services associated with the Product Profile. Thus, allowing you to control the level of access to the product and its APIs. In AEM as a Cloud Service, services represent user groups with predefined Access Control Lists (ACLs) for repository nodes, allowing granular permission management.

## Next steps{#next-steps}

With an understanding of the different AEM API types, including 
OpenAPI-based AEM APIs, and the key concepts of accessing Adobe APIs, you are now ready to start building custom applications that interact with AEM.

Let's get started with the [How to invoke OpenAPI-based AEM APIs](invoke-openapi-based-aem-apis.md) tutorial.
