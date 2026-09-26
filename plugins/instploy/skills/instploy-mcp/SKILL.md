---
name: instploy-mcp
description: Connect and use InstPloy MCP in Claude. When the user enables InstPloy, says connect InstPloy, or pastes instploy url/Authorization JSON, run the connect-instploy flow first, then use InstPloy tools.
---

# InstPloy MCP (Claude)

## First-time / reconnect

If InstPloy tools are missing, failing auth, or the user wants to connect:

1. Run **`/instploy:connect-instploy`** (or ask them to paste JSON)
2. Accept JSON like:

```json
"instploy": {
  "url": "https://YOUR_INSTANCE.instploy.com/instploy/manager/mcp",
  "headers": {
    "Authorization": "Bearer YOUR_TOKEN_HERE"
  }
}
```

3. Guide them to set plugin options:
   - **InstPloy MCP URL** (`instploy_url`)
   - **Authorization Bearer token** (`instploy_token`, without the word `Bearer`)
4. Reload plugins if needed (`/reload-plugins`)

Never invent URL or token values. Never echo the full token — mask it (first 8 chars + `…`).
Do not write Cursor or ChatGPT config paths from this Claude plugin.

## After connected

- Prefer InstPloy MCP tools for remote workspace, Odoo install/upgrade, terminals, and deploy tasks
- Confirm the target instance before restart/upgrade/delete
- Never commit Bearer tokens to a repo
