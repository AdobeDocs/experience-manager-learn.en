---
title: Search and analyze AEM content with natural language
description: Learn how to search and analyze AEM Content AI sources in natural language from Adobe CX Coworker, without writing low-level API code or navigating the UI.
version: Experience Manager as a Cloud Service
role: Leader, User, Developer
level: Beginner
doc-type: tutorial
duration: null
---
# Search and analyze AEM content with natural language

Use the **Content AI MCP Server** (a companion to the [AEM MCP Server](./overview.md)) from [Adobe CX Coworker](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/ai-in-aem/using-mcp-with-aem-as-a-cloud-service) to search and analyze Content AI sources in natural language, without writing low-level API code or navigating the UI.

In this tutorial you _discover_ available sources, run _keyword_, _semantic_, and _hybrid_ searches, and use _natural language search_ to express complex intent, all from Adobe CX Coworker against a Content AI source.

## Tools and access

The Content AI MCP Server provides six tools:

| Tool | Purpose |
| ---- | ------- |
| `list_indexes` | Discover available indexes in your AEM environment. |
| `get_index_config` | Inspect the raw index configuration and metadata. |
| `fulltext_search` | Keyword-based search with fuzzy matching and field selection. |
| `semantic_search` | Vector-based similarity search for conceptual queries. |
| `hybrid_search` | Combined keyword + semantic search for the best general-purpose recall. |
| `natural_language_search` | Express intent in plain English; the server translates it into structured filters, ranges, and semantics. |

The Content AI MCP Server is **public-source-only**: the `X-Api-Key` header grants source access. An API key is required; a request without it is rejected.

>[!IMPORTANT]
>
> Any signed-in Adobe identity or OAuth/IMS bearer token used to authenticate your MCP session is **never forwarded** to Content AI and has no effect on which sources you can search. Only public, read-only sources are searchable through this server, regardless of your signed-in identity's other entitlements.

## Add the Content AI MCP Server

Connect [Adobe CX Coworker](https://ao.adobe.io/#) to the Content AI MCP Server and run the scenario below.

Let's set up the Content AI MCP Server in Adobe CX Coworker with these steps.

1. Sign in to Adobe CX Coworker.
    <!-- SCREENSHOT: Adobe CX Coworker sign-in / home -->
    ![Adobe CX Coworker Sign In](../assets/content-ai-mcp-server/cx-coworker-signin.png){zoomable="yes"}

1. From the side rail, click **MCP Servers**.
    <!-- SCREENSHOT: MCP Servers in the CX Coworker side rail -->
    ![MCP Servers Side Rail](../assets/content-ai-mcp-server/cx-coworker-mcp-servers-side-rail.png){zoomable="yes"}

1. Click **Add MCP Server**.
    <!-- SCREENSHOT: Add MCP Server button -->
    ![Add MCP Server](../assets/content-ai-mcp-server/cx-coworker-add-mcp-server.png){zoomable="yes"}

1. In the **Add MCP Server** dialog, enter the following details:

    | Field | Value |
    | ----- | ----- |
    | **Server name** | `content-ai-mcp` |
    | **MCP URL** | `https://mcp.adobeaemcloud.com/adobe/experimental/aemagents-expires-20260331/mcp/content-ai` |
    | **Connection type** | `HTTP` |
    | **Authentication type** | `Passthrough` |

    <!-- SCREENSHOT: Add MCP Server dialog with server name, URL, connection type, and authentication type -->
    ![Add MCP Server Dialog](../assets/content-ai-mcp-server/cx-coworker-add-mcp-server-dialog.png){zoomable="yes"}

    >[!NOTE]
    >
    > **Authentication type** is set to `Passthrough` so CX Coworker forwards your signed-in Adobe identity to the MCP Server. This identity is not used for Content AI source access (see [Tools and access](#tools-and-access)), so you do not need a separate sign-in or OAuth step for search itself.

1. Click **Add headers** and add:

    | Header | Value |
    | ------ | ----- |
    | `X-Api-Key` | Your Content AI API key. Required — searches are rejected without it. |
    | `x-content-ai-mcp-routing` | _(Optional)_ Environment/routing info, for example `tier=publish,bucket=p12345-e67890,cluster=ethos21-prod-va7,namespace=ns-team-example`. |

    >[!NOTE]
    >
    > If you do not set the `x-content-ai-mcp-routing` header, the server asks for your environment (`tier` and `bucket`) in chat the first time you run a tool, then retries automatically.
    >
    > `natural_language_search` needs more than the other five tools: it requires **`cluster`** and **`namespace`** in routing, in addition to `tier` and `bucket`. If either is missing, the tool returns a `missing_nls_routing` error — reply with the missing value(s) and the server retries automatically.

1. Click **Add**. The **content-ai-mcp** server now appears in your list of MCP Servers.
    <!-- SCREENSHOT: content-ai-mcp listed in MCP Servers -->
    ![Content AI MCP Server Listed](../assets/content-ai-mcp-server/cx-coworker-content-ai-mcp-listed.png){zoomable="yes"}

1. Click **New chat** to start using the Content AI MCP Server.
    <!-- SCREENSHOT: New chat with Content AI MCP Server -->
    ![New Chat](../assets/content-ai-mcp-server/cx-coworker-new-chat.png){zoomable="yes"}

## Searching public sources

Content AI sources exposed through this server are **public**: read-only, and intended for openly available, non-sensitive content. Anyone with a valid API key can search them.

Use this server when:

- You want to search openly available content (for example, public documentation or a demo catalog).
- You do not need per-user, permission-scoped results.
- You want a simple setup that only requires an API key.

With the server connected as described in [Add the Content AI MCP Server](#add-the-content-ai-mcp-server), discover and search sources directly from chat.

1. In CX Coworker, open a new chat and list the sources available to your API key:

    ```text
    List all Content AI sources available in my environment.
    ```

    The server returns the public sources matching your routing/environment.

## Congratulations!

You set up the Content AI MCP Server in Adobe CX Coworker and used it to search Content AI sources. You discovered available sources and searched them in natural language, with keyword, semantic, hybrid, and natural language search. You also learned that this server searches **public sources only** via an API key, and how to reduce response size with field selection. You can use the same simple approach from CX Coworker to search and analyze Content AI sources without switching to a UI or writing low-level search API code.
