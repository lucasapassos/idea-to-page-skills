# Idea to Page Skills

Public, installable agent skills for working with Idea to Page.

## Available skill

### `idea-to-page-mcp`

Connects an AI agent to an Idea to Page MCP instance, verifies authenticated
resource access, and loads the platform documentation from
`itp://docs/llm.md`.

The repository contains onboarding instructions only. It does not publish the
private SDK documentation.

## Install

### `npx skills` (recommended)

Works with Claude Code, OpenCode, Codex, Cursor, and 70+ other agents:

```bash
npx skills add lucasapassos/idea-to-page-skills
```

Then select `idea-to-page-mcp` when prompted. To skip the prompts:

```bash
# Project scope, specific agent
npx skills add lucasapassos/idea-to-page-skills --skill idea-to-page-mcp -a claude-code

# Global scope (all projects)
npx skills add lucasapassos/idea-to-page-skills --skill idea-to-page-mcp -g
```

Update later with `npx skills update idea-to-page-mcp`.

### Ask your agent

Send this instruction to an agent that can install skills:

```text
Install the idea-to-page-mcp skill from
https://github.com/lucasapassos/idea-to-page-skills,
using the path skills/idea-to-page-mcp.
```

In Codex, explicitly ask it to use `$skill-installer` for this request.

### Claude Code

Install globally (all projects):

```bash
mkdir -p ~/.claude/skills
git clone https://github.com/lucasapassos/idea-to-page-skills.git /tmp/idea-to-page-skills
cp -r /tmp/idea-to-page-skills/skills/idea-to-page-mcp ~/.claude/skills/
```

Or install for a single project:

```bash
git clone https://github.com/lucasapassos/idea-to-page-skills.git /tmp/idea-to-page-skills
mkdir -p .claude/skills
cp -r /tmp/idea-to-page-skills/skills/idea-to-page-mcp .claude/skills/
```

### Generic agents (`~/.agents/skills/`)

```bash
mkdir -p ~/.agents/skills
git clone https://github.com/lucasapassos/idea-to-page-skills.git /tmp/idea-to-page-skills
cp -r /tmp/idea-to-page-skills/skills/idea-to-page-mcp ~/.agents/skills/
```

### Other agents

If your agent installs skills from a Git repository, point it at
`https://github.com/lucasapassos/idea-to-page-skills.git` with skill path
`skills/idea-to-page-mcp`.

Repository coordinates:

- Repository: `https://github.com/lucasapassos/idea-to-page-skills`
- Skill path: `skills/idea-to-page-mcp`
- Skill name: `idea-to-page-mcp`

### After installing

Invoke `$idea-to-page-mcp`, or simply ask the agent to connect to the Idea to
Page MCP. You may send the endpoint and token directly in the conversation —
see [Security](#security).

## Security

- You may supply the MCP endpoint and token in the conversation; the agent uses
  them to configure the connection.
- The token is sent only to the Idea to Page MCP endpoint, never to other hosts.
- Prefer the client's credential store where available, and avoid committing
  tokens to repository files.
- Revoke exposed credentials from the Idea to Page token management screen.
- Technical documentation remains available only through the authenticated MCP.

## License

MIT License. See [LICENSE](LICENSE).
