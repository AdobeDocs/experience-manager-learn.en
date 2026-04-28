---
title: Set up AEM Agent Skills
description: Learn how to set up AEM Agent Skills for AI-assisted development.
feature: Developer Tools
version: Experience Manager as a Cloud Service
role: Developer
level: Beginner
doc-type: Tutorial
duration: 0
last-substantial-update: 2026-04-24
jira: KT-20900
thumbnail: KT-20900.png
---

# Set up AEM Agent Skills

Learn how to set up AEM Agent Skills for AI-assisted development.

When you ask a coding agent through an AI-powered IDE to work on AEM development tasks, it can use **AEM Agent Skills** procedural guidance from Adobe instead of relying only on generic model training or whatever it can infer from your repository alone.

Adobe provides the AEM Agent Skills via the [Adobe Skills](https://github.com/adobe/skills) repository. Also see the [AI-assisted development](../overview.md) for how Adobe helps with AI-assisted development.

In this tutorial, you install the skills on a local clone of the [WKND Sites Project](https://github.com/adobe/aem-guides-wknd). You can use the same steps for your own AEM as a Cloud Service project.

## Prerequisites

To follow this tutorial, you need the following:

- A local clone of the [WKND Sites Project](https://github.com/adobe/aem-guides-wknd) or your own AEM as a Cloud Service project.
- An AI-powered IDE such as Cursor, or Visual Studio Code with GitHub Copilot.

## Install AEM Agent Skills

Install AEM Agent Skills with the `npx` command (requires [Node.js](https://nodejs.org/) so `npx` is available). For other install options, for example, Claude Code plugins or the GitHub CLI extension, see the [Installation](https://github.com/adobe/skills/tree/main#installation) section in the Adobe Skills repository.

1. Clone the [WKND Sites Project](https://github.com/adobe/aem-guides-wknd) locally:

    ```shell
    $ git clone https://github.com/adobe/aem-guides-wknd.git
    ```

1. Open the cloned project in your AI-powered IDE (for example, Cursor) and open the integrated terminal.
    ![Open the terminal](../assets/agent-skills/wknd-in-cursor-ide-open-terminal.png)

1. Run the following command to add AEM Agent Skills for Cursor:

    ```shell
    $ npx skills add https://github.com/adobe/skills/tree/main/plugins/aem/cloud-service --agent cursor
    ```

    For other agent types, see the [Installation](https://github.com/adobe/skills/tree/main#installation) section in the Adobe Skills repository.

1. When prompted, choose which AEM Agent Skills to install.
    ![Select which AEM Agent Skills to install](../assets/agent-skills/select-aem-agent-skills-to-install.png)

    Select the **ensure-agents-md** skill so the installer can create **AGENTS.md** and **CLAUDE.md** files at the repository root. That bootstrap skill inspects your project, for example, the root `pom.xml` and modules, and generates tailored agent guidance. 
    
    If **AGENTS.md** already exists, it is **not** overwritten.

1. Choose the installation scope. For this walkthrough, the **Project** scope is typical so skill files live in the repo.
    ![Select the installation scope](../assets/agent-skills/select-installation-scope.png)

1. Confirm the install under `.agents/skills`. You should see **SKILLS.md** and related reference and asset folders.
    ![Review the installed skills](../assets/agent-skills/review-installed-skills.png)

1. When Adobe adds or updates skills, use the CLI to add, update, remove, or list them. To see all commands:

    ```shell
    $ npx skills --help
    ```

    ![Review the available skills commands](../assets/agent-skills/review-available-skills-commands.png)

## Use Cases

<!-- 
CARDS
{target = _self}

* ../use-cases/component-development.md    
    {title = Create AEM Component with AI-assisted development}
    {description = Learn how to use AI-assisted development to develop AEM components.}
    {image = ../assets/component-development/review-generated-code.png}
    {cta = Create AEM Component}
-->
<!-- START CARDS HTML - DO NOT MODIFY BY HAND -->
<div class="columns">
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Create AEM Component with AI-assisted development">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="../use-cases/component-development.md" title="Create AEM Component with AI-assisted development" target="_self" rel="referrer">
                        <img class="is-bordered-r-small" src="../assets/component-development/review-generated-code.png" alt="Create AEM Component with AI-assisted development"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="../use-cases/component-development.md" target="_self" rel="referrer" title="Create AEM Component with AI-assisted development">Create AEM Component with AI-assisted development</a>
                    </p>
                    <p class="is-size-6">Learn how to use AI-assisted development to develop AEM components.</p>
                </div>
                <a href="../use-cases/component-development.md" target="_self" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Create AEM Component</span>
                </a>
            </div>
        </div>
    </div>
</div>
<!-- END CARDS HTML - DO NOT MODIFY BY HAND -->

## Additional resources

- [Local Development with AI Tools](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/ai-in-aem/local-development-with-ai-tools)

- [Adobe Skills for AI Coding Agents](https://github.com/adobe/skills)

- [AGENTS.md](https://agents.md/)

- [Agent Skills](https://agentskills.io/home)
