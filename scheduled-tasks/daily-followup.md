# Daily Follow-up Check

**Schedule:** Every day at 2:00 PM
**Cron:** `0 14 * * *`
**Skills used:** inbox, contacts

## What It Does

Every afternoon, reviews your WhatsApp conversations and leads to find:
- Unanswered messages from contacts
- New leads that haven't been contacted
- Contacts who were messaged days ago but haven't replied

Then drafts personalized replies and waits for your approval before sending anything.

## Workflow

1. Call `get_inbound_messages` with `unread_only: true` to find unanswered messages
2. For each message, check the `already_replied` field — skip any where `already_replied` is true
3. For each truly unanswered message:
   - Check if it's within the 24h reply window
   - Draft a reply that matches the message tone and answers the question
   - Present for approval: send / edit / skip
4. Call `get_leads` to find leads with status 'new' that haven't been contacted
4. For new leads:
   - Group them together
   - Suggest sending the welcome template to all at once
   - Use `send_whatsapp_template` for first contacts (required by WhatsApp)
5. Check `get_send_logs` with `days_back: 7` for contacts messaged 2+ days ago with no reply
6. For stale conversations:
   - Suggest a gentle follow-up using a template
7. Present summary of actions taken

## Output Format

```
Today's follow-up report:
- 2 unanswered messages (replied to 1, skipped 1)
- 3 new leads contacted with welcome template
- 1 follow-up reminder sent

Everything else looks good! Your inbox is at webbai.nl/inbox.
```

## Rules

- NEVER send a message without user approval
- Always use templates for first contact (WhatsApp requires this)
- Be specific about timing: "3 days ago", "yesterday", not raw timestamps
- Group similar actions: "Send welcome to all 3 new leads?" instead of one by one
- If nothing needs follow-up: "All caught up! No pending follow-ups."
