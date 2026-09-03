# Troubleshooting

Read this reference only when installation, authentication, discovery, or
documentation loading fails.

## Endpoint not found

- Confirm the endpoint uses the `api.` host, not `web.`.
- Confirm the path is exactly `/mcp`.
- For local development, use `http://api.localhost/mcp`.
- A public URL such as `web.<domain>/docs/llm.md` is intentionally unavailable.

## 401 Unauthorized

- Confirm the client sends a Bearer credential.
- Ask the user to verify the token in their client configuration; never ask them
  to reveal its value.
- The token may be invalid or revoked. Have the user generate a replacement in
  `web.<domain>/account/tokens`.
- Retry once after the user confirms the credential update. If it still fails,
  stop and report that authentication remains blocked.

## Resources are missing

- Reconnect so the client repeats MCP initialization.
- Confirm initialization advertises a `resources` capability.
- List resources and look for `holter://docs/llm.md`.
- If tools work but resources do not appear, the server or client may predate
  authenticated documentation resources. Report that incompatibility; do not
  substitute guessed documentation.

## Resource unavailable

- Confirm the URI is exact, including `.md`.
- Use resource discovery instead of constructing arbitrary names.
- Do not try filesystem paths, traversal, query strings, fragments, or public
  HTTP equivalents.
- If a listed resource cannot be read, report a server publication problem.

## Connection succeeds but a task fails

Read the relevant artifact referenced by `holter://docs/llm.md` again and use
the current tool schemas from tool discovery. The skill intentionally contains
no copied tool or SDK contract that could drift.
