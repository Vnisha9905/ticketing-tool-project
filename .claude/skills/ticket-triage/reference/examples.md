# Worked Examples

## Example 1 — Normal ticket (no escalation)

**Input:**
> Subject: Can't update my credit card on file
> Body: Hi, I'm trying to change my payment method to a new card but the
> "update" button doesn't do anything when I click it. This is just for my
> account, nothing urgent, but I'd like to get it fixed before my next
> billing cycle.

**Output:**
```json
{
  "category": "Billing",
  "priority": "P2",
  "destination_team": "Billing Team",
  "escalate": false,
  "reason": "The customer cannot update their payment method, a billing-related issue affecting only one account with no urgent deadline."
}
```

## Example 2 — Live outage (escalation)

**Input:**
> Subject: URGENT - site is completely down
> Body: Nobody on our team can log in right now, we're getting a 500 error
> on every page. This has been going on for 20 minutes and it's affecting
> our entire company.

**Output:**
```json
{
  "category": "Outage",
  "priority": "P0",
  "destination_team": "Engineering",
  "escalate": true,
  "reason": "Multiple users are unable to access the platform and are receiving 500 errors, indicating a live, widespread outage."
}
```

## Example 3 — Legal/security (escalation)

**Input:**
> Subject: Data breach concern
> Body: We just discovered that some of our customer PII may have been
> exposed due to a misconfigured export. We need this looked at immediately,
> our legal team is asking questions.

**Output:**
```json
{
  "category": "Legal/Security",
  "priority": "P0",
  "destination_team": "Legal/Security Team",
  "escalate": true,
  "reason": "Customer PII may have been exposed due to a misconfiguration, a potential data breach requiring immediate legal/security attention."
}
```

## Example 4 — Feature request (low priority, no escalation)

**Input:**
> Subject: Would love a dark mode
> Body: Not a big deal, but it would be nice if the dashboard had a dark
> mode option. No rush at all.

**Output:**
```json
{
  "category": "Feature Request",
  "priority": "P3",
  "destination_team": "Product",
  "escalate": false,
  "reason": "The customer is requesting a new dark mode feature with no urgency, not reporting a problem."
}
```
