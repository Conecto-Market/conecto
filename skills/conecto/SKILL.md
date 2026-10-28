---
name: conecto
description: "Business tools for your AI agent through one MCP server: a lead finder, a CRM, email inboxes, phone numbers it answers, invoices and bookkeeping, a booking calendar, e-signatures and a help desk. Works with Claude Code, Codex, Cursor, Gemini CLI, Hermes Agent and OpenClaw. Conecto is a paid service, charged per tool call from a prepaid balance."
metadata:
  openclaw:
    homepage: https://conecto.chat/agents/openclaw
---

# Conecto

Conecto gives you, the agent, the systems a small business runs on: its CRM, email inboxes, phone line, invoices and books, booking calendar, e-signatures, help desk and more. They run on Conecto's servers and reach you as tools on one MCP server, `https://api.conecto.chat/v1/mcp`. Conecto is a paid service: each tool call is charged to the business's prepaid balance (see Money).

## Connect once

Add the server once, in the agent you run in. Ask the person to add it, or add it yourself if they say so.

Most agents connect with a key. The owner makes one on the account page (https://conecto.chat/account). A new business creates its account at https://conecto.chat/account/signup first. Keep the key in the `CONECTO_KEY` environment variable. No key goes in this skill. If the person has no key yet, https://conecto.chat/SKILL.md shows how you sign up with one call, or join their account with a code from the account page.

### Claude Code

Steps: https://conecto.chat/agents/claude-code.md. In a terminal:

```bash
claude mcp add --transport http --scope user conecto https://api.conecto.chat/v1/mcp \
  --header "Authorization: Bearer $CONECTO_KEY"
```

Restart Claude Code so the tools load. `/mcp` lists them.

### Codex

Steps: https://conecto.chat/agents/codex.md. In `~/.codex/config.toml`:

```toml
[mcp_servers.conecto]
url = "https://api.conecto.chat/v1/mcp"
bearer_token_env_var = "CONECTO_KEY"
```

Codex sends the variable's value as `Authorization: Bearer`. Start a new session so the tools load.

### Cursor

Steps: https://conecto.chat/agents/cursor.md. In `.cursor/mcp.json` in the project, or in the global `mcp.json`:

```json
{
  "mcpServers": {
    "conecto": {
      "url": "https://api.conecto.chat/v1/mcp",
      "headers": {
        "Authorization": "Bearer ${env:CONECTO_KEY}"
      }
    }
  }
}
```

Open Customize, MCP, and check that the server shows its tools.

### Gemini CLI

Steps: https://conecto.chat/agents/gemini-cli.md. Under `mcpServers` in `~/.gemini/settings.json`:

```json
{
  "mcpServers": {
    "conecto": {
      "httpUrl": "https://api.conecto.chat/v1/mcp",
      "headers": {
        "Authorization": "Bearer $CONECTO_KEY"
      }
    }
  }
}
```

Run `/mcp` in Gemini CLI to see the tools.

### Hermes Agent

Steps: https://conecto.chat/agents/hermes-agent.md. In `~/.hermes/config.yaml`, with the key in `~/.hermes/.env`:

```yaml
mcp_servers:
  conecto:
    url: "https://api.conecto.chat/v1/mcp"
    headers:
      Authorization: "Bearer ${CONECTO_KEY}"
```

Start a new session, or run `/reload-mcp` in the one you have.

### OpenClaw

Steps: https://conecto.chat/agents/openclaw.md. OpenClaw signs in instead of using a key. In a terminal:

```bash
openclaw mcp add conecto \
  --url https://api.conecto.chat/v1/mcp \
  --transport streamable-http \
  --auth oauth
openclaw mcp login conecto
openclaw mcp doctor conecto --probe
```

`openclaw mcp login conecto` opens Conecto's sign-in. The person signs in, ticks the areas you may use and allows it. You then run on a key of your own that acts as that person, and no key goes in an environment variable. `doctor --probe` should list Conecto's tools.

### Other agents

Add `https://api.conecto.chat/v1/mcp` as a remote MCP server over streamable HTTP, with the key in the header `Authorization: Bearer <key>`.

## What you can do

Each area is a set of tools. Before you call a tool for the first time, read its page at `https://conecto.chat/tools/<area>/<tool>.md`: its inputs, an example call, a real reply and its errors.

- Lead finder: businesses that could buy from the business, and the person to reach at each, with their work email checked (`prospects_prepare`, `prospects_find`). A short interview about the customers wanted comes first, and you ask it in your own chat. Each prospect found with a working email costs $0.05, and the rest cost nothing. The interview, reading and keeping prospects are free.
- CRM: contacts, companies, deals, notes and tasks (`crm_search`, `crm_save_contact`, `crm_save_deal`).
- Email: inboxes on the business's own subdomain that you send from and read (`email_send`, `email_list_messages`).
- Phone: numbers in the US and Canada that you answer, with a transcript of every call (`phone_search_numbers`, `phone_setup_assistant`).
- Invoices and books: quotes, invoices, expenses and the books behind them (`invoices_create`, `invoices_send`, `books_record_expense`).
- Calendar: booking pages and meetings (`calendar_find_times`, `calendar_book`).
- E-signature: documents sent for signing (`esign_send`).
- Help desk: tickets from email and chat (`ticket_create`, `ticket_list`).
- Also forms, files, projects, HR, hiring, inventory, purchasing, newsletters, website chat and more. Every area and tool: https://conecto.chat/tools.md

## Money

- Every tool has a published price on its page. Examples: $0.01 for a CRM change, $0.001 per email recipient, $0.10 for an invoice sent, $0.01 for a meeting booked, $0.50 for a document sent for signing, $0.25 per started minute of an answered call.
- Reading the business's own data is free up to 1,000,000 reads a month, and a call that fails costs nothing. Every reply carries `cost_usd` and `balance_usd`.
- A new account starts with $1.00 of free credit. Only a person adds money, through a Stripe checkout on the account page (https://conecto.chat/account), from $5.00 plus a 7% + $0.35 fee.
- AI visibility and the phone run only on credit someone bought, never on free or bonus credit.
- Each key has a daily budget ($20.00 by default) and the account a monthly ceiling ($100.00). Only the owner raises them.

## Before you act

- Ask the person before a call that reaches people outside the business (an email to a customer, an invoice, a document to sign), starts a monthly rental (an inbox or a phone number), or costs more than $1.00, unless they asked for exactly that. Reading and searching need no question.
- The owner can make chosen tools wait for a person's approval. Such a call answers `approval_required`, and the request goes to the approver.
- A refused call says why and how to fix it. Every error code: https://conecto.chat/docs/errors.md
- Conecto's own rules: email and calls to people outside the business need one real top-up first, the phone line tells every caller it is an AI, and the only outbound calls confirm meetings booked in advance.

## More

- What Conecto is, who runs it and what it costs: https://conecto.chat/ai-questions
- Every tool with one line each: https://conecto.chat/tools/llms.txt
- Terms: https://conecto.chat/terms
