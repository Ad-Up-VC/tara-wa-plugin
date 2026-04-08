# Daily Appointment Reminders

**Schedule:** Every day at 8:00 AM
**Cron:** `0 8 * * *`
**Skills used:** send-reminders

## What It Does

Every morning, checks the user's Google Calendar for today's appointments and sends a personalized WhatsApp reminder to each client who has a phone number in the event.

## Workflow

1. Use Google Calendar to fetch all events for today
2. For each event, extract:
   - Contact name (from attendee or event title)
   - Phone number (from description, notes, location, or attendee fields)
   - Appointment time (event start time)
   - Type (from event title — e.g., "Consultation", "Follow-up")
3. Skip events without phone numbers
4. Deduplicate by phone number (keep earliest appointment)
5. Format all phone numbers to E.164 (default +31 for Netherlands)
6. For each contact:
   - Call `generate_whatsapp_message` with name, time, and type
   - Call `send_whatsapp_message` to send the personalized reminder
7. Report summary of sent and skipped reminders

## Output Format

```
Sent 4 reminders for today's appointments:
- Sarah Johnson — 10:00 AM consultation
- Mike de Vries — 11:30 AM follow-up
- Lisa Bakker — 2:00 PM intake
- Tom Hendriks — 4:00 PM review

Skipped 1 (no phone number): Team standup at 9:00 AM
```

## Rules

- Do NOT ask for confirmation — send automatically (this runs unattended)
- Use `generate_whatsapp_message` for personalized messages, not generic text
- Always include the appointment time and type in the reminder
- If no appointments have phone numbers, report "No reminders to send today"
- Requires Google Calendar to be connected in Claude Settings → Connected Apps
