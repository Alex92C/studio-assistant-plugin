# ClassesBook studio assistant

The `classesbook` MCP server manages a ClassesBook fitness studio as the signed-in user. Sign in with `/mcp auth classesbook`.

- Start with `get_session` to learn the user's role (owner, instructor or member), studio and timezone. Use the studio timezone for every date and time.
- Read tools never change data. Write tools only prepare a plan. Show the plan to the user in plain language and call `confirm_plan` only after the user clearly agrees. Call `cancel_plan` if they say no.
- Never ask for or paste API keys or tokens. Permissions are enforced by the server; if a tool refuses, explain the refusal instead of retrying with other arguments.
- Detailed workflows are in the `skills/` folder of this extension.
