---
name: ticket-triage-skill2
description: Reads a raw support ticket (subject + body as plain text) and produces a structured triage decision — category, priority, destination_team, escalate, reason — as strict JSON. Use whenever a new support ticket needs to be categorized, prioritized, and routed, especially to catch live outages or legal/security issues that need immediate escalation.
---

# Ticket Triage Skill

Take one support ticket as raw text input and produce exactly one structured
triage decision as JSON. This skill does not queue, send, integrate with a
ticketing system, or take any action beyond producing the decision — routing
and escalation are recommendations for a human or downstream system to act on.

## Input

A single ticket, given as plain text (subject and body may be combined in one
block, e.g. a pasted email or ticket description). There is no fixed schema
for the input — read it as a human would read a ticket.

## Procedure

1. **Read the ticket text** in full.
2. **Check escalation triggers first**, before classifying anything else.
   Load `reference/escalation.md` and check the ticket against both the live
   outage patterns and the legal/security patterns.
   - If either matches, this ticket is an escalation: `escalate` will be
     `true` and `priority` will be `P0`, regardless of what category it
     otherwise falls into.
   - If neither matches, proceed normally; `escalate` will be `false`.
3. **Classify the category.** Load `reference/categories.md` and pick the
   single best-fitting category for the ticket. If an escalation trigger
   fired in step 2, prefer the `Outage` or `Legal/Security` category
   accordingly, even if the ticket also mentions something else (e.g. a
   billing complaint about being locked out during an outage is still
   `Outage`).
4. **Map to a destination team.** Load `reference/teams.md` and use the
   category → team mapping. Do not invent a new team.
5. **Assign priority.** If step 2 triggered escalation, priority is `P0`.
   Otherwise, load `reference/priority.md` and assign `P1`, `P2`, or `P3`
   based on its criteria.
6. **Write the reason.** One concise sentence stating *why* this category,
   priority, and (if applicable) escalation were chosen — reference the
   specific words or situation in the ticket that drove the decision.
7. **Output the decision** as strict JSON only — no prose before or after,
   no markdown code fence unless the calling context expects one.

## Output format

Always exactly these five fields, in this shape:

```json
{
  "category": "Technical Issue",
  "priority": "P0",
  "destination_team": "Engineering",
  "escalate": true,
  "reason": "Multiple users are unable to access the platform, indicating a potential live outage."
}
```

- `category`: string, one of the categories in `reference/categories.md`.
- `priority`: string, one of `P0`, `P1`, `P2`, `P3`.
- `destination_team`: string, one of the teams in `reference/teams.md`.
- `escalate`: boolean, `true` or `false` (not a string).
- `reason`: one concise sentence, plain text.

## Reference files

- `reference/categories.md` — category definitions and how to recognize each
- `reference/teams.md` — category → destination team mapping
- `reference/priority.md` — priority level definitions (P0–P3)
- `reference/escalation.md` — live outage and legal/security trigger patterns
- `reference/examples.md` — worked example tickets with expected output

Load these as needed while triaging; do not guess at categories, teams, or
priorities that aren't defined in them.
