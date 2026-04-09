---
name: appointment-followup
description: Daily check for completed appointments needing follow-up and due reminders
schedule: "0 10 * * *"
---

Run this task every morning at 10 AM to check on appointments and reminders.

## Step 1: Check appointments needing follow-up

Call `get_appointments` with `needs_followup: true`.

If any found, notify the user:
"📅 **Appointment follow-up check:**
[X] appointments need follow-up. Run `/webbai:appointments` to see details and send follow-up messages."

## Step 2: Check due reminders

Call `get_due_reminders`.

If any found, notify:
"⏰ **[X] reminders are due:**
[List contact names and brief context]

Reply to handle these, or I'll include them in your next follow-up run."

## Step 3: If nothing pending

"✅ All caught up — no appointments need follow-up and no reminders are due."
