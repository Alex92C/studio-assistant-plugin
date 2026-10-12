# Studio assistant

Cursor / Grok Bot plugin for the [ClassesBook](https://app.classesbook.com) booking app. It packages agent skills and a remote MCP server so a Grok Bot or Cursor agent can look up classes, bookings, attendees, packages, forms, and settings the same way the in-app assistant does.

Writes never save until the user agrees and the host calls `confirm_plan`.

MCP server:

`https://us-central1-angular-auth-app-da196.cloudfunctions.net/mcpServer`

## Install in Grok Bot (after marketplace listing)

1. Open **Connect Apps** in the Grok Bot sidebar (on mobile: avatar → Connect Apps).
2. Search for **studio-assistant** and add it.
3. Choose **Authorize** and sign in with the same email, password, or Google account you use in the booking app. The account must already exist in ClassesBook.
4. Confirm the plugin is under **Installed** and authenticated.
5. In chat, attach `@studio-assistant` if the Bot does not pick it up on its own.

Until Cursor lists this repository, add the MCP URL in Grok Bot chat as a custom streamable HTTP server, then Authorize. Do not paste an API key or Firebase token into chat.

## Install in Cursor

After the listing is approved, install from the Cursor Marketplace in **Customize**. To try the package locally before that:

```bash
cp -R . ~/.cursor/plugins/local/studio-assistant
```

Reload the Cursor window and confirm skills plus the MCP server appear under Customize. Complete the browser login with a ClassesBook account.

## Test prompt

After you are signed in, ask:

> What is my studio session, and what is on the schedule this week?

You should get a role, timezone, booking window, and upcoming classes. Then ask to change something (for example cancel a class). The assistant should describe the change and wait for your agreement before `confirm_plan`.

## Layout

```
plugin.json                 Agent Plugins manifest
.cursor-plugin/plugin.json  Cursor plugin manifest
mcp.json                    Remote MCP URL
skills/                     Workflow skills
assets/logo.svg             Marketplace logo
```

## Auth

Sign-in uses OAuth 2.1 authorization-code + PKCE against the MCP server. Role and studio owner are derived on the server from the Firebase user, never from the client. There is no shared studio API key.

Grok Bot / Cursor Agents currently need the MCP server to allow Cursor's OAuth callback (`https://www.cursor.com/agents/mcp/oauth/callback`) and Dynamic Client Registration or a pinned Cursor client. If Authorize fails after install, that server change is still outstanding.

## Source

The booking app that hosts this MCP server is [Alex92C/classes-booking-app](https://github.com/Alex92C/classes-booking-app).
