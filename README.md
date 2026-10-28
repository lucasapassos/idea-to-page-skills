# Idea to Page Skills (archived)

The `idea-to-page-mcp` skill is deprecated and this repository is archived.

Idea to Page agents are now guided by the MCP server itself: `initialize`
returns instructions, `get_started` describes identity, permissions, tools and
limits, `get_docs` serves the documentation, and prompts embed the right tool
order. There is nothing to install.

To connect an assistant, open your organization's **Conectar assistente** page
(`https://<organization>.<domain>/ai`):

- Chat assistants (ChatGPT, Claude.ai) add `https://api.<domain>/mcp` as a
  connector and sign in; no token.
- Coding agents (Codex, Claude Code, Cursor) use a personal token and the
  ready-made prompt from that page.

Existing installations of the skill can be removed safely.

## License

MIT License. See [LICENSE](LICENSE).
