# Installation and connection

Read this reference only when the Idea to Page MCP has not been configured.

## Install the skill

Install this repository with the skill installation mechanism supported by the
agent client. For Codex, users can request installation from the GitHub
repository path after it is published, selecting:

`skills/idea-to-page-mcp`

Restart or reload the client if it does not discover newly installed skills
automatically.

## Connect the MCP

1. Identify the base domain. If the portal is
   `https://web.example.internal`, the endpoint is
   `https://api.example.internal/mcp`.
2. In the portal, open `/account/tokens` and create a personal MCP token.
3. Configure a Streamable HTTP MCP connection in the client:
   - URL: the endpoint derived above.
   - Authentication: `Authorization: Bearer <token>`.
4. Enter the token only in the client's protected credential field or secret
   store. Do not place it in repository files, shell history, prompts, screenshots,
   issue reports, or shared configuration.
5. Connect, list resources, and read `holter://docs/llm.md`.

Client configuration formats vary. Explain the required URL and Bearer header,
but do not invent product-specific JSON when the client is unknown. Ask which
client the user uses only if its concrete configuration steps are necessary.

## Rotation

If a token is exposed or no longer needed, revoke it in `/account/tokens`,
create a replacement, and update only the client's protected credential.
