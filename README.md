# GlassFrog MCP Server

Connect AI agents and assistants to [GlassFrog](https://www.glassfrog.com) — the organizational clarity platform for Holacracy and role-based organizations.

The GlassFrog MCP server gives any MCP-compatible client (Claude Code, Claude Desktop, Cursor, and others) live access to your organization's roles, accountabilities, skills, notes, tensions, and governance — so agents can operate as first-class participants in your organization.

## Server URL

```
https://app.glassfrog.com/api/v5/mcp
```

- **Transport:** Streamable HTTP (JSON-RPC over POST)
- **Auth:** GlassFrog API key via the `X-Auth-Token` header

## Quick start

Get an API key from your GlassFrog account (Profile → API Keys), then add the server to your client.

**Claude Code:**

```bash
claude mcp add --transport http glassfrog https://app.glassfrog.com/api/v5/mcp \
  --header "X-Auth-Token: YOUR_API_KEY"
```

**Generic `.mcp.json` / client config:**

```json
{
  "mcpServers": {
    "glassfrog": {
      "type": "http",
      "url": "https://app.glassfrog.com/api/v5/mcp",
      "headers": {
        "X-Auth-Token": "YOUR_API_KEY"
      }
    }
  }
}
```

## Tools

- **glassfrog_startSession** — Start an agent session for a role; returns full role context (purpose, accountabilities, org rules, skills, notes) so an agent can fill the role.
- **glassfrog_endSession** — End a session with a summary of what was accomplished.
- **glassfrog_listRoles** — List roles in the organization, with accountabilities, domains, and fillers.
- **glassfrog_getRole** — Get a single role by ID.
- **glassfrog_getRoleContext** — (Deprecated — use `glassfrog_startSession`.) Get everything needed to fill a role.
- **glassfrog_listSkills** — List skills in the organization's skill library, filterable by role or tags.
- **glassfrog_getSkill** — Get a skill's full markdown content.
- **glassfrog_createSkill** — Create a skill in the organization skill library.
- **glassfrog_updateSkill** — Update a skill's content, name, or tags.
- **glassfrog_listNotes** — List notes across the organization.
- **glassfrog_getNote** — Get a note's full content.
- **glassfrog_createNote** — Create a note on a role.
- **glassfrog_updateNote** — Update a note.
- **glassfrog_createTension** — Create a tension on a role, feeding the organization's governance process.
- **glassfrog_listAssignments** — List assignments (who fills a role).
- **glassfrog_readApiSpec** — Read the GlassFrog v5 OpenAPI specification.
- **glassfrog_apiCall** — Make an authenticated call to any GlassFrog v5 REST endpoint.

## What you can build

- **Agents that fill organizational roles** — boot with `glassfrog_startSession` to load a role's purpose, accountabilities, and accumulated knowledge, then work the role.
- **Governance participation** — sense and file tensions programmatically; the full proposal flow is available via `glassfrog_apiCall` against the v5 API.
- **Organizational memory** — skills and notes as durable, shared agent knowledge that survives sessions.
- **Custom integrations** — `glassfrog_apiCall` + `glassfrog_readApiSpec` open the entire v5 REST API through a single MCP connection.

## API documentation

Full v5 API reference: https://app.glassfrog.com/api/v5/docs

## Support

- Product: https://www.glassfrog.com
- Questions and issues: open an issue on this repository
