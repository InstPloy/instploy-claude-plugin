---
name: connect-instploy
description: Connect InstPloy MCP by pasting your instploy JSON (url + Authorization Bearer). Use when enabling the InstPloy plugin or when the user says connect InstPloy.
---

# Connect InstPloy (Claude)

## Goal

Ask the user for their InstPloy MCP JSON, parse it, and connect Claude to that MCP server.

## Step 1 — Ask for JSON

Ask the user (in their language) to paste a config like this:

```json
"instploy": {
  "url": "https://YOUR_INSTANCE.instploy.com/instploy/manager/mcp",
  "headers": {
    "Authorization": "Bearer YOUR_TOKEN_HERE"
  }
}
```

Accept any of these shapes:

- The `instploy` object only
- Wrapped as `{ "instploy": { ... } }`
- Wrapped as `{ "mcpServers": { "instploy": { ... } } }`

## Step 2 — Parse

From the pasted JSON extract:

1. `url` — required string, must start with `http`
2. Bearer token — from `headers.Authorization`
   - If value is `Bearer xxx`, keep `xxx` only
   - If value has no `Bearer` prefix, use it as-is

If `url` or token is missing, ask again. Do not invent values.

## Step 3 — Connect

Prefer plugin settings (userConfig):

1. Tell the user to open **Plugins → InstPloy → Configure** (or Claude Code plugin settings)
2. Set **InstPloy MCP URL** = parsed URL
3. Set **Authorization Bearer token** = parsed token
4. Reload plugins (`/reload-plugins`) if needed

Optional fallback — write user MCP config at `~/.claude.json` or project `.mcp.json` only if the user asks for a file-based connect:

```json
"instploy": {
  "type": "http",
  "url": "<parsed-url>",
  "headers": {
    "Authorization": "Bearer <parsed-token>"
  }
}
```

Do not print the full token — confirm with a masked form (first 8 chars + `…`).

## Step 4 — Confirm

Tell the user:

1. InstPloy MCP URL/token are configured
2. Start a new Claude session or run `/reload-plugins`
3. Confirm InstPloy tools are available

## Security

- Never commit the pasted JSON or token to a repo
- Never store the token inside the plugin files
- Prefer masking the token in replies
