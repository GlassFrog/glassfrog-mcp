# GlassFrog MCP Server

Connect Claude and other AI assistants to [GlassFrog](https://www.glassfrog.com), the platform for Holacracy and role-based organizations.

Once connected, your assistant can read and work with your GlassFrog data as you: roles, accountabilities, projects, actions, tensions, policies, notes and messages. It sees and does only what you can, and anything it changes shows as changed by you.

## Server URL

```
https://app.glassfrog.com/api/v5/mcp/core
```

- **Transport:** Streamable HTTP
- **Auth:** OAuth 2.0 with dynamic client registration. You sign in to GlassFrog and approve the connection; no API key needed.
- **Tool sets:** `/api/v5/mcp/core` serves the everyday tools listed below. `/api/v5/mcp` serves every tool, including skill authoring, for clients that want the full set. Both use the same sign-in and permissions.

## Before you start

- Your organization needs **AI Integration** turned on. An organization admin turns it on in the organization settings. If it's off, GlassFrog won't list your organization when you connect.
- You need a GlassFrog account in that organization.

## Connect Claude

**Pro or Max:** in Claude, open **Customize → Connectors**, click **+ Add**, then **Add custom connector**. Enter the name `GlassFrog` and the URL above, leave the request headers empty, and click **Add**.

**Team or Enterprise:** an owner adds the connector once under **Organization settings → Connectors**. Each member then goes to **Customize → Connectors**, finds GlassFrog and clicks **Connect**. Everyone connects with their own GlassFrog account.

Claude then opens GlassFrog in your browser. Sign in, and on the approval screen:

- **Organization:** pick the one Claude should work in. Each connection covers one organization.
- **Permissions:**
  - **Everything I can access:** Claude acts as you, with everything you can see and do. This is the usual choice.
  - **Only selected roles:** Claude acts only through the roles you tick, with View or Edit for each.
  - **Everything in this organization:** admin access, shown only to organization admins.
- Click **Approve**. GlassFrog sends you back to Claude.

What you approve is fixed. To change it, disconnect and connect again.

## Example prompts

- "What projects and next actions do I have in GlassFrog?"
- "Summarize the purpose and accountabilities of the Marketing circle's roles."
- "Which of my projects haven't been updated in the last two weeks?"
- "Add a project to my Website role: 'New pricing page live', with a first action to draft the copy."
- "Raise a tension on the Facilitator role: our meeting notes aren't being shared after tacticals."
- "What does our circle's policy say about spending authorization?"

## Disconnect

In GlassFrog, click your name in the sidebar, open the **API** tab and go to **Connected apps**. Revoke Claude there. Removing the connector in Claude alone doesn't revoke GlassFrog's side.

## Other clients

Any MCP client that supports Streamable HTTP and OAuth 2.0 can connect with the URL above. Clients without OAuth can use a GlassFrog API key (your profile → **API** tab) in an `Authorization: Bearer` header:

```bash
claude mcp add --transport http glassfrog https://app.glassfrog.com/api/v5/mcp/core \
  --header "Authorization: Bearer YOUR_API_KEY"
```

## Tools

The tools on `/api/v5/mcp/core`. Read-only:

- **glassfrog_search** — Search across the organization.
- **glassfrog_listRoles** / **glassfrog_getRole** — Roles with purpose, accountabilities, domains and fillers.
- **glassfrog_getRoleContext** — Everything needed to work a role.
- **glassfrog_listAssignments** — Who fills which role.
- **glassfrog_listPeople** / **glassfrog_getPerson** — Organization members.
- **glassfrog_listProjects** / **glassfrog_getProject** — Projects.
- **glassfrog_listActions** / **glassfrog_getAction** — Next actions.
- **glassfrog_getPolicy** / **glassfrog_getOrgRule** — Policies and organization rules.
- **glassfrog_listNotes** / **glassfrog_getNote** — Role notes.
- **glassfrog_listSkills** / **glassfrog_getSkill** — Skills in the organization's library.
- **glassfrog_listChannels** / **glassfrog_getChannel** / **glassfrog_listMessages** — Role channels and messages.
- **glassfrog_listMyMessages** — New messages across all your channels.
- **glassfrog_listWorkRequests** / **glassfrog_getWorkRequest** — Requests between roles.
- **glassfrog_readApiSpec** — The GlassFrog v5 OpenAPI specification.

Write:

- **glassfrog_createProject** / **glassfrog_updateProject** — Create or update projects.
- **glassfrog_createAction** / **glassfrog_updateAction** — Create or update next actions.
- **glassfrog_createTension** — Raise a tension on a role.
- **glassfrog_createNote** / **glassfrog_updateNote** — Create or update role notes.
- **glassfrog_addTag** / **glassfrog_removeTag** — Tag notes, skills, roles, projects and actions.
- **glassfrog_postMessage** / **glassfrog_markChannelRead** — Post to role channels; mark them read.
- **glassfrog_startSession** / **glassfrog_endSession** — Start and end an agent session for a role.

Only **glassfrog_removeTag** is marked destructive; no tool deletes records.

## Privacy

See the [GlassFrog privacy policy](https://www.glassfrog.com/privacy-policy). The server returns only data the connected user can access. GlassFrog receives the tool calls Claude makes, not your conversations.

## Support

- Email: support@glassfrog.com
- REST API reference: https://app.glassfrog.com/api/v5/docs
