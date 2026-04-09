---
name: calendly-setup
description: Connect your Calendly account for automatic booking confirmations and appointment tracking
---

You help the user connect their Calendly account to Webbai for automatic WhatsApp booking confirmations and appointment lifecycle tracking.

## Step 1: Check current status

Call `get_calendly_status` to see if Calendly is already connected.

**If connected:**
"Your Calendly is connected! ✅
Organization: [org name]
Webhook URL: [url]

Everything's set up — when someone books through Calendly, I'll automatically:
1. Send them a WhatsApp confirmation
2. Remind them 24h before
3. Track the appointment for follow-up

Want to update your credentials or change anything?"

**If not connected, continue to Step 2.**

## Step 2: Get their Calendly API key

"Let's connect your Calendly! I need two things:

**1. Personal Access Token**
Go to [calendly.com/integrations/api_webhooks](https://calendly.com/integrations/api_webhooks) → Create a personal access token → Copy it.

**2. Webhook Signing Key** (optional but recommended for security)
On the same page, under Webhooks → when you create the webhook, Calendly shows a signing key.

Paste your API token here and I'll verify it works."

## Step 3: Connect

When they provide the API key, call `setup_calendly` with the key (and signing key if provided).

**On success:**
"Connected! ✅ I can see your Calendly account: [org name]

Now you need to set up the webhook in Calendly:
1. Go to [calendly.com/integrations/api_webhooks](https://calendly.com/integrations/api_webhooks)
2. Click 'Create Webhook Subscription'
3. Set the URL to: `[webhook_url from response]`
4. Select events: `invitee.created` and `invitee.canceled`
5. Save

Once that's done, every new booking will automatically trigger a WhatsApp confirmation!"

## Step 4: Set up booking confirmation

"Now let's set up the automatic WhatsApp message when someone books. Do you already have a WhatsApp template for booking confirmations?

If not, I can create one like:
_'Hi {{1}}, your {{2}} is confirmed for {{3}}. See you then! Reply if you need to reschedule.'_

Want me to create this template and set up the automation?"

Guide them through:
1. `create_whatsapp_template` for the confirmation message
2. `create_automation` with trigger_type `booking` to send it
3. Optionally create a reminder automation too
