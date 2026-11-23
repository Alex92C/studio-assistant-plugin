# ClassesBook AI Studio Assistant plugin

Cursor and Grok Bot plugin for [ClassesBook](https://classesbook.com), the class booking software for fitness studios. It packages agent skills and the ClassesBook remote MCP server, so your agent can check the schedule, see who is booked, manage waitlists, book and cancel classes, and edit classes, packages, forms and studio settings.

Every change is prepared as a plan and is saved only after you confirm it (`confirm_plan`).

## MCP server

```
https://mcp.classesbook.com
```

- Transport: Streamable HTTP (remote MCP)
- Auth: OAuth 2.1 authorization code + PKCE (S256), with dynamic client registration and client ID metadata documents. Scope: `offline_access`.
- Sign in with the same email, password or Google account you use in ClassesBook. The account must already exist.
- The server acts only as the signed-in user. Role (owner, instructor, member) and studio are derived on the server, never from the client. There is no shared API key: never paste a key or token into chat.

You don't need this plugin to use the connector: any MCP client that supports remote servers with OAuth can add the URL above. See the setup guide for Claude, ChatGPT, Grok Bot, Cursor, Mistral Le Chat, Gemini CLI, Codex, VS Code, n8n and more: https://classesbook.com/ai-connector/ *(page pending publication)*.

## Install in Grok Bot

After the marketplace listing is live:

1. Open **Connect Apps** in the Grok Bot sidebar (on mobile: avatar → Connect Apps).
2. Search for **studio-assistant** and add it.
3. Choose **Authorize** and sign in with your ClassesBook account.
4. In chat, attach `@studio-assistant` if the Bot does not pick it up on its own.

Before the listing is live, ask Grok Bot to add the MCP connector `https://mcp.classesbook.com`, then Authorize.

## Install in Cursor

After the listing is approved, install from the Cursor Marketplace. To try the package locally:

```bash
cp -R . ~/.cursor/plugins/local/studio-assistant
```

Reload Cursor, confirm the skills and the MCP server appear, and complete the browser sign-in. Or add only the server to `~/.cursor/mcp.json`:

```json
{ "mcpServers": { "classesbook": { "url": "https://mcp.classesbook.com" } } }
```

## Install in Gemini CLI

```bash
gemini extensions install https://github.com/Alex92C/studio-assistant-plugin
```

Then run `/mcp auth classesbook` to sign in.

## Test prompt

> What is my studio session, and what is on the schedule this week?

You should get your role, the studio timezone, the booking window and upcoming classes. Then ask for a change (for example "cancel Saturday's 10:00 class"). The assistant should describe the plan and wait for your OK before `confirm_plan`.

## Layout

```
plugin.json                 Agent Plugins manifest
.cursor-plugin/plugin.json  Cursor plugin manifest
.claude-plugin/plugin.json  Claude plugin manifest
mcp.json / .mcp.json        Remote MCP URL
gemini-extension.json       Gemini CLI extension manifest (+ GEMINI.md context)
skills/                     Workflow skills
assets/logo.png             Marketplace logo (512×512)
```

## Privacy, terms and support

- Privacy: https://classesbook.com/ai-connector/privacy/ *(pending publication)*; general policy https://classesbook.com/privacy-policy/
- Terms: https://classesbook.com/ai-connector/terms/ *(pending publication)*; general terms https://classesbook.com/terms-of-service/
- Support: support@classesbook.com

## License

MIT
