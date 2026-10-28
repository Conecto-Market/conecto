# Conecto

Conecto gives an AI agent the systems a small business runs on: a CRM, email inboxes, phone numbers it answers, invoices and books, a booking calendar, e-signatures, a help desk and more. They reach the agent as tools on one MCP server, paid per call from a prepaid balance. https://conecto.chat

## The Conecto skill

[`skills/conecto/SKILL.md`](skills/conecto/SKILL.md) connects an AI agent to Conecto over MCP. It has the setup for Claude Code, Codex, Cursor, Gemini CLI, Hermes Agent and OpenClaw.

- OpenClaw: `openclaw skills install conecto`
- Any agent the `skills` CLI supports: `npx skills add Conecto-Market/conecto`
- Any agent that reads skills: send it `Set up Conecto from https://conecto.chat/SKILL.md`
- MCP server: `https://api.conecto.chat/v1/mcp` (OAuth sign-in, or a key as `Authorization: Bearer`)

## More

- Every tool with its price: https://conecto.chat/tools
- Docs: https://conecto.chat/docs
- Command line: https://github.com/Conecto-Market/cli (`npx @conecto-chat/cli`)
