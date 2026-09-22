---
name: at-risk-customer-briefing
description: Synthesizes billing history, product usage logs, and past support tickets for a customer who has already been identified as at-risk into a concise one-page Retention Briefing for a retention representative ahead of a call. Use whenever account information for a flagged at-risk customer has been gathered and needs to become a synthesized, human-readable briefing rather than a raw data dump.
---

# At-Risk Customer Briefing Skill

This skill takes information about **one** customer who has already been
identified, by another process, as at-risk. It produces a single one-page
Retention Briefing to prepare a retention representative for a call. It does
not decide whether a customer is at risk, does not search for or fetch data
from any system, and does not take any action — it only synthesizes what it
is given.

This is a bounded skill: one pass, one customer, one briefing. It does not do
autonomous investigation, does not choose which sources to consult, and does
not recommend what offer or action to give the customer.

## Input

Plain text describing the customer, organized into up to four blocks. Any
block may be partial or entirely missing — that is expected, not an error:

- **Customer context/identity** — name/account ID, company, plan or tier,
  tenure, other relevant account details
- **Billing history** — payments/invoices, late or failed payments,
  refunds/disputes, outstanding balances, significant billing changes,
  relevant dates and amounts
- **Product usage logs** — login/activity frequency, active users, feature
  usage, usage trends, significant increases or decreases, last activity
  date, adoption or drop-off signals
- **Past support tickets** — ticket dates, issues/complaints, priority and
  status, resolution, repeated issues, escalations, relevant customer
  comments, evidence that an issue may remain unresolved

There is no fixed schema. Read the input the way a person would read a case
file assembled from a CRM export, a usage dashboard, and a support ticket
log — the format of each source will vary.

## Procedure

1. **Read everything first.** Read all provided information in full before
   drafting any part of the briefing.
2. **Extract signals per source.** Use `reference/signal-guide.md` to
   identify what is genuinely relevant to retention risk in each of the
   three sources, and set aside data that is routine or expected and
   therefore not a signal.
3. **Cross-reference across sources.** Use `reference/synthesis-guide.md`
   to look for patterns that reinforce each other across billing, usage,
   and support (for example, a spike in failed payments coinciding with a
   drop in usage and an unresolved billing ticket). Also look for
   contradictions between sources (for example, usage climbing while a
   support ticket expresses strong dissatisfaction).
4. **Separate fact, evidence-supported synthesis, and correlation.** A
   fact is something directly stated in the source data. A synthesis is a
   conclusion drawn by connecting facts, and may only use causal language
   ("caused," "root cause," "driver," "led to") when the source data
   itself supports that specific causal claim. If two signals merely
   occur in the same period with nothing in the source connecting them,
   that is a correlation, not a cause — describe it as such ("coincided
   with," "during the same period as"). Never state an inference or a
   correlation as if it were a proven fact or a supported cause — see
   `reference/synthesis-guide.md` for how to phrase each.
5. **Identify unresolved issues.** Look for tickets without a clear
   resolution, disputes still open, repeated complaints about the same
   problem, or cross-source contradictions that were never reconciled.
6. **Note gaps honestly.** If something relevant is missing from the input,
   or two sources conflict, record it — do not fill the gap with an
   assumption or guess.
7. **Draft the briefing.** Follow `reference/output-template.md` section by
   section, in the order given.
8. **Keep it to one page.** Write for a representative who has a couple of
   minutes to read this before a call, not for an analyst preparing a
   report. Favor actionable insight over restating raw data.

## Output

A single Markdown document with these sections, in this order:

1. Customer Retention Briefing (title)
2. Customer
3. Overall Risk Picture
4. Why the Customer May Be at Risk
5. Customer History That Matters
6. Key Unresolved Issues / Concerns
7. What to Know Before the Retention Call
8. Data Gaps / Uncertainty (include only when something meaningful is
   missing or contradictory; omit the section entirely otherwise)

Full section-by-section guidance and a template are in
`reference/output-template.md`.

The output must be written in normal, readable business language. Do not
output JSON, code, database schemas, or technical/programming terminology.
Do not include a numeric score or a risk-level tag (e.g. "High/Medium/Low")
— the customer has already been identified as at-risk upstream; this
skill's job is to explain why and what matters, not to re-rank the risk.

## Constraints

- Do not invent information that is not present in the input. If something
  is not stated, it belongs in "Data Gaps / Uncertainty," not in the body
  of the briefing as if it were known.
- If sources conflict (for example, billing shows the account current but a
  support ticket references a failed payment), surface the conflict in
  "Data Gaps / Uncertainty" rather than silently choosing one version.
- Do not add a risk score, tier, or label of any kind.
- Do not describe one signal as the "root cause," "driver," or cause of
  another unless the source data explicitly supports that causal claim.
  Signals that merely occur in the same period are a correlation, not a
  cause — see "Correlation vs. causation" in `reference/synthesis-guide.md`.
- Do not recommend a specific retention offer, discount, or script — this
  skill informs the representative, it does not make retention decisions.

## Reference files

- `reference/signal-guide.md` — what counts as a meaningful retention-risk
  signal in each of the three sources, and what is routine noise to leave
  out
- `reference/synthesis-guide.md` — how to connect patterns across sources,
  distinguish fact from inference, and handle contradictions or unresolved
  issues
- `reference/output-template.md` — the exact section-by-section briefing
  template with writing guidance for each section
- `reference/example.md` — one fully worked example, from sample input data
  to a finished briefing

Load these as needed while drafting. Where a reference file gives specific
guidance, follow it rather than relying on general judgment alone.
