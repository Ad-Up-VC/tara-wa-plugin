---
name: crm-status
description: Check lead/deal status and activity in connected CRM (Pipedrive, HubSpot, Zoho)
---

When the user asks about a lead, deal, follow-up status, or pipeline:

## Check lead / contact status

1. **Find the contact**: call `search_crm_contacts` with the phone number (preferred) or email/name.
   - If the user mentions a name only, first try `search_contacts` in Webbai to get their phone number, then search the CRM by phone.
   - Phone matching is most reliable — always prefer it.

2. **Show deal status**: for each associated deal, show:
   - Deal title and stage
   - Value and currency
   - Last update date
   - Status (open/won/lost)

3. **Check follow-up**: call `get_crm_activities` to see recent activities.
   - If the last activity was **>7 days ago** and the deal is still open, flag it: "This lead may need follow-up — last CRM activity was X days ago."
   - If there are open tasks, mention them.

4. **Offer action**: if the lead needs follow-up, offer:
   "Want me to send them a WhatsApp follow-up?"
   → Use `generate_whatsapp_message` with CRM context (deal stage, last activity) to craft a relevant message, then `send_whatsapp_message`.

## Show pipeline overview

When the user asks about their pipeline, funnel, or deal overview:

1. Call `get_crm_pipeline` to get stage breakdown.
2. Present as a clear summary: stage name, deal count, total value.
3. Highlight any stages with stale deals if relevant.

## Get deal details

When the user asks about a specific deal:

1. Call `get_crm_deal` with the deal ID (from a previous search).
2. Show full details: stage, value, contact, activities, expected close date.
3. If the deal has no recent activity, suggest follow-up.

## CRM not connected

If any CRM tool returns `connected: false`:
- Tell the user: "Your CRM isn't connected yet. Go to **webbai.nl/settings** and add your CRM API key under **CRM Integration**. We support Pipedrive, HubSpot, and Zoho."
- Don't retry the tool — wait for them to configure it.

## Important notes

- CRM data is fetched live — every call hits the CRM API directly, nothing is cached.
- The `search_crm_contacts` tool also syncs deal status back to Webbai: if a deal is Won, the Webbai contact status updates to "converted"; if Lost, it updates to "lost". This prevents stale follow-ups.
- Always use phone number as the primary match key between Webbai contacts and CRM contacts.
