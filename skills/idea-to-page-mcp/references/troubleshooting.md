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
- Use the token the user supplied in the conversation when present, or have the
  user verify the token in their client configuration.
- The token may be invalid or revoked. Have the user generate a replacement in
  `web.<domain>/account/tokens`.
- Retry once after the credential is confirmed. If it still fails, stop and
  report that authentication remains blocked.

## Resources are missing

- Reconnect so the client repeats MCP initialization.
- Confirm initialization advertises a `resources` capability.
- List resources and look for `itp://docs/llm.md`.
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

Read the relevant artifact referenced by `itp://docs/llm.md` again and use
the current tool schemas from tool discovery. The skill intentionally contains
no copied tool or SDK contract that could drift.

## Only two tools are visible

If discovery returns only `search_datasets` and `prepare_page_upload`, the client
is connected to the initial organization MCP deployment. A current server also
advertises authenticated documentation resources and page/dataset lifecycle
tools. Reconnect after the server is upgraded and run `initialize`,
`resources/list`, and `tools/list` again. Do not answer that dataset creation or
SDK documentation does not exist based on that partial list.
