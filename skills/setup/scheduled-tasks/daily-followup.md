# Daily Follow-up Check

**What it does:** Every afternoon, reviews your WhatsApp conversations to find unanswered messages and stale leads. Drafts replies and asks for your approval before sending.

**Schedule:** Daily at 2:00 PM (customizable)

**Cron:** `0 14 * * *`

**Task:** `Run the follow-up-agent: Check for unanswered WhatsApp messages and leads that need follow-up. Draft replies and suggest actions.`

**Requirements:**
- WhatsApp connected via Webbai
- At least some contacts or leads in your system
