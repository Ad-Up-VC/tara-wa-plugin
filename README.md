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

## Skills (13)

Claude loads these on-demand based on what you ask. You don't have to remember the names — just describe what you want.

| Command | What it does |
|---------|-------------|
| `/webbai:setup` | First-run onboarding — links your account, walks you through WhatsApp connect, Google Calendar, contacts, scheduled tasks. Knows about the coexistence pairing window. |
| `/webbai:inbox` | Review unread WhatsApp messages, get AI-drafted replies, send within the 24h window. |
| `/webbai:send` | Send a one-off message or a quick bulk. Picks template (cold) vs free-form (within 24h) automatically. |
| `/webbai:send-reminders` | Check today's calendar → generate + send personalized appointment reminders. Dedups by phone. |
| `/webbai:campaigns` | Bulk template campaigns: pick template, pull contact list (filters / CSV / manual), confirm count, monitor batch progress. |
| `/webbai:contacts` | Search, import, update status, view a lead's full activity. |
| `/webbai:flows` | Build automation flows in plain English — welcome, follow-ups, auto-replies, multi-step nurture. Now covers the `connected_whatsapp` event_type for "welcome customer on WA connect" automations. |
| `/webbai:templates` | **(new in v1.3)** Create / edit / list / delete WhatsApp message templates. Handles Meta's gotchas — required `example.body_text`, UTILITY vs MARKETING rules, headers, footers, URL/phone buttons, what to do with REJECTED templates. |
| `/webbai:appointments` | View + update appointments, create manual ones (no Calendly needed). |
| `/webbai:demo-followups` | Find yesterday's completed demos → propose + send personalized WhatsApp follow-ups. |
| `/webbai:crm-status` | Query your connected CRM (Pipedrive / HubSpot / Zoho / Tribe) — deals, pipeline, activity for any contact. |
| `/webbai:calendly-setup` | Connect Calendly with a Personal Access Token. |
| `/webbai:settings` | View + change account settings, plan, billing, regenerate your API key. |

## What you can do

### Messaging + inbox

- **"Check my inbox"** — see unread WhatsApp messages with AI-drafted reply suggestions
- **"Reply to Sam"** — Claude drafts, you confirm, it sends (respects 24h window)
- **"Send the welcome template to all new leads"** — bulk messaging with smart queue + plan-aware throttling

### Leads + follow-up

- **"What new leads came in today?"** — lead tracking with source + status
- **"Find yesterday's demos and send follow-ups"** — auto-personalized per attendee
- **"Set up an automation: when a Facebook lead comes in, send `welcome_v1` instantly, then follow-up after 24h"** — multi-step nurture in plain English
- **"Build a flow that sends `webbai_connected` the moment a customer connects WhatsApp"** — uses `event_type='connected_whatsapp'` filter (canonical "welcome on connect" pattern)

### Templates

- **"Create a UTILITY template that confirms a booking"** — Claude handles `example.body_text` so Meta doesn't auto-reject
- **"Add a URL button to my welcome template that opens the inbox"** — full button-type support (Quick reply / URL / Phone)
- **"My `welcome_v2` template got rejected — fix it"** — Claude diagnoses + resubmits with corrected components

### CRM + integrations

- **"What's Sam's status in Pipedrive?"** — searches connected CRM by name/phone/email, returns deals + activities
- **"When a deal in HubSpot moves to Won, send my onboarding sequence"** — CRM-event-driven automation flows

### Bulk + campaigns

- **"Import contacts.csv and queue the spring promo"** — CSV import + bulk template send
- **"How's batch #12 doing?"** — live progress on bulk campaigns

### Settings + connections

- **"Connect my Google Calendar"** / **"Connect Calendly with this PAT"** — guided integration setup
- **"Show my API key"** / **"Rotate my API key"** — account management

## What runs automatically (no command needed)

These fire in the background — useful to know about but you never invoke them:

- **Welcome email** sent immediately when a new account signs up at webbai.nl
- **Signup follow-up emails** at day 1 / 3 / 7 for accounts that haven't connected WhatsApp yet (stops automatically once they connect)
- **Coexistence sync** — if a customer has the WhatsApp Business app on the same number, messages they send from the phone app are mirrored into your Webbai inbox via `smb_message_echoes`
- **Daily / weekly briefings** — if you've toggled them on at `/automations`, Claude composes a digest of pending inbox items and sends to your email
- **Queue worker** — drains pending sends to Meta every ~2 seconds, retries 3× with backoff on transient failures
- **Plan-aware rate limits** — bulk sends and automation queues respect your plan's daily message cap

## Safety + 24h window

The plugin respects WhatsApp's rules so your number never gets flagged:

- Free-form messages are only sent within 24h of a contact's last inbound — outside that, templates only.
- Bulk campaigns and first-contact messages always confirm recipient count + template name before firing.
- Inbound message content is treated as untrusted — Claude won't follow instructions embedded in customer messages.
- Plan limits are checked before flow/campaign creation so you don't hit Meta's rate caps mid-send.

## Need help

- Setup guide with screenshots: [webbai.nl/connect-claude](https://webbai.nl/connect-claude)
- Dashboard: [webbai.nl](https://webbai.nl)
- Product overview: [PRODUCT.md](./PRODUCT.md)
- Internal docs: [CLAUDE.md](./CLAUDE.md)
