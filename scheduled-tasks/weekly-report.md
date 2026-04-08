# Weekly WhatsApp Report

**Schedule:** Every Monday at 9:00 AM
**Cron:** `0 9 * * 1`
**Skills used:** inbox, contacts

## What It Does

Every Monday morning, generates a summary of your WhatsApp activity from the past week — messages sent, replies received, new leads, and pending follow-ups.

## Workflow

1. Call `get_send_logs` to count messages sent in the past 7 days
2. Call `get_inbound_messages` to count replies received in the past 7 days
3. Call `get_leads` to find new leads from the past 7 days
4. Call `get_leads` to find contacts with status 'new' or 'contacted' that still need attention
5. Calculate response rate: (replies / messages sent) * 100
6. Identify top conversations (most messages exchanged)
7. Present the report in a clear, scannable format

## Output Format

```
Weekly WhatsApp Report (March 31 - April 7)

Messages sent: 47
Replies received: 32 (68% response rate)
New leads: 8
  - 5 from Facebook
  - 2 from website
  - 1 from WhatsApp

Still need attention:
- 3 leads not yet contacted
- 2 follow-ups pending (no reply after 3+ days)

Top conversations:
- Sarah Johnson: 12 messages exchanged
- Mike de Vries: 8 messages exchanged

Tip: Your response rate is great! Consider setting up auto-replies for common questions to respond even faster.
```

## Rules

- Always include the date range in the report header
- Calculate response rate as a percentage
- Group new leads by source
- Highlight contacts that need attention
- End with a practical tip or suggestion
- If it was a quiet week: "Quiet week! Only [N] messages sent. Consider running a campaign to re-engage your contacts."
