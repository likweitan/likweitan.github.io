---
title: Automated Fiori Unit Testing
date: 2026-02-12 00:02:00
tags: [SAP, MCP, AI, Fiori]
categories: [Technology]
description: "A comprehensive guide to automate unit testing for SAP Fiori applications using an AI agent. The goal is simple: an agent reads a functional specification (Word document), extracts the test cases, executes them against a live system, and generates a comprehensive test report with screenshots."
---

In this post, I'll demonstrate how to **automate unit testing for SAP Fiori applications** using an AI agent. The goal is simple: an agent reads a functional specification (Word document), extracts the test cases, executes them against a live system, and generates a comprehensive test report with screenshots.

### Tools Required

- ✅ **AI Agent**: Claude Code (or similar)
- ✅ **MCP Server**: [mcp-abap-adt](https://github.com/mario-andreschak/mcp-abap-adt) for ABAP connectivity
- ✅ **Agent Skills**: [abap-skills](https://github.com/likweitan/abap-skills) for specialized SAP tasks

## Step 1: Install Claude Code

Claude Code is an agentic coding tool that lives in your terminal. It understands your codebase and helps you code faster through natural language commands.

1. **Prerequisites**: Ensure you have Node.js 18+ installed on your machine.

2. **Install Claude Code** globally using npm:

   ```bash
   npm install -g @anthropic-ai/claude-code
   ```

   You can install other ways [Claude Code overview](https://code.claude.com/docs/en/overview)

3. **Launch Claude Code** by running:

   ```bash
   claude
   ```

4. **Authenticate** with your Anthropic account when prompted. You'll need an active subscription or API access.

5. **Navigate to your project directory** and start coding with Claude!

## Step 2: Install Playwright MCP

Playwright MCP enables browser automation capabilities, allowing Claude to interact with web applications like SAP Fiori for testing purposes.

1. **Add Playwright MCP** to your Claude Code configuration. Use the Claude Code CLI to add the Playwright MCP server:

   ```bash
   claude mcp add playwright npx @playwright/mcp@latest
   ```

2. **Verify installation** by asking Claude to open a browser and navigate to a website.

## Step 3: Install Claude Skills

{% asset_img install_anthropic_skills.png %}

## Step 4: Install ABAP Skills

ABAP Skills provides specialized capabilities for SAP development, including ADT (ABAP Development Tools) integration through the MCP protocol.

1. **Clone the repository**:
   ```bash
   git clone https://github.com/likweitan/abap-skills.git ./.claude
   ```

2. **Add ABAP ADT MCP** to your Claude Code configuration in `~/.claude/claude_desktop_config.json`:
   ```json
   {
     "mcpServers": {
       "mcp-abap-adt": {
         "command": "npx",
         "args": ["-y", "mcp-abap-adt"]
       }
     }
   }
   ```

3. **Configure your SAP connection** by setting environment variables or using the MCP's configuration prompts.

4. **Copy the skills folder** from the cloned repository to your `.claude/skills` directory for enhanced ABAP capabilities.

## Step 5: Add CLAUDE.md

The `CLAUDE.md` file contains project-specific instructions that guide Claude's behavior. Create this file in your project root to define your testing workflow.

```md
# AGENTS.md — SAP Fiori Unit Testing Agent                                          
  ## Role                                                                                                                                                                   
                                                                                                                                                                          
  You are a SAP Fiori testing specialist. You execute manual unit test cases against SAP Fiori applications based on a provided functional specification, capture evidence  
  (screenshots) at each step, and produce a structured test results document.

  ## Workflow

  1. **Read the functional specification** — Use the `docx` skill to open and extract the test cases from the provided specification document. Identify each test case, its
  preconditions, steps, input values, and expected results.

  2. **Resolve app references** — Use the `sap-fiori-apps-reference` skill to look up the target Fiori app(s) referenced in the specification (app ID, URL path, tile name,
  OData services).

  3. **Execute test cases** — Use the `webapp-testing` skill (Playwright) to interact with the Fiori app in the browser:
     - Navigate to the Fiori launchpad and open the target app.
     - For each test case step, perform the described action (click, enter value, select dropdown, etc.).
     - Capture a screenshot after every step.
     - Record the actual result and compare it against the expected result.
     - Mark each test case as **PASS** or **FAIL**.

  4. **Generate the test results document** — Use the `docx` skill to create a Word document containing:
     - **Summary table** — Test case ID, title, status (PASS/FAIL), timestamp.
     - **Detailed results per test case** — Step number, action performed, input values used, expected result, actual result, screenshot, and status.
     - **Overall statistics** — Total cases, passed, failed, pass rate.

  ## Rules

  - Execute every step listed in the specification; do not skip steps or test cases.
  - Always capture a screenshot per step, not just per test case.
  - Record the exact values entered or selected during testing (dates, amounts, dropdown selections, text inputs).
  - If a step fails, continue executing remaining steps in the test case and remaining test cases — do not stop early.
  - If the app is unreachable or login fails, report it immediately and stop.
  - Do not modify the application or its data beyond what the test case prescribes.

  ## Output

  A `.docx` file named `Test_Results_<DOC_ID>_<Date>.docx` with full step-level evidence and a pass/fail summary.

  Key changes from your original:

  - Structured as a numbered workflow so the agent follows a deterministic sequence.
  - Explicit tool-to-task mapping — each skill is tied to a specific phase rather than listed generically.
  - Rules section covers edge cases (what to do on failure, evidence requirements, exact value recording).
  - Defined output format so the deliverable is unambiguous.
  - Removed redundancy — the original repeated the same intent in multiple sentences.

  Adjust the skill names (sap-fiori-apps-reference, webapp-testing, docx) to match whatever is actually registered in your environment.
```

## Understanding Agent Skills

Agent Skills are essentially reusable packages of instructions or tools that extend the agent's capabilities. They handle repetitive tasks or domain-specific logic. You can explore more skills at [Claude Code Skills](https://code.claude.com/docs/en/skills).

### Key Skills Used

**1. sap-fiori-apps-reference**
Resolves Fiori App IDs to technical details like OData services and URL paths.

**2. docx**
Reads and writes Microsoft Word documents, essential for parsing specs and generating reports.

### Business Requirement

When a user initiates the creation of a maintenance request (notification type Y1), the system must enforce that the Technical Object field is mandatory. This ensures every Y1 maintenance request is linked to a valid technical object for proper asset tracking and maintenance planning.

{% pdf /FS_Create_Maintenance_Request.pdf %}

## Demo Walkthrough

### 1. Initialization
We begin in the terminal using Claude Code. After clearing the workspace, we initialize the Model Context Protocol (MCP) to connect our local Playwright environment. We verify the active skills, ensuring the agent has the necessary tools to navigate the file system and execute browser-based tasks.

### 2. Analysis
The agent reads the functional specification `DFS_Create_Maintenance_Request.docx` to extract test cases. It identifies the target application—App ID **F1511A**—and determines the necessary SAP credentials and environment URLs. It then cross-references the AppId with local metadata to ensure the paths are correct.

### 3. Execution

#### Authentication
The agent prompts for the SAP client, language, and Fiori Launchpad URL. Once provided, Claude uses Playwright to launch a headless browser, navigates to the login screen, enters the credentials, and successfully authenticates into the SAP S/4HANA 2023 sandbox.

#### Test Case 001: Positive Validation
The first test verifies that the 'Technical Object' field becomes mandatory when notification type 'Y1' is selected. The agent:
1. Navigates to the 'Create Maintenance Request' app.
2. Selects 'Y1'.
3. Intentionally leaves 'Technical Object' blank to trigger a validation error.
4. Confirms the system blocks the save.
5. Enters a valid object to complete the request.
The notification is successfully created, and screenshots are captured at every step.

#### Test Case 002: Negative Validation & Defect Discovery
Next, we move to TC-MR-002. This is a negative test to ensure the 'Technical Object' field remains optional for other notification types, like 'M1'. However, during execution, the agent discovers a UI inconsistency: **while the field should be optional, the server-side validation is still throwing a mandatory error.** Claude identifies this as a 'Fail' and notes the discrepancy between the visual indicators and the system behavior.

### 4. Results & Reporting
With the execution complete, Claude provides a high-level summary: one 'Pass' and one 'Fail'. The agent highlights the defect found in Case 002. Finally, it compiles these results into a professional Test Results Report, including an executive summary, detailed steps, and automated screenshots.

{% pdf /test.pdf %}