# Idea to Page Skills

Public, installable agent skills for working with Idea to Page.

## Available skill

### `idea-to-page-mcp`

Connects an AI agent to an Idea to Page MCP instance, verifies authenticated
resource access, and loads the platform documentation from
`holter://docs/llm.md`.

The repository contains onboarding instructions only. It does not publish the
private SDK documentation or accept credentials.

## Install

Install the skill from this repository path:

`skills/idea-to-page-mcp`

With an agent that supports skill installation from GitHub, provide the
repository URL and the path above. After installation, invoke
`$idea-to-page-mcp` or ask the agent to connect to the Idea to Page MCP.

## Security

- Configure MCP tokens only in the client's protected credential mechanism.
- Never paste a token into an agent conversation.
- Revoke exposed credentials from the Idea to Page token management screen.
- Technical documentation remains available only through the authenticated MCP.

## License

MIT License. See [LICENSE](LICENSE).
