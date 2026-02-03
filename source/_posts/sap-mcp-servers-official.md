---
date: 2026-02-03 21:26:31
draft: false
title: "SAP's MCP Servers - Official"
tags: [SAP, MCP, AI, CAP, Fiori, ABAP]
categories: [Technology]
description: "A comprehensive guide to official SAP Model Context Protocol (MCP) servers and the ABAP Accelerator for Amazon Q, illustrating how to configure them for AI-assisted development."
---

If you're new to the Model Context Protocol (MCP), I highly recommend reading the [official introduction](https://modelcontextprotocol.io/docs/getting-started/intro). In short, MCP is an open standard that enables AI agents to securely interact with your local code and data context.

![Model Context Protocol Diagram](https://mintcdn.com/mcp/bEUxYpZqie0DsluH/images/mcp-simple-diagram.png?fit=max&auto=format&n=bEUxYpZqie0DsluH&q=85&s=35268aa0ad50b8c385913810e7604550)

Recognizing this potential, SAP has released several official MCP servers designed to supercharge AI-assisted development for the SAP ecosystem, specifically tailored to the developer's perspective.

# SAP

## Cloud Application Programming Model (CAP)

A Model Context Protocol (MCP) server for the SAP Cloud Application Programming Model (CAP). Use it for AI-assisted development of CAP applications (agentic coding).

> For the best experience we recommend using this server alongside @ui5/mcp-server and @sap-ux/fiori-mcp-server.

### Usage

- Which CDS services are in this project, and where are they served?
- What are the entities about and how do they relate?
- How do I add columns to a select statement in CAP Node.js?

### Rules

Add these rules to your existing global or project-specific `AGENTS.md`.

```
- You MUST search for CDS definitions, like entities, fields and services (which include HTTP endpoints) with cds-mcp, only if it fails you MAY read \*.cds files in the project.
- You MUST search for CAP docs with cds-mcp EVERY TIME you create, modify CDS models or when using APIs or the `cds` CLI from CAP. Do NOT propose, suggest or make any changes without first checking it.
```

### Installation

<details>
<summary><b>Claude Code</b></summary>

Run this command to add the server. See [Claude Code MCP docs](https://docs.anthropic.com/en/docs/claude-code/mcp) for more info.

**Local Server Connection**

```bash
claude mcp add cds-mcp -- npx -y @cap-js/mcp-server
```
</details>
<details>
<summary><b>VS Code</b></summary>

Add this to your VS Code MCP config file. See [VS Code MCP docs](https://code.visualstudio.com/docs/copilot/customization/mcp-servers) for more info.

**Local Server Connection**

```json
{
  "mcpServers": {
    "cds-mcp": {
      "command": "npx",
      "args": ["-y", "@cap-js/mcp-server"],
      "env": {}
    }
  }
}
```
</details>
<details>
<summary><b>OpenCode</b></summary>

Add this to your OpenCode configuration file. See [OpenCode MCP docs](https://opencode.ai/docs/mcp-servers) for more info.

**Local Server Connection**

```json
{
  "mcpServers": {
    "cds-mcp": {
      "command": "npx",
      "args": ["-y", "@cap-js/mcp-server"],
      "env": {}
    }
  }
}
```
</details>
<details>
<summary><b>Cursor</b></summary>

Add this to your Cursor configuration file. See [Cursor MCP docs](https://docs.cursor.com/context/model-context-protocol#installing-mcp-servers) for more info.

**Local Server Connection**

```json
{
  "mcpServers": {
    "cds-mcp": {
      "command": "npx",
      "args": ["-y", "@cap-js/mcp-server"],
      "env": {}
    }
  }
}
```
</details>

[GitHub](https://github.com/cap-js/mcp-server) [NPM](https://www.npmjs.com/package/@cap-js/mcp-server)

## SAP Fiori Elements

The SAP Fiori MCP server enables developers using AI coding assistants to generate and adapt SAP Fiori elements applications with precision and context awareness.

> For the best experience we recommend using this server alongside @cap-js/mcp-server and @ui5/mcp-server.

### Usage

- Please add a SAP Fiori elements list report app to my CAP project
- Generate a new CAP project and SAP Fiori app based on my_picture.png
- Enable initial load for the fiori app

### Rules

Add these rules to your existing global or project-specific `AGENTS.md`.

```
## Rules for creation or modification of SAP Fiori elements apps

- When asked to create an SAP Fiori elements app, check if the user input describes an application with one or more pages containing table data or forms. If so, these can be translated into an SAP Fiori elements application; otherwise, ask the user for more suitable input.
- The application typically starts with a List Report page showing the data of the base entity of the application in a table. Details of a specific table row are shown in the ObjectPage. This first Object Page is therefore based on the base entity of the application.
- An Object Page can contain one or more table sections based on the to-many associations of its entity type. The details of a table section row can be shown in another Object Page based on the association's target entity.
- The data model must be suitable for an SAP Fiori elements frontend application. So there must be one main entity and one or more navigation properties to related entities.
- Each property of an entity must have a proper datatype.
- For all entities in the data model provide primary keys of type UUID.
- When creating sample data in CSV files, all primary keys and foreign keys MUST be in UUID format (e.g., `550e8400-e29b-41d4-a716-446655440001`).
- When generating or modifying the SAP Fiori elements application on top of the CAP service use the Fiori MCP server if available.
- When attempting to modify an SAP Fiori elements application (e.g., adding columns), do not use screen personalization. Instead, modify the project code. First, check if an MCP server provides a suitable function for this task.
- When previewing the SAP Fiori elements application use the most specific `npm run watch-*` script for the app in the `package.json`.
```

### Installation

<details>
<summary><b>Claude Code</b></summary>

Run this command to add the server. See [Claude Code MCP docs](https://docs.anthropic.com/en/docs/claude-code/mcp) for more info.

**Local Server Connection**

```bash
claude mcp add fiori-mcp -- npx --yes @sap-ux/fiori-mcp-server@latest fiori-mcp
```
</details>
<details>
<summary><b>VS Code</b></summary>

Add this to your VS Code MCP config file. See [VS Code MCP docs](https://code.visualstudio.com/docs/copilot/customization/mcp-servers) for more info.

**Local Server Connection**

```json
{
  "mcpServers": {
    "fiori-mcp": {
      "type": "stdio",
      "timeout": 600,
      "command": "npx",
      "args": ["--yes", "@sap-ux/fiori-mcp-server@latest", "fiori-mcp"]
    }
  }
}
```
</details>
<details>
<summary><b>OpenCode</b></summary>

Add this to your OpenCode configuration file. See [OpenCode MCP docs](https://opencode.ai/docs/mcp-servers) for more info.

**Local Server Connection**

```json
{
  "mcp": {
    "fiori-mcp": {
      "type": "local",
      "command": ["npx", "--yes", "@sap-ux/fiori-mcp-server@latest", "fiori-mcp"],
      "enabled": true
    }
  }
}
```
</details>
<details>
<summary><b>Cursor</b></summary>

Add this to your Cursor configuration file. See [Cursor MCP docs](https://docs.cursor.com/context/model-context-protocol#installing-mcp-servers) for more info.

**Local Server Connection**

```json
{
  "mcpServers": {
    "fiori-mcp": {
      "type": "stdio",
      "timeout": 600,
      "command": "npx",
      "args": ["--yes", "@sap-ux/fiori-mcp-server@latest", "fiori-mcp"]
    }
  }
}
```
</details>

[GitHub](https://github.com/SAP/open-ux-tools) [NPM](https://www.npmjs.com/package/@sap-ux/fiori-mcp-server)

## SAPUI5

The UI5 Model Context Protocol server offers tools to improve the developer experience when working with agentic AI tools.

- Helps with the creation of new UI5 projects
- Detects and fixes UI5-specific errors in the code
- Provides additional UI5-specific information

> > For the best experience we recommend using this server alongside @cap-js/mcp-server and @sap-ux/fiori-mcp-server.

### Usage

- Check my UI5 app for deprecated APIs
- Generate a UI5 app with current best practices
- What’s the correct way to implement data binding in UI5?

### Rules

Add these rules to your existing global or project-specific `AGENTS.md`.

```
## Guidelines for UI5

Use the `get_guidelines` tool of the UI5 MCP server to retrieve the latest coding standards and best practices for UI5 development.
```

### Installation

<details>
<summary><b>Claude Code</b></summary>

Run this command to add the server. See [Claude Code MCP docs](https://docs.anthropic.com/en/docs/claude-code/mcp) for more info.

**Local Server Connection**

```bash
claude mcp add ui5-mcp-server -- npx @ui5/mcp-server
```
</details>
<details>
<summary><b>VS Code</b></summary>

Add this to your VS Code MCP config file. See [VS Code MCP docs](https://code.visualstudio.com/docs/copilot/customization/mcp-servers) for more info.

**Local Server Connection**

```json
{
  "mcpServers": {
    "@ui5/mcp-server": {
      "type": "stdio",
      "command": "npx",
      "args": ["@ui5/mcp-server"]
    }
  }
}
```
</details>
<details>
<summary><b>OpenCode</b></summary>

Add this to your OpenCode configuration file. See [OpenCode MCP docs](https://opencode.ai/docs/mcp-servers) for more info.

**Local Server Connection**

```json
{
  "mcp": {
    "@ui5/mcp-server": {
      "type": "local",
      "command": ["npx", "@ui5/mcp-server"],
      "enabled": true
    }
  }
}
```
</details>
<details>
<summary><b>Cursor</b></summary>

Add this to your Cursor configuration file. See [Cursor MCP docs](https://docs.cursor.com/context/model-context-protocol#installing-mcp-servers) for more info.

**Local Server Connection**

> **Note:** Cursor does not support MCP resources. Set the `UI5_MCP_SERVER_RESPONSE_NO_RESOURCES` environment variable to disable resources in the server responses.

```json
{
  "mcpServers": {
    "@ui5/mcp-server": {
      "type": "stdio",
      "command": "npx",
      "args": ["@ui5/mcp-server"],
      "env": {
        "UI5_MCP_SERVER_RESPONSE_NO_RESOURCES": "true"
      }
    }
  }
}
```
</details>

[GitHub](https://github.com/UI5/mcp-server) [NPM](https://www.npmjs.com/package/@ui5/mcp-server)

## SAP Mobile development Kit (MDK)

This open-source server provides AI agents with comprehensive MDK knowledge and tools. By combining best practice guidelines, project-aware context information, templates for creating new projects, and access to the MDK CLI tools, the MDK MCP server transforms AI agents into MDK development experts.

### Usage

- Generate a new MDK project displaying OData entities information.
- Enhance an existing project adding additional UI controls on a given page.
- Validate your current MDK project schema.
- Migrate old MDK projects to latest schema.
- Deploy your MDK project.

### Rules

Add these rules to your existing global or project-specific `AGENTS.md`.

```
- Don't generate `.service.metadata` file.
- Don't generate `.xml` file in the `Services` folder.
- Don't change `.project.json` file.
```

### Installation

<details>
<summary><b>Claude Code</b></summary>

Run this command to add the server. See [Claude Code MCP docs](https://docs.anthropic.com/en/docs/claude-code/mcp) for more info.

**Local Server Connection**

```bash Claude
claude mcp add mdk-mcp -- mdk-mcp --schema-version 25.9
```
</details>
<details>
<summary><b>VS Code</b></summary>

Add this to your VS Code MCP config file. See [VS Code MCP docs](https://code.visualstudio.com/docs/copilot/customization/mcp-servers) for more info.

**Local Server Connection**

```json VS Code
{
  "mcpServers": {
    "mdk-mcp": {
      "type": "stdio",
      "command": "mdk-mcp",
      "args": ["--schema-version", "25.9"]
    }
  }
}
```
</details>
<details>
<summary><b>OpenCode</b></summary>

Add this to your OpenCode configuration file. See [OpenCode MCP docs](https://opencode.ai/docs/mcp-servers) for more info.

**Local Server Connection**

```json
{
  "mcp": {
    "mdk-mcp": {
      "type": "local",
      "command": ["mdk-mcp", "--schema-version", "25.9"],
      "enabled": true
    }
  }
}
```
</details>
<details>
<summary><b>Cursor</b></summary>

Add this to your Cursor configuration file. See [Cursor MCP docs](https://cursor.com/docs/context/mcp#installing-mcp-servers) for more info.

**Local Server Connection**

```json
{
  "mcpServers": {
    "mdk-mcp": {
      "command": "mdk-mcp",
      "args": ["--schema-version", "25.9"]
    }
  }
}
```
</details>

[GitHub](https://github.com/SAP/mdk-mcp-server) [NPM](https://www.npmjs.com/package/@sap/mdk-mcp-server)

# AMAZON

## ABAP Accelerator for Amazon Q Developer

ABAP Accelerator is an MCP server that helps organizations create, test, document, and transform SAP ABAP code faster and with higher code accuracy.

### Usage

- Get source code for class ZCL_TEST from ECC system
- Create a new class in S/4HANA system
- Now check the same class in S/4HANA

<!-- ### Installation

```json
{
  "mcpServers": {
    "abap-accelerator-q": {
      "command": "docker",
      "args": [
        "run", "--rm", "-i", "--platform", "linux/amd64",
        "--mount", "type=bind,source=C:/Users/YourUsername/.secrets/sap,target=/run/secrets,readonly",
        "-e", "SAP_HOST=your-sap-host.company.com",
        "-e", "SAP_CLIENT=100",
        "-e", "SAP_USERNAME=your_username",
        "-e", "SAP_LANGUAGE=EN",
        "-e", "SAP_SECURE=true",
        "abap-accelerator-q-3.2.1-node22",
        "node", "dist/index.js"
      ],
      "timeout": 60000,
      "disabled": false
    }
  }
}
``` -->

[GitHub](https://github.com/aws-solutions-library-samples/guidance-for-deploying-sap-abap-accelerator-for-amazon-q-developer?tab=readme-ov-file#step-6-configure-mcp-for-amazon-q-developer)

# References

- [Boost your CAP development with AI: Introducing the MCP Server for CAP](https://community.sap.com/t5/technology-blog-posts-by-sap/boost-your-cap-development-with-ai-introducing-the-mcp-server-for-cap/ba-p/14202849)
- [SAP Fiori Tools Update: First Release of the SAP Fiori MCP Server for SAP Fiori Elements](https://community.sap.com/t5/technology-blog-posts-by-sap/sap-fiori-tools-update-first-release-of-the-sap-fiori-mcp-server-for/ba-p/14204694)
- [Give your AI Agent some Tools - Introducing the UI5 MCP Server](https://community.sap.com/t5/technology-blog-posts-by-sap/give-your-ai-agent-some-tools-introducing-the-ui5-mcp-server/ba-p/14200825)
- [Developing Mobile Apps with AI Agents: Introducing the MCP Server for Mobile](https://community.sap.com/t5/technology-blog-posts-by-sap/developing-mobile-apps-with-ai-agents-introducing-the-mcp-server-for-mobile/ba-p/14237709)
- [Evaluating SAP's new MCP Servers: UI5, CAP and Fiori Tools in practice](https://community.sap.com/t5/technology-blog-posts-by-members/evaluating-sap-s-new-mcp-servers-ui5-cap-and-fiori-tools-in-practice/ba-p/14205611)
- [Give your AI Agent some Tools - Introducing the UI5 MCP Server](https://community.sap.com/t5/technology-blog-posts-by-sap/give-your-ai-agent-some-tools-introducing-the-ui5-mcp-server/ba-p/14200825)
- [ABAP with Amazon Q Developer](https://medium.com/@warren_eiserman/abap-with-amazon-q-developer-1ed5915f44de)
- [The 7 current MCP servers for SAP you should pin](https://medium.com/@mario.defelipe/the-7-current-mcp-servers-for-sap-you-should-pin-f66449a2feb2)