---
date: "2025-11-18T17:00:50+08:00"
draft: false
title: "Introducing SAP's MCP Servers"
---

Model-driven tooling, like SAP Cloud Application Programming Model, SAP Fiori elements, SAPUI5, and SAP’s mobile development kit, increases developer productivity and supports consistency across [SAP Build](https://www.sap.com/products/technology-platform/build.html) projects. The MCP servers are generally available now. With local MCP servers, SAP now provides new support for code assistants that power developers' preferred agentic development solutions, such as Cursor, Windsurf, Claude Code, and Cline, while maintaining enterprise-grade governance and clean core alignment. These code assistants are generally available now.

### [Cloud Application Programming Model (CAP)](https://community.sap.com/t5/technology-blog-posts-by-sap/boost-your-cap-development-with-ai-introducing-the-mcp-server-for-cap/ba-p/14202849)

https://github.com/cap-js/mcp-server

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

### [SAP Fiori Elements](https://community.sap.com/t5/technology-blog-posts-by-sap/sap-fiori-tools-update-first-release-of-the-sap-fiori-mcp-server-for/ba-p/14204694)

https://github.com/SAP/open-ux-tools

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

### [SAPUI5](https://community.sap.com/t5/technology-blog-posts-by-sap/give-your-ai-agent-some-tools-introducing-the-ui5-mcp-server/ba-p/14200825)

https://github.com/UI5/mcp-server

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

### [SAP Mobile development Kit (MDK)](https://community.sap.com/t5/technology-blog-posts-by-sap/developing-mobile-apps-with-ai-agents-introducing-the-mcp-server-for-mobile/ba-p/14237709)

https://github.com/SAP/mdk-mcp-server

```json
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

Looking ahead, a new ABAP-based MCP server will expose ABAP Cloud development capabilities and ABAP AI capabilities to coding agents. General availability is planned for H1 2026.

## References

https://community.sap.com/t5/technology-blog-posts-by-members/evaluating-sap-s-new-mcp-servers-ui5-cap-and-fiori-tools-in-practice/ba-p/14205611

https://community.sap.com/t5/technology-blog-posts-by-sap/give-your-ai-agent-some-tools-introducing-the-ui5-mcp-server/ba-p/14200825
