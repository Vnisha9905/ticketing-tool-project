# Escalation Triggers

Check these BEFORE classifying the rest of the ticket. If either group
matches, the ticket is an escalation: `escalate: true`, `priority: "P0"`.

## Live outage signals
- "down", "outage", "not working for everyone / all users"
- "500 error", "503 error", "service unavailable"
- "can't access the platform / site / app" (framed as widespread, not one user)
- "everything is broken", "total failure", "system is unresponsive"

## Legal/security signals
- "breach", "hacked", "unauthorized access", "data leak", "data exposed"
- "GDPR", "CCPA", "compliance violation"
- "subpoena", "lawsuit", "legal action", "cease and desist"
- "PII exposed", "personal data leaked", "security vulnerability"

## Rule
- Either group matching → `escalate: true`, `priority: "P0"`.
- Category becomes `Outage` (for outage signals) or `Legal/Security` (for
  legal/security signals) — this overrides any other category the ticket
  might otherwise suggest.
- If a ticket plausibly matches both groups, prefer `Legal/Security` as the
  category, since it's the higher-stakes concern.
- Neither group matching → `escalate: false`; classify and prioritize
  normally using `categories.md` and `priority.md`.
