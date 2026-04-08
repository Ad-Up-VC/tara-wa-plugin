# Daily Appointment Reminders

**What it does:** Every morning, checks your Google Calendar for today's appointments and sends a personalized WhatsApp reminder to each client who has a phone number.

**Schedule:** Daily at 8:00 AM (customizable)

**Cron:** `0 8 * * *`

**Task:** `Run /webbai:send-reminders`

**Requirements:**
- Google Calendar connected in Claude Settings
- WhatsApp connected via Webbai
- Clients' phone numbers stored in calendar event descriptions or attendee fields
