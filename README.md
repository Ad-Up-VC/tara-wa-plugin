# Webbai

Connect Claude to WhatsApp. Send messages, follow up with leads, run bulk campaigns, and set up automations — all through natural language.

## Install

**Option 1 — slash command (fastest, Claude Code terminal):**

```
/install github:MaikelSnijders/wa-plugin
```

**Option 2 — via the Cowork UI (if you're not in a terminal):**

1. Open Claude → **Cowork** (or **Code**) in the sidebar → **Customize**
2. Click the **+ icon** → **Create plugin** → **Add marketplace**
3. Paste: `https://github.com/MaikelSnijders/wa-plugin`
4. Confirm — the plugin installs automatically

Either way, Claude will open your browser to log in at [webbai.nl](https://webbai.nl) the first time you use a Webbai command. No API key needed.

Full step-by-step with screenshots: [webbai.nl/connect-claude](https://webbai.nl/connect-claude).

## Skills

| Command | Description |
|---------|-------------|
| `/webbai:setup` | Connect your WhatsApp Business number and set up reminders |
| `/webbai:send-reminders` | Check calendar and send WhatsApp reminders to today's clients |
| `/webbai:inbox` | View and reply to incoming WhatsApp messages |
| `/webbai:flows` | Create and manage automation flows in plain English |

## What you can do

- **"Send the welcome template to all new leads"** — bulk messaging with smart queue
- **"Set up an automation: when a Facebook lead comes in, send welcome_v1"** — automations in plain English
- **"Import contacts.csv and send them the promo template"** — CSV import + bulk send
- **"Check my inbox for unread messages"** — WhatsApp inbox management
- **"What new leads came in today?"** — lead tracking
