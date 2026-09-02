# aica — Comdei Life OS plugin for Cursor / Grok Bot

The hosted **AICA Life OS MCP** as a one-click plugin. Public name: **Comdei**.
Product: [aica.guru](https://aica.guru).

```
MCP URL   https://aica.guru/life/mcp
Auth      OAuth 2.1 (Authorization Code + PKCE, dynamic client registration)
```

## Install

- **Cursor Marketplace** — search `aica` (or `comdei`) in the plugin store and
  click **Install**. The connect card is **OAuth**: Cursor opens a browser
  page, you confirm your AICA e-mail, click the link in your inbox, tap
  **Autorizar**, and you are connected.
- **Grok Bot plugins** — same bundle, same OAuth card.

Do **not** paste a JWT, an API key or any header. This plugin declares the
URL and nothing else — `mcp.json` has no `headers`, no `Bearer`, no
variables. If a client asks you for a token, you are adding the server by
hand instead of installing the plugin; use the plugin.

### The e-mail step

AICA signs you in with a magic link (no password). Open that e-mail **on the
same computer** where Cursor is running — the link returns the authorization
to the app on that machine. Once connected, the plugin refreshes its own
credential; you will not be asked again until you disconnect.

## What the tools do

Reads: `get_today`, `list_tasks`, `search_moments`, `get_life_score`,
`list_notices`. Writes are **proposals** (`propose_task`, `propose_moment`,
`propose_complete_task`, …): nothing lands in your Life OS until you tap
**Aceitar** in AICA (chat session *Propostas MCP*). Same rules as every other
AICA client.

## Bundle

```
.cursor-plugin/plugin.json   manifest (name `aica`, keywords aica/comdei/…)
mcp.json                     one remote server: https://aica.guru/life/mcp
assets/logo.png              official Comdei mark (lowercase comdei, cruz/vine in the d)
```

Source of the MCP server: private `Comdei/aica`, `tools/aica-mcp`. Spec:
`docs/specs/2026-09-01-mcp-oauth-catalog-2401.md` there.
