---
title: Component development using AEM Agent Skills
description: Learn how to develop an AEM component using AEM Agent Skills as part of AI-assisted development.
version: Experience Manager as a Cloud Service
feature: Developer Tools
role: Developer, Architect
level: Beginner
doc-type: Article
duration: 0
last-substantial-update: 2026-04-24
jira: KT-20901
thumbnail: KT-20901.png
exl-id: bd9b74e8-81ab-4d42-bd0a-5443248b5770
---
# Component development using AEM Agent Skills

Learn how to develop an AEM component using AEM Agent Skills as part of [AI-assisted development](../overview.md).

In this walkthrough, you use natural language in an AI-powered IDE (for example, Cursor) to develop a **Promo Banner** component in the [WKND Sites Project](https://github.com/adobe/aem-guides-wknd). The coding agent applies the `create-component` AEM Agent Skill to generate the implementation.

>[!VIDEO](https://video.tv.adobe.com/v/3484952/?learn=on&enablevpops)

## Prerequisites

To follow this tutorial, you need the following:

- An AI-powered IDE such as Cursor, or Visual Studio Code with GitHub Copilot.
- A local clone of the [WKND Sites Project](https://github.com/adobe/aem-guides-wknd), built and deployed to a _local AEM SDK_ instance.
- _AEM Agent Skills_ installed in that project. If you have not done that yet, complete [Setup AEM Agent Skills](../setup/agent-skills.md).

## Component requirement

Let's assume the WKND team wants to display a promo banner on the home page, and the design reference is as follows:

![Promo Banner Design Reference](../assets/component-development/promo-banner-design-reference.png)

Authors must be able to set _Promo label_, _CTA label_, and _CTA link_ fields in the component dialog.

The design reference is a screenshot obtained via wireframe, mockup or static markup capture.

## Develop the component

1. Open the WKND project in your IDE. Confirm that AEM Agent Skills are present (for example, under `.agents/skills`), then start a new agent chat.
    ![Verify AEM Agent Skills are installed](../assets/component-development/verify-aem-agent-skills-installed.png)

1. Enter a prompt like the following. Attach the component design screenshot (obtained via wireframe, mockup or static markup capture) if your IDE supports images in chat:

    ```text
    Create a WKND Promo Banner Component. Please see attached screenshot for design reference.

    Dialog specification are:

    1. Promo Label - Textfield, required
    2. CTA Text - Textfield, required
    3. CTA Link - Pathfield, required
    ```

1. The coding agent uses the `create-component` AEM Agent Skill to generate the component. Review the proposed HTL, Sling Model, dialog XML, and related files.
    ![Review the generated code](../assets/component-development/review-generated-code.png)

>[!TIP]
>
>Instead of providing the design reference as a screenshot, you can also provide a Figma design via the [Figma MCP server](https://www.figma.com/mcp-catalog/) to generate the component. The `create-component` skill supports the [Figma design integration](https://github.com/adobe/skills/blob/main/plugins/aem/cloud-service/skills/create-component/references/figma-design-rules.md)


1. Deploy the component to the local AEM instance/SDK.

    ```shell
    $ mvn clean install -PautoInstallSinglePackage
    ```

1. In authoring, place the Promo Banner on the home page and validate behavior. Refine the implementation if it still diverges from the design reference.
    ![Author the Promo Banner component](../assets/component-development/author-promo-banner-component.png)

1. Review the newly created component by publishing the page or View as Published.
    ![Review the newly created component](../assets/component-development/review-newly-created-component.png)

Congratulations! You have successfully created a new AEM component using AEM Agent Skills as part of AI-assisted development.

## Beyond simple components

This walkthrough uses a simple component. The same `create-component` skill also supports richer cases, including:

- Multifields and nested dialogs fields
- AEM Core Components extensions (including Sling Resource Merger patterns)
- Figma file or frame URLs for layout and styling, when the Figma MCP server (for example `plugin-figma-figma`) is enabled in your IDE

For field types, dialog patterns, Figma rules, and examples, read `SKILL.md` in your installed skill folder, for example, `.agents/skills/create-component/SKILL.md`. 

For an overview, installation paths by IDE, and troubleshooting, see [AEM Component Development Agent](https://github.com/adobe/skills/blob/main/plugins/aem/cloud-service/skills/create-component/README.md) in the Adobe Skills repository.

## AGENTS.md

Before we wrap up, let's understand how AGENTS.md was generated as part of creating the component.

For AEM as a Cloud Service projects, the `ensure-agents-md` bootstrap skill (selected during [Setup AEM Agent Skills](../setup/agent-skills.md)) creates `AGENTS.md` at the repository root when it is **missing**. It uses what it learns from your project layout. 

It does **not** overwrite an existing `AGENTS.md` file.

![AGENTS.md creation](../assets/component-development/agents-md-creation.png)

## Additional resources

- [Local Development with AI Tools](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/ai-in-aem/local-development-with-ai-tools)

- [Adobe Skills for AI Coding Agents](https://github.com/adobe/skills)

- [AGENTS.md](https://agents.md/)

- [Agent Skills](https://agentskills.io/home)
