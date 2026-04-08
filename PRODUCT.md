# Webbai — WhatsApp AI Agent for Business

Webbai connects Claude AI to WhatsApp Business API, giving business owners a conversational assistant that handles their WhatsApp communication.

## What Webbai does

- **Send WhatsApp messages** — free-form text or pre-approved templates, to individuals or in bulk
- **Manage your inbox** — read incoming messages, draft replies, send them with one confirmation
- **Automate follow-ups** — multi-step message sequences with delays, keyword auto-replies, lead nurturing flows
- **Daily appointment reminders** — checks Google Calendar every morning and sends personalized reminders to clients
- **Lead management** — import contacts, track lead status, search your contact database
- **Bulk campaigns** — send template messages to hundreds of contacts at once with rate limiting
- **Create templates** — draft and submit WhatsApp message templates for Meta approval

## How it works

Webbai runs as a hosted backend at `webbai.nl` that:
1. Connects to your WhatsApp Business account via Meta Cloud API
2. Stores your contacts, messages, and automations in a secure database
3. Exposes MCP tools that Claude can call to perform actions
4. Receives incoming WhatsApp messages via webhooks and makes them available in your inbox

## Key concepts

### WhatsApp messaging rules
- **First contact**: You MUST use an approved template message. Free-form text is blocked.
- **24-hour window**: After someone messages you, you can reply with free-form text for 24 hours.
- **After 24 hours**: Back to templates only.
- **Templates must be approved by Meta** before they can be used.

### Automations
- **Trigger types**: `new_lead` (when a lead comes in), `inbound_reply` (when someone messages you with a keyword)
- **Multi-step flows**: Chain multiple messages with delays (e.g., welcome → 24h follow-up → 3-day nudge)
- **Flow groups**: Group related automation steps together under a single flow name

### Contacts & leads
- Contacts are stored with name, phone, email, and source
- Leads have a status pipeline: new → contacted → qualified → converted / lost
- Contacts can be imported individually or in bulk via CSV

## MCP Tools available

| Tool | What it does |
|------|-------------|
| `get_setup_status` | Check if WhatsApp is connected |
| `setup_whatsapp` | Connect WhatsApp credentials |
| `send_whatsapp_message` | Send a free-form text message |
| `send_whatsapp_template` | Send a pre-approved template message |
| `list_whatsapp_templates` | List available templates |
| `create_whatsapp_template` | Create a new template for Meta approval |
| `delete_whatsapp_template` | Delete a template |
| `get_template_details` | Get full template details |
| `generate_whatsapp_message` | AI-generate a personalized message |
| `get_inbound_messages` | Fetch incoming messages |
| `mark_message_read` | Mark a message as read |
| `get_send_logs` | View sent message history |
| `search_contacts` | Search contacts by name or phone |
| `get_leads` | View leads with status filter |
| `update_lead_status` | Change a lead's pipeline status |
| `import_contacts` | Bulk import contacts |
| `send_bulk_template` | Send template to many contacts at once |
| `get_batch_status` | Check bulk send progress |
| `list_batches` | View all bulk send batches |
| `create_automation` | Create an automation rule |
| `list_automations` | View all automations |
| `update_automation` | Edit an automation |
| `delete_automation` | Remove an automation |

## Web dashboard

Users can also manage everything at `webbai.nl`:
- Real-time inbox with conversation threads
- Sent message log
- Settings (WhatsApp credentials, API key, webhooks)
- Contact management

## Phone number formatting (Netherlands default)
- `0612345678` → `31612345678`
- `+31 6 12345678` → `31612345678`
- `06-12345678` → `31612345678`
