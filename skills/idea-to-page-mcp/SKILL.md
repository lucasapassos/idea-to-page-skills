---
name: idea-to-page-mcp
description: Deprecated. Idea to Page agents are guided by the MCP server itself; connect through the organization's "Conectar assistente" page instead of installing this skill.
---

# Idea to Page MCP (deprecated)

This skill is no longer needed and is no longer maintained. The Idea to Page MCP
server now carries everything an agent needs:

- `initialize` returns `instructions` with the recommended flow and rules.
- `get_started` reports your identity, permissions, available tools and limits.
- `get_docs` reads the platform documentation when the client cannot read MCP
  resources (`itp://docs/llm.md` remains the index).
- Prompts (`create_page`, `update_page`, `page_with_data`, `make_page_public`,
  `diagnose_publication`) embed the correct tool order.
- Every error carries `message`, `hint` and `next_tool`.

## How to connect instead

- **Chat assistants (ChatGPT, Claude.ai):** add `https://api.<base-domain>/mcp`
  as a connector and sign in to the organization. No token.
- **Coding agents (Codex, Claude Code, Cursor):** open the organization web app
  at **Conectar assistente** (`/ai`), generate a personal token and paste the
  ready-made prompt into the agent. It configures the Streamable HTTP connection
  with `Authorization: Bearer <token>` and tells the agent to start with
  `get_started`.

If this skill is already installed, you can remove it; nothing depends on it.
