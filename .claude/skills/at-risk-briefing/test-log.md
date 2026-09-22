# Test Log — at-risk-customer-briefing

**Purpose:** Verify the skill's behavior (`SKILL.md` +
`reference/signal-guide.md`, `synthesis-guide.md`, `output-template.md`)
produces correct, consistent, non-inventive Retention Briefings across a
range of realistic and edge-case inputs.

**Method:** Each customer case below was run through the actual skill
live — this is genuine model execution against the documented procedure
and reference files, not a script or simulation. Test 1 surfaced a real
issue in the skill's synthesis instructions, which was fixed in the
reference files themselves (not worked around in the output), and Test 1
was then re-verified against the corrected rule. Tests 2–5 ran against the
already-corrected version of the skill.

**Live execution:** 2026-08-23, Claude Sonnet 5, Claude Code.

---

## Test 1 — BrightDesk (C-1042): recurring issue + usage decline + billing lateness

**Input:** Billing showing progressively later payments over three months;
usage showing a steady three-month decline in active users; two support
tickets on the same underlying dashboard-performance issue, the second
still open with a customer comment tying it to reduced product use.

**What it validated:** correctly identified the two tickets (#4521, #4788)
as one recurring issue rather than two unrelated ones; used the
customer's own quote as direct evidence rather than paraphrasing it
stronger than stated.

**Issue found:** the initial output described the dashboard issue as the
"most likely root cause" of *both* the usage decline and the payment
delays. The usage-decline link was evidence-supported (the customer's own
comment ties the two), but the payment-delay link was only a same-period
coincidence with nothing in the source data connecting it to the
dashboard issue — an unsupported causal claim.

**Fix applied:** added a "Correlation vs. causation" rule to
`reference/synthesis-guide.md` (causal language — "root cause," "driver,"
"caused," "led to" — is only allowed when the source data explicitly
supports that specific link; same-period co-occurrence defaults to
correlation language), referenced it from `SKILL.md` step 4 and a new
Constraints bullet, added the same note to the relevant sections of
`reference/output-template.md`, and corrected two spots in
`reference/example.md` that modeled the same over-claiming pattern.

**Re-verified output (corrected bullet):** "The dashboard performance
issue is directly tied by the customer's own comment to reduced regular
use of the product... The payment delays occurred during this same window
but nothing in the data connects them to the dashboard issue
specifically, so that link should be treated as a coincidence in timing,
not a confirmed cause."

**Result:** PASS (after correction — this is the highest-value test in
the set, since a weaker implementation could plausibly bundle every
same-period signal into one causal narrative)

---

## Test 2 — Northstar Labs (C-2087): billing/balance contradiction, stable usage, same-period ticket

**Input:** Billing showing two failed May payments and a 12-days-late June
payment, but June is recorded as "paid" while the account also shows a
current $2,000 outstanding balance (an internal contradiction in the
source data itself). Usage flat/stable across the period. One May ticket
questioning an invoice amount (resolved) and one open June ticket about a
payment failure.

**What it validated:** surfaced the paid-vs-outstanding-balance
contradiction explicitly in "Data Gaps / Uncertainty" rather than
silently resolving it or picking one version; treated the May invoice
ticket and the same-month payment failures as correlated ("occurred in
the same billing cycle"), not as one causing the other; correctly used
the flat usage numbers as a finding in their own right (risk here is
billing-driven, not engagement-driven) rather than omitting them for
showing no decline.

**Result:** PASS

---

## Test 3 — Vertex Health (C-3154): no support ticket data, clean billing, near-stable usage

**Input:** Three months of on-time payments, a very slight (28→27→26)
usage dip explicitly described in the source as "broadly stable," and no
support ticket data at all.

**What it validated:** did not invent a risk narrative to justify the
account's already-flagged status; stated plainly that available data does
not show a clear driver of risk; flagged the entirely-missing ticket
source as the most consequential gap (one of the skill's three core
sources); used the template's "state plainly rather than omit" rule for
an empty "Key Unresolved Issues / Concerns" section.

**Result:** PASS

---

## Test 4 — cus_9F3kLp2Q: raw JSON input, two of three sources missing, one non-signal ticket

**Input:** A raw, truncated JSON fragment containing only a `tickets`
array with one closed, low-priority, CSAT-5 "how do I add a team member"
ticket. No billing data, no usage data, minimal customer identity (ID
only).

**What it validated:** parsed structured JSON input correctly with no
schema having been specified (per `SKILL.md`'s "no fixed schema" input
rule); did not treat the one available ticket as a risk signal, correctly
applying `reference/signal-guide.md`'s "routine how-to ticket, resolved
quickly, no complaint" as a non-signal; flagged the truncated/incomplete
JSON structure and the two entirely absent sources rather than treating
silence as evidence of nothing wrong.

**Result:** PASS

---

## Test 5 — Ashgrove Media (C-5521, synthetic): literal billing/usage contradiction

**Input:** Purpose-built test case (constructed for this test, since none
was supplied): billing shows a stable, fully-paid 10-seat plan with no
seat changes on record; usage logs show 42–45 active users per month over
the same period — a direct factual contradiction between the two sources,
not just a diverging trend. No ticket data supplied.

**What it validated:** stated both conflicting facts plainly without
assuming either source was wrong or stale; did not invent an explanation
(unlicensed sharing, an unrecorded upgrade, a tracking bug); surfaced the
contradiction explicitly in "Data Gaps / Uncertainty" per the
constraint in `SKILL.md` ("if sources conflict... surface the conflict...
rather than silently choosing one version"); kept "Overall Risk Picture"
honest that this account does not show the usual disengagement pattern
even though it is already flagged at risk.

**Result:** PASS

---

## Summary

| # | Customer | Scenario tested | Result |
|---|---|---|---|
| 1 | BrightDesk (C-1042) | Recurring issue + usage decline + billing lateness; triggered the correlation-vs-causation fix | PASS (after correction) |
| 2 | Northstar Labs (C-2087) | Internal billing contradiction, stable usage, same-period ticket correlation | PASS |
| 3 | Vertex Health (C-3154) | Missing ticket source, weak/no signals, honest "nothing found" | PASS |
| 4 | cus_9F3kLp2Q | Raw/truncated JSON input, two missing sources, one non-signal ticket | PASS |
| 5 | Ashgrove Media (C-5521, synthetic) | Literal billing-vs-usage factual contradiction | PASS |

**Status:** Confirmed by live execution across 5 customer scenarios
(2026-08-23, Claude Sonnet 5, Claude Code). One correction was made to
the skill's own instructions after Test 1 (correlation vs. causation,
applied to `reference/synthesis-guide.md`, `SKILL.md`,
`reference/output-template.md`, and `reference/example.md`), and Test 1
was re-verified against the corrected rule. No further changes were
required after Tests 2–5; all outputs stayed within the skill's
constraints (no invented data, no risk score/tag, contradictions and gaps
surfaced rather than resolved silently).
