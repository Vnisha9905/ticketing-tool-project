# Worked Example

This example shows one full pass through the skill: sample input data,
followed by the briefing it should produce. Use it to calibrate tone,
length, and how facts vs. synthesis should read.

## Sample input

**Customer context:**
Account: Meridian Logistics (Account ID AC-48213). Plan: Growth tier, 40
seats. Customer since March 2023 (about 2.5 years). Primary contact: Dana
Ruiz, Operations Manager.

**Billing history:**
- Paid on time from March 2023 through Feb 2026.
- April 2026 invoice: payment failed (card declined), retried successfully
  5 days later.
- June 2026 invoice: payment failed again, retried successfully 3 days
  later.
- July 2026: customer requested a downgrade from 40 seats to 25 seats,
  effective next renewal. Reason given in the request: "reassessing which
  teams are actually using this."
- No refunds or disputes on file. No current outstanding balance.

**Product usage logs:**
- Weekly active users averaged 34 of 40 seats from March 2023 to March
  2026.
- Starting April 2026, weekly active users declined steadily; by July 2026,
  averaging 14 of 40 seats.
- The reporting/analytics feature, previously used weekly by the ops team,
  has had no usage since May 2026.
- Last login recorded: August 10, 2026 (13 days before this briefing).

**Past support tickets:**
- Ticket #5521 (April 2026, Priority: High): "Reports are showing wrong
  totals for last month." Status: Resolved. Resolution note: "Identified a
  data sync issue, fixed on our end." No customer comment after
  resolution.
- Ticket #5602 (May 2026, Priority: High): "Still seeing incorrect report
  totals, this is the second time." Status: Resolved. Customer's final
  comment: "OK it looks right now but we've lost confidence in these
  numbers for planning."
- Ticket #5810 (July 2026, Priority: Medium): "Can you confirm if seat
  reduction will affect our historical data?" Status: Resolved, single
  reply.
- No escalations on file.

## Resulting briefing

```
# Customer Retention Briefing

## Customer
Meridian Logistics (Account ID AC-48213). Growth tier, 40 seats currently
(reducing to 25 at next renewal). Customer since March 2023 (~2.5 years).
Primary contact: Dana Ruiz, Operations Manager.

## Overall Risk Picture
Meridian's risk pattern centers on a repeated reporting-accuracy problem
that the customer directly tied to lost confidence in the data, alongside
a drop in usage and a seat downgrade during the same period. The account
is current on payments, but two recent card failures and the pending seat
reduction suggest the relationship has cooled since a stable first two
years.

## Why the Customer May Be at Risk
- Weekly active users dropped from an average of 34/40 seats to 14/40
  seats starting in April 2026, and this decline lines up closely with a
  reporting accuracy issue reported that same month.
- The reporting/analytics feature has had no recorded usage since May
  2026, despite being used weekly before that.
- The customer reported the same reporting-totals problem twice (April and
  May 2026); after the second fix, the customer stated they had "lost
  confidence in these numbers for planning" — this is a direct statement
  of diminished trust, not an inference.
- The customer has requested a seat reduction from 40 to 25, citing a need
  to "reassess which teams are actually using this," which is consistent
  with the usage decline already visible in the data.
- Two payment failures in three months (April and June 2026) is a new
  pattern for an account with no billing issues in its first two years.

## Customer History That Matters
Meridian was a stable, actively-used account for its first two years. The
pattern changes starting April 2026: a reporting accuracy issue was
reported and marked fixed, but recurred a month later, and the customer's
own comment indicates the second fix did not fully restore their
confidence in the reports. Usage of the reporting feature stopped entirely
after that second ticket, and overall weekly active users roughly halved
over the following months. The seat downgrade request in July, along with
two payment failures in the same window, both surfaced after this
sequence of events rather than before it.

## Key Unresolved Issues / Concerns
- Ticket #5602 was closed, but the customer's final comment expressed
  ongoing lack of confidence in report accuracy — there is no record that
  this concern was followed up on after the ticket was closed.
- No usage of the reporting/analytics feature has been recorded since May
  2026, and it is not confirmed whether the customer has resumed relying
  on it at all, or has replaced it with something else.

## What to Know Before the Retention Call
- The reporting accuracy issue appears to be the more significant concern
  relative to billing, based on the customer's own comment — leading with
  a billing-focused retention offer may miss the actual issue.
- The customer has not escalated or complained loudly; the risk signals
  here are behavioral (usage, downgrade) more than vocal, so the
  representative should not expect the customer to raise these concerns
  unprompted.
- The seat downgrade is already scheduled for the next renewal, so there
  is a concrete deadline context for this conversation.

## Data Gaps / Uncertainty
- There is no data confirming whether the reporting feature is genuinely
  fixed and simply unused, or still considered unreliable by the customer
  — this was not addressed after ticket #5602 closed.
- No information is available on whether other stakeholders at Meridian
  beyond Dana Ruiz are aware of or involved in the seat reduction decision.
```

## What to notice

- Every bullet in "Why the Customer May Be at Risk" is traceable back to a
  specific fact in the input, and cross-source points (usage decline plus
  the reporting ticket) are called out explicitly rather than left
  implicit.
- The customer's own words ("lost confidence in these numbers") are used
  as direct evidence, not paraphrased into something stronger than what
  was said.
- No risk score, tier, or label appears anywhere.
- "Data Gaps / Uncertainty" only lists things that are genuinely unknown,
  not a general disclaimer.
- The seat downgrade and payment failures are described as surfacing in
  the same window as the usage decline, not as being caused by it — the
  source data never states that connection, so the briefing stays at
  correlation. The reporting-to-trust link, by contrast, is stated more
  directly only because the customer's own comment supports it.
