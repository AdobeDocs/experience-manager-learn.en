---
title: AI-assisted development
description: Learn about AI-assisted development that uses an AI-powered IDE or coding agents along with AGENTS.md, Agent Skills, and MCP servers to help produce high-quality, production-ready code for projects on AEM as a Cloud Service.
version: Experience Manager as a Cloud Service
feature: Developer Tools
role: Developer, Architect
level: Beginner
doc-type: Article
duration: 0
last-substantial-update: 2026-04-24
jira: KT-20899
thumbnail: KT-20899.pngKT-20899
exl-id: 19b7ab0b-2f47-434a-a141-17701f432fac
---
# AI-assisted development

AI-assisted development uses an AI-powered IDE or coding agents along with `AGENTS.md`, Agent Skills, and MCP servers to help produce high-quality, production-ready code for AEM as a Cloud Service projects.

Tools such as [Cursor](https://www.cursor.com/), [GitHub Copilot in Visual Studio Code](https://code.visualstudio.com/docs/copilot/overview), [Claude Code](https://code.claude.com/docs/en/overview), and similar AI-powered IDEs and coding agents help in a few key ways:

- **Faster iteration**: generate or refactor code from natural language prompts that describe the desired feature or change.
- **Learning aid**: explain unfamiliar code paths, configuration, concepts, or best practices when prompted.

However, these benefits depend heavily on the _context available to the coding agent_. Generic training data and a single repository snapshot are often _not sufficient_ to reliably produce production-ready AEM code.

## Why AI alone is insufficient

Without the right context, AI models (via an AI-powered IDE or coding agent) can:

- **Hallucinate APIs or lifecycles**: suggest code or configurations that do not align with AEM as a Cloud Service best practices or latest features.
- **Miss procedural steps**: omit required steps not visible in code repository or training data.
- **Drift from project standards**: ignore established patterns for components, OSGi services, workflows, or Dispatcher configuration.

This gap is where _structured context_ (Agent Skills and AGENTS.md) and _runtime visibility_ (MCP servers) become essential to make AI-assisted development _productive_ and _reliable_.

## How Adobe helps with AI-assisted development

For AEM as a Cloud Service projects, Adobe provides:

- Agent Skills and AGENTS.md via [Adobe Skills for AI Coding Agents](https://github.com/adobe/skills)
- Local MCP servers for the AEM SDK and local Dispatcher via the [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?fulltext=mcp*&1_group.propertyvalues.property=.%2Fjcr%3Acontent%2Fmetadata%2Fdc%3AsoftwareType&1_group.propertyvalues.operation=equals&1_group.propertyvalues.0_values=software-type%3Atooling&orderby=%40jcr%3Acontent%2Fjcr%3AlastModified&orderby.sort=desc&layout=list&p.offset=0&p.limit=3) portal
- Adobe-hosted AEM MCP servers for content and Cloud Manager workflows from your IDE or chat application — see [MCP Servers in AEM](../mcp/overview.md)

The following sections summarize each item. Use the **Setup** and **Use Cases** sections at the end of this page for installation and walkthroughs for AI-assisted development.

## What are Agent Skills

Agent Skills are _procedural knowledge or expertise_ to help coding agents _perform real work reliably_. For more information, see the [Agent Skills](https://agentskills.io).

For an AEM as a Cloud Service project, Agent Skills are available in the [Adobe Skills for AI Coding Agents](https://github.com/adobe/skills) repository.

## What is AGENTS.md

AGENTS.md provides the _context and instructions_ to help coding agents _work on your project_. For more information, see [AGENTS.md](https://agents.md/).

For an AEM as a Cloud Service project, the `ensure-agents-md` bootstrap skill creates **AGENTS.md** at the repository root **when it is missing**. The skill inspects your project (for example, the root `pom.xml` and modules) and generates tailored guidance instead of using a static file. If **AGENTS.md** already exists, it is **not** overwritten.

After the file exists, you can edit it to add more context and instructions for your team or organization's best practices. The skill may also create **CLAUDE.md** that references **AGENTS.md** so Claude based tools pick up the same guidance.

## What are MCP Servers

MCP servers expose tools and data to the coding agent through the [Model Context Protocol](https://modelcontextprotocol.io/), which supports actions like debugging, inspection, execution, and validation of changes. An MCP server can run on your workstation (**local**) or as a hosted service (**remote**).

For **local development** against the AEM SDK and Dispatcher, install these **local MCP servers** from the [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?fulltext=mcp*&1_group.propertyvalues.property=.%2Fjcr%3Acontent%2Fmetadata%2Fdc%3AsoftwareType&1_group.propertyvalues.operation=equals&1_group.propertyvalues.0_values=software-type%3Atooling&orderby=%40jcr%3Acontent%2Fjcr%3AlastModified&orderby.sort=desc&layout=list&p.offset=0&p.limit=3) portal:

- **AEM Quickstart Local MCP server**: Exposes live runtime data from a local AEM SDK instance to support troubleshooting and development. For more information, see [AEM Quickstart MCP Server](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/ai-in-aem/local-development-with-ai-tools#aem-quickstart-mcp-server).
- **Dispatcher Local MCP server**: Enables runtime validation and inspection of a local Dispatcher instance. For more information, see [Dispatcher MCP Server](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/ai-in-aem/local-development-with-ai-tools#dispatcher-mcp-server).

For Adobe-hosted AEM MCP servers (for example, content, read-only content, and Cloud Manager), see [MCP Servers in AEM](../mcp/overview.md).

## Setup

<!-- 
CARDS
{target = _self}

* ./setup/agent-skills.md
    {title = Set up AEM Agent Skills}
    {description = Learn how to set up AEM Agent Skills for AI-assisted development.}
    {image = ./assets/agent-skills/select-aem-agent-skills-to-install.png}
    {cta = Install AEM Agent Skills}

-->
<!-- START CARDS HTML - DO NOT MODIFY BY HAND -->
<div class="columns">
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Set up AEM Agent Skills">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="./setup/agent-skills.md" title="Set up AEM Agent Skills" target="_self" rel="referrer">
                        <img class="is-bordered-r-small" src="./assets/agent-skills/select-aem-agent-skills-to-install.png" alt="Set up AEM Agent Skills"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="./setup/agent-skills.md" target="_self" rel="referrer" title="Set up AEM Agent Skills">Set up AEM Agent Skills</a>
                    </p>
                    <p class="is-size-6">Learn how to set up AEM Agent Skills for AI-assisted development.</p>
                </div>
                <a href="./setup/agent-skills.md" target="_self" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Install AEM Agent Skills</span>
                </a>
            </div>
        </div>
    </div>
</div>
<!-- END CARDS HTML - DO NOT MODIFY BY HAND -->

## Use Cases

<!-- 
CARDS
{target = _self}

* ./use-cases/component-development.md    
    {title = Create AEM Component with AI-assisted development}
    {description = Learn how to use AI-assisted development to develop AEM components.}
    {image = ./assets/component-development/review-generated-code.png}
    {cta = Create AEM Component}
-->
<!-- START CARDS HTML - DO NOT MODIFY BY HAND -->
<div class="columns">
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Create AEM Component with AI-assisted development">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="./use-cases/component-development.md" title="Create AEM Component with AI-assisted development" target="_self" rel="referrer">
                        <img class="is-bordered-r-small" src="./assets/component-development/review-generated-code.png" alt="Create AEM Component with AI-assisted development"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="./use-cases/component-development.md" target="_self" rel="referrer" title="Create AEM Component with AI-assisted development">Create AEM Component with AI-assisted development</a>
                    </p>
                    <p class="is-size-6">Learn how to use AI-assisted development to develop AEM components.</p>
                </div>
                <a href="./use-cases/component-development.md" target="_self" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Create AEM Component</span>
                </a>
            </div>
        </div>
    </div>
</div>
<!-- END CARDS HTML - DO NOT MODIFY BY HAND -->

## Additional resources

- [Local development with AI Tools](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/ai-in-aem/local-development-with-ai-tools)

- [Adobe Skills for AI Coding Agents](https://github.com/adobe/skills)

- [AGENTS.md](https://agents.md/)

- [Agent Skills](https://agentskills.io/home)
