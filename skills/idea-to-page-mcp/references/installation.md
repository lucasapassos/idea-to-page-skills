# Installation and connection

Read this reference only when the Idea to Page MCP has not been configured.

## Install the skill

The recommended cross-agent installer is:

```bash
npx skills add lucasapassos/idea-to-page-skills
```

Select `idea-to-page-mcp` when prompted. For a non-interactive global
installation, use:

```bash
npx skills add lucasapassos/idea-to-page-skills --skill idea-to-page-mcp -g
```

Ask the agent to install:

```text
Install the idea-to-page-mcp skill from
https://github.com/lucasapassos/idea-to-page-skills,
using the path skills/idea-to-page-mcp.
```

For Codex, use `$skill-installer` when explicit skill routing is available.
The installation coordinates are:

- Repository: `https://github.com/lucasapassos/idea-to-page-skills`
- Path: `skills/idea-to-page-mcp`
- Name: `idea-to-page-mcp`

Restart or reload the client if it does not discover newly installed skills
automatically.

## Connect the MCP

The user may send the install and connect request directly, for example:

```text
Install the idea-to-page-mcp skill from
https://github.com/lucasapassos/idea-to-page-skills (path skills/idea-to-page-mcp)
by running:

npx skills add lucasapassos/idea-to-page-skills

Then connect the Idea to Page MCP to your coding agent:

- Endpoint: https://api.example.internal/mcp
- Token: <MCP token — click "Generate quick token">

With the connection active, list the available MCP resources, read
itp://docs/llm.md, and follow the documented guidance before creating or
changing any application.
```

1. Determine the endpoint. If the user supplied a full endpoint, use it verbatim,
   including any explicit port and path. Otherwise derive it from the base domain:
   if the portal is `https://web.example.internal`, the endpoint is
   `https://api.example.internal/mcp`; local development normally uses
   `http://api.localhost/mcp`.
2. Obtain the MCP credential. The user may provide the token directly in the
   conversation; otherwise have them create a personal token in `/account/tokens`.
3. Configure a Streamable HTTP MCP connection in the client:
   - URL: the endpoint from step 1.
   - Authentication: `Authorization: Bearer <token>`.
4. Prefer the client's protected credential field or secret store. If the token
   was supplied in the conversation, it is authorized for immediate use to
   establish the connection. Avoid committing it to repository files or leaving
   it in shell history.
5. Connect, list resources, and read `itp://docs/llm.md`.

Client configuration formats vary. Explain the required URL and Bearer header,
but do not invent product-specific JSON when the client is unknown. Ask which
client the user uses only if its concrete configuration steps are necessary.

## Rotation

If a token is no longer needed or may have been shared more widely than
intended, revoke it in `/account/tokens`, create a replacement, and update the
client's credential.
