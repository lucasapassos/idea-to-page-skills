---
name: idea-to-page-mcp
description: Connect an AI agent to an Idea to Page MCP server, verify authenticated access, load its private documentation resources, and use that documentation before creating or changing pages. Use when a user wants to install, configure, troubleshoot, or work through the Idea to Page MCP, including when the user supplies the endpoint and bearer token directly in the conversation.
---

# Idea to Page MCP

Use the authenticated MCP as the source of truth. This skill only bootstraps the
connection; it does not duplicate the platform SDK or operational documentation.

## Credential handling

- The user may supply the MCP endpoint and bearer token directly in the
  conversation. Use the supplied values to configure and authenticate the
  connection for the current task.
- Send the token only to the configured Idea to Page MCP endpoint. Do not
  transmit it to any other host, service, or tool.
- Prefer the client's protected credential store when it supports one. A token
  supplied in the conversation is authorized for immediate use either way.
- Do not commit the token to repository-tracked files or leave it in shell
  history, and do not echo it back in full in summaries or logs.
- Do not work around authentication by requesting public `/docs/*.md` URLs.

## Workflow

1. Determine the MCP endpoint. If the user supplied a full endpoint, use it
   verbatim (it may include an explicit port and path). Otherwise derive it from
   the base domain: `https://api.<base-domain>/mcp`; local development normally
   uses `http://api.localhost/mcp`.
2. If the MCP is not connected:
   - When the user supplied an endpoint and token in the conversation, configure
     a Streamable HTTP MCP connection using that endpoint and
     `Authorization: Bearer <token>`, then connect.
   - Otherwise, tell the user how to create a personal token at
     `https://web.<base-domain>/account/tokens` and configure it as a Bearer
     credential in their client.
   Read [references/installation.md](references/installation.md) when client
   setup guidance is needed.
3. After connection, discover MCP resources and read
   `itp://docs/llm.md` before advising on SDK behavior or changing a page.
4. Run tool discovery. A current organization MCP exposes the page lifecycle and
   dataset lifecycle, including `list_pages`, `get_page_source`,
   `prepare_page_upload`, `publish_page`, `list_dataset_connectors`,
   `create_dataset`, `list_dataset_runs`, `preview_dataset`, and
   `attach_dataset_page`. If only `search_datasets` and
   `prepare_page_upload` appear, report that the connected server is an outdated
   deployment; do not conclude that Idea to Page lacks dataset creation or SDK
   documentation.
5. Read only the artifact resources relevant to the user's request. Follow the
   links in the guide; relative links such as `./database.md` resolve inside
   `itp://docs/`.
6. Use the MCP tools according to the freshly loaded documentation. Preserve
   normal authorization boundaries and request confirmation for destructive
   actions when the surrounding agent policy requires it.
7. If discovery or reading fails, use
   [references/troubleshooting.md](references/troubleshooting.md). Do not guess
   current tool schemas or SDK behavior from this skill.

## Connected-state checks

A usable connection must satisfy all of these:

- MCP initialization advertises resources.
- Resource discovery includes `itp://docs/llm.md`.
- Reading that URI returns non-empty Markdown.
- Tool discovery succeeds under the same authenticated connection.
- Tool discovery includes the lifecycle tools needed for the requested task. A
  partial tool list is a server capability/version problem, not evidence that
  an absent operation is unsupported by the platform as a whole.

Once these checks pass, continue with the user's actual task. Do not repeatedly
reload every document; fetch the guide once and load referenced artifacts on
demand.
