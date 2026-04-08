---
name: flows
description: Create and manage WhatsApp automation flows — multi-step sequences, auto-replies, delayed follow-ups, and more
---

Help the user create and manage automation flows through natural language conversation.

## Step 1: Show current automations

Call `list_automations` to see what's already set up. Show a clear summary:
- Standalone automations: name, trigger, template, delay, active/paused
- Multi-step flows: grouped by flow_group with step order
- If none exist: "You don't have any automations yet. Let me help you set one up."

## Step 2: Understand what they want

Ask what they'd like to automate. Examples:
- "Send a welcome message when a new lead comes in, then follow up after 24h"
- "When someone replies with 'yes', send the booking link"
- "Create a 3-step onboarding sequence for new leads"
- "Turn off the follow-up automation"

## Step 3: Create automations

### Trigger types
Map the user's description to:
- "new lead" / "lead comes in" / "form submitted" → `new_lead`
- "booking" / "appointment" / "someone books" → `booking`
- "reminder" / "before appointment" → `appointment_reminder`
- "when someone replies" / "when they message back" → `inbound_reply`
- "manually" / "on demand" → `manual`

### Single-step automation
```
name: "Welcome new leads"
trigger_type: "new_lead"
template_name: "welcome_message"
delay_minutes: 0
```

### Multi-step flow
Group automations with the same `flow_group` and sequential `step_order`:

```
Step 1: Welcome (instant)
  flow_group: "onboarding"
  step_order: 1
  trigger_type: "new_lead"
  template_name: "welcome_msg"
  delay_minutes: 0

Step 2: Follow-up (24h later)
  flow_group: "onboarding"
  step_order: 2
  trigger_type: "new_lead"
  template_name: "followup_24h"
  delay_minutes: 1440

Step 3: Last chance (3 days later)
  flow_group: "onboarding"
  step_order: 3
  trigger_type: "new_lead"
  template_name: "last_chance"
  delay_minutes: 4320
```

All steps queue at trigger time with their respective delays. The queue worker picks them up when `scheduled_for` arrives.

### Keyword-based auto-reply
```
name: "Confirm on 'yes'"
trigger_type: "inbound_reply"
trigger_config: {"keyword": "yes"}
template_name: "booking_confirmation"
delay_minutes: 0
```

### Delay reference
- Instant: `0`
- 1 hour: `60`
- 6 hours: `360`
- 24 hours: `1440`
- 2 days: `2880`
- 3 days: `4320`
- 1 week: `10080`

## Step 4: Create templates if needed

If the user needs a template that doesn't exist:
1. Ask what the message should say
2. Choose category: MARKETING (promos), UTILITY (transactional), AUTHENTICATION (OTPs)
3. Use `create_whatsapp_template` to create it
4. Tell user: "UTILITY templates are usually approved instantly. MARKETING may take a few hours."
5. Set up the automation to use the new template

## Step 5: Variable mappings

When setting up template variables:
- `{{contact.name}}` → contact's name
- `{{contact.phone}}` → their phone number
- `{{contact.email}}` → their email
- `{{lead.source}}` → where the lead came from (facebook, generic, etc.)
- `{{lead.event_type}}` → type of event
- Or any literal text string

## Step 6: Managing automations

- "Turn off [name]" → `update_automation` with `active: false`
- "Change the delay to 48h" → `update_automation` with `delay_minutes: 2880`
- "Remove step 3 from the onboarding flow" → `delete_automation`
- "Add a step to the welcome flow" → `create_automation` with matching flow_group

After any changes, show the updated list.

## Important notes

- WhatsApp requires template messages for first contact. Free-form only within 24h of their last reply.
- `inbound_reply` automations have a built-in 24h cooldown per contact to prevent spam.
- Deactivating an automation cancels any pending delayed messages for that automation.
- Templates must be approved by Meta before use. Use `create_whatsapp_template` to create them.
- For complex logic beyond these automations (e.g. "check CRM, find inactive contacts, send personalized messages"), suggest using Claude scheduled tasks instead.
