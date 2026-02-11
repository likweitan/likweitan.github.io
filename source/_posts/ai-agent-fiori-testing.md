---
title: Automated Fiori Unit Testing
date: 2026-02-12 00:02:00
tags:
---

This time let me show you how I automated my unit testing with documentation and screenshots. Objective is to read the functional specification and execute the test cases. In the functional specification, there is test cases that required to be tested and created in a docx format.

Tools needed:
✅ Any AI Agent
✅ MCP: [mcp-abap-adt](https://github.com/mario-andreschak/mcp-abap-adt)
✅ Agent Skills: [abap-skills](https://github.com/likweitan/abap-skills)

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

## Step 3: Install ABAP Skills

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

## Step 4: Add CLAUDE.md

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

## What is Agent Skills? 

Skills basically is a series of instruction or rules that is repetitive check more on https://code.claude.com/docs/en/skills.

The main 2 skills I use are:

sap-fiori-apps-reference
docx

The functional specification is generated from Claude.

{% pdf /FS_Create_Maintenance_Request.pdf %}

### Business Requirement

When a user initiates the creation of a maintenance request (notification type Y1), the system must enforce that the Technical Object field is mandatory. This ensures every Y1 maintenance request is linked to a valid technical object for proper asset tracking and maintenance planning.


{% pdf /test.pdf %}