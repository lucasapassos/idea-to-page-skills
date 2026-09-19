---
name: idea-to-page-mcp
description: Connect an AI agent to an Idea to Page MCP server, verify authenticated access, load its private documentation resources, and use that documentation before creating or changing pages. Use when a user wants to install, configure, troubleshoot, or work through the Idea to Page MCP. Do not use this skill to solicit, display, store, or transmit the user's bearer token.
---

# Idea to Page MCP

Use the authenticated MCP as the source of truth. This skill only bootstraps the
connection; it does not duplicate the platform SDK or operational documentation.

## Safety boundary

- Never ask the user to paste a bearer token into the conversation.
- Never print, log, commit, or place a token in a command line.
- Have the user configure the token through the MCP client's secret or
  credential mechanism.
- Treat a token as compromised if it appears in chat or output. Stop and direct
  the user to revoke it in Idea to Page before continuing.
- Do not work around authentication by requesting public `/docs/*.md` URLs.

## Workflow

1. Determine the instance base domain from the user's URL or deployment context.
   The MCP endpoint is `https://api.<base-domain>/mcp`; local development
   normally uses `http://api.localhost/mcp`.
2. If the MCP is not connected, tell the user how to create a personal token at
   `https://web.<base-domain>/account/tokens` and configure it as a Bearer
   credential in their client. Read
   [references/installation.md](references/installation.md) only when client
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
