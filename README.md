# AICA Life OS — plugin for Cursor / Grok Bot

**AICA Life OS** as a hosted MCP server: your AI assistant reads your day,
tasks, moments and Life Score, and proposes changes that you confirm in AICA.
One URL, OAuth sign-in, nothing to paste.
Product: [aica.guru](https://aica.guru).

```
MCP URL   https://aica.guru/life/mcp
Auth      OAuth 2.1 (Authorization Code + PKCE, dynamic client registration)
License   MIT
```

## 1. Connect

Two ways. Both end on the same OAuth screen.

**From a marketplace** — Cursor: search `aica` in the plugin store and click
**Install**. Grok Bot plugins: same bundle. The connect card is **OAuth**: a
browser page opens, you confirm your AICA e-mail, click the link in your
inbox, tap **Autorizar**, and you are connected.

**From any MCP client or AI harness** — paste this prompt:

```
Connect the AICA Life OS MCP server.

URL: https://aica.guru/life/mcp
Transport: Streamable HTTP (remote server).
Auth: OAuth. The server advertises it; discover it dynamically.
Leave every auth field blank: no header, no token, no API key, no env var.

When the browser opens I will confirm my AICA e-mail, click the link in my
inbox and tap "Autorizar". After that, call get_today to confirm the
connection and tell me what you see.
```

Do **not** paste a JWT, an API key or any header. `mcp.json` declares the URL
and nothing else. If a client asks you for a token, you are adding the server
by hand the wrong way; stop and let the OAuth flow run.

### The e-mail step

AICA signs you in with a magic link (no password). Open that e-mail **on the
same computer** where your client is running — the link returns the
authorization to the app on that machine. Once connected, the client
refreshes its own credential; you will not be asked again until you
disconnect.

## 2. After Autorizar: first sync

Nothing is written to AICA on its own. Paste this to make the assistant look
at what it can reach and propose what belongs in your Life OS:

```
You are connected to AICA Life OS. Scan the calendar, files and task lists
you can reach from here. For each item decide whether it belongs in AICA
(a commitment, a task, a moment worth keeping, a notice). Propose each one
with the propose_* tools, one proposal per item, with a short reason.
Do not invent items. When done, list what you proposed.
```

Then open [aica.guru](https://aica.guru), go to the chat session
*Propostas MCP* and tap **Aceitar** on each proposal you want (or dismiss it).
Same rules as every other AICA client: the assistant proposes, you accept.

## 3. Manus

Add the MCP server by hand:

```
URL     https://aica.guru/life/mcp
Auth    leave blank (no token, no header, no key)
```

Manus runs the OAuth flow in the browser: confirm e-mail, magic link,
**Autorizar**. If Manus insists on an API key or token to save the server,
**stop**. There is no key. The server speaks OAuth only; pasting anything
there will not work.

## 4. Optional: a standing daily routine

Add a standing instruction in your harness (Cursor rules, a Claude Code
scheduled routine, a Manus scheduled task, …). Example:

```
Every morning: call get_today and list_tasks on AICA Life OS and summarize
my day in five lines. If anything on my calendar, in my files or in my
tasks is missing from AICA, propose it with propose_* and remind me to
review it in Propostas MCP.
```

Proposals from a routine follow the same rule: nothing lands until you tap
**Aceitar**.

## What the tools do

Reads: `get_today`, `list_tasks`, `search_moments`, `get_life_score`,
`list_notices`. Writes are **proposals** (`propose_task`, `propose_moment`,
`propose_complete_task`, …): nothing lands in your Life OS until you tap
**Aceitar** in AICA (chat session *Propostas MCP*).

## Bundle

```
.cursor-plugin/plugin.json   manifest (name `aica`, displayName `AICA Life OS`, MIT)
mcp.json                     one remote server: https://aica.guru/life/mcp
assets/logo.png              official AICA mark (white: rings, serif A, vine, “Aica”)
LICENSE                      MIT
```
