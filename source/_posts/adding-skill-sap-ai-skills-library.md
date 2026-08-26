---
title: "Adding Skill to the SAP AI Skills Library"
date: 2026-08-12 21:58:09
tags: [SAP, AI, BTP]
categories: [Technology]
---

# Adding Skill to the SAP AI Skills Library

If you've been building "skills" for AI coding agents — the kind of reusable `SKILL.md` instructions that Claude Code, Copilot, Cursor, and similar tools can pick up — there's now a central place to make them discoverable to the SAP community: [SAP/ai-skills-library](https://github.com/SAP/ai-skills-library), which powers the public catalog at [skills.cloud.sap](https://skills.cloud.sap).

{% asset_img sap-ai-skills.png "SAP AI Skills Library page in VS Code marketplace" %}

## It's a "Bring Your Own Repo" Library

The most important thing to understand before you start: **you don't submit your skill code to the `ai-skills-library` repo at all.** Your skills stay in your own public GitHub repository. The library itself is just a registry — a maintainer reviews your repo and adds a pointer to it so it shows up in the catalog.

That means the whole contribution is really two steps:

1. Make sure your repository is laid out in a way the library can discover.
2. Open a short GitHub issue asking to be registered.

No pull request, no code review against SAP's repo, no build pipeline to satisfy. Let's go through both steps.

## Step 1: Structure Your Repository

Your repo needs a `skills/` folder, with one subfolder per skill, each containing a `SKILL.md` file:

```
your-repo/
└── skills/
    └── <skill-slug>/
        └── SKILL.md      # must include "name" and "description" frontmatter
```

The `SKILL.md` file needs YAML frontmatter with at least a `name` and a `description`:

```yaml
---
name: btp-diagram-generator
description: "Generate SAP BTP (Business Technology Platform) solution architecture diagrams as native draw.io (.drawio) files following the official SAP BTP Solution Diagram guidelines (Fiori Horizon design system) and open them via a configured draw.io MCP server. USE WHEN: user asks to create/draw/design/sketch a BTP diagram, BTP architecture, BTP landscape, BTP solution diagram, BTP reference architecture, SAP Business Technology Platform diagram, or wants to visualize SAP BTP services (CAP, Build, Integration Suite, SAC, AI Core, HANA Cloud, Cloud Foundry, Kyma, Workzone, etc.) and their interdependencies in draw.io / drawio / diagrams.net. DO NOT USE FOR: non-BTP architecture diagrams, generic flowcharts, sequence/UML diagrams, or diagrams that should remain in Mermaid/PlantUML."
---
# BTP Solution Diagram Generator

...skill content...
```

That `description` field isn't just documentation — it's what shows up on the skills.cloud.sap listing, and it's also what drives AI agent trigger-matching (i.e., how an agent decides _when_ to pull this skill into context). Write it the way you'd write a good tool description: specific, and rich with the phrases a user might actually say.

{% asset_img atc-cloudification.png "SAP AI Skills Library page in VS Code marketplace" %}

You can have as many skill folders under `skills/` as you like.

## Step 2: Open a "Register a New Skill" Issue

Once your repo is public and structured correctly, head to:

👉 **[Register skill here](https://github.com/SAP/ai-skills-library/issues/new?template=new-skill.yml)**

{% asset_img github-issue.png "SAP AI Skills Library page in VS Code marketplace" %}

This opens a structured GitHub issue form (not a blank text box) with a few fields:

- **Repository URL** — the public GitHub URL of your skills repo.
- **Skills in this repository** — a list of each skill slug and a one-line description of what it does.
- **Readiness checklist** — a set of checkboxes you self-certify before submitting:
  - The repository is public on github.com
  - Each skill has a `skills/<slug>/SKILL.md` file with `name` and `description` frontmatter
  - Author information is available (e.g. in README or `package.json`)
  - License information is available (e.g. a `LICENSE` file or `package.json`)
- **Additional context** — optional free text for anything else the maintainers should know.

Once submitted, a maintainer reviews the issue and, if everything checks out, onboards your repo — no PR required on your end.

## Example

[ABAP Skills](https://github.com/SAP/ai-skills-library/issues/22) is a good template to model your own submission on. It points to the repository `https://github.com/likweitan/abap-skills` and lists 18 ABAP-focused skills in the exact "slug — description" format the template expects, for example:

- `abap` — Check and improve ABAP code with abaplint and Clean ABAP principles.
- `abap-cloud` — Develop clean-core extensions using released APIs and the ABAP Cloud language model.
- `rap` — Build RAP business objects with behavior definitions, EML, draft, and save handling.
- `clean-abap` — Review ABAP code for compliance with Clean ABAP principles and best practices.
- `abapgit` — Use abapGit for repository setup, branching, serialization, and CI/CD workflows.

Covering everything from OData services to BTP architecture diagram generation. Notice the pattern in each line: **skill slug**, an em dash, then a **short, imperative, trigger-rich description** — exactly the phrasing style the library wants.

All four readiness checklist boxes are ticked, and the issue was accepted and closed after maintainer review — a clean example of the process working as intended.

## Governance Basics to Know Before You Submit

A few housekeeping points from the [CONTRIBUTING.md](https://github.com/SAP/ai-skills-library/blob/main/CONTRIBUTING.md) that are easy to overlook:

- All contributions must be licensed under **Apache 2.0**.
- If you ever open a pull request against the repo (e.g., for a skill improvement), you'll be asked to accept a **Developer Certificate of Origin (DCO)** — handled automatically during submission.
- If you used AI tools to help generate your skill content, it must follow SAP's [guidelines on AI-generated code](https://github.com/SAP/.github/blob/main/CONTRIBUTING_USING_GENAI.md).
- All participants are expected to follow the [SAP Open Source Code of Conduct](https://github.com/SAP/.github/blob/main/CODE_OF_CONDUCT.md).
