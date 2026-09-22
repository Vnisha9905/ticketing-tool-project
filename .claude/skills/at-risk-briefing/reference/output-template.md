# Output Template

The briefing always uses these section headers, in this order, written in
Markdown. Keep the whole document to roughly one page — dense enough to be
useful, short enough to read in a couple of minutes.

```
# Customer Retention Briefing

## Customer
[Basic identity/context: name or account ID, company, plan/tier, tenure,
and any other relevant account details available. If something is not
provided, do not guess it — simply omit it rather than writing "unknown."]

## Overall Risk Picture
[2-3 sentences. A plain-language summary of the overall situation: what
kind of risk this is (e.g. billing-driven, usage-driven, support-driven,
or a mix) and the general trajectory. No score or risk-level label.]

## Why the Customer May Be at Risk
[3-5 bullet points. Each one is the strongest evidence-backed signal
available, stated concisely. Where a point draws on more than one source,
say so — those cross-source points are usually the most important ones.
Use hedge language for synthesis, per synthesis-guide.md.]

## Customer History That Matters
[A short synthesized narrative or bullets covering the billing, usage, and
support history that provides context for the risk picture above. This is
not a full recap of every record — only what a representative needs to
understand how the account got here.]

## Key Unresolved Issues / Concerns
[Bullets listing specific unresolved items: open tickets, unconfirmed
resolutions, repeated complaints, open disputes. If there are none, state
that plainly rather than omitting the section.]

## What to Know Before the Retention Call
[Practical, forward-looking context: things the representative should be
ready to acknowledge, be careful about, or expect from the customer based
on their history. Not a script, and not a recommended offer — context.]

## Data Gaps / Uncertainty
[Only included when something meaningful is missing or contradictory.
Name specifically what is missing or which sources conflict, so the
representative knows what to verify. Omit this entire section if there is
nothing meaningful to flag.]
```

## Section-by-section notes

- **Customer**: Keep to what was actually provided. This section grounds
  the reader in who the briefing is about before they read anything else.
- **Overall Risk Picture**: This is the only place a broad summary
  statement belongs. It should be readable on its own, in case that is all
  the representative has time for.
- **Why the Customer May Be at Risk**: This is the evidentiary core of the
  briefing. Every bullet should be traceable to specific source data. Order
  points from strongest to weakest evidence. When a bullet connects two
  signals, use causal language ("caused," "root cause," "driver") only if
  the source data itself supports that specific causal claim; otherwise
  describe the signals as coinciding or occurring in the same period — see
  "Correlation vs. causation" in `synthesis-guide.md`.
- **Customer History That Matters**: This is synthesis, not a transcript.
  Group related facts together (e.g., describe the billing and usage
  pattern together if they are connected) rather than listing all billing
  items, then all usage items, then all ticket items, disconnected from
  each other. The same correlation-vs-causation rule applies here: do not
  narrate one event as having caused another unless the source data says
  so.
- **Key Unresolved Issues / Concerns**: Be specific enough that the
  representative could reasonably reference the issue if the customer
  brings it up.
- **What to Know Before the Retention Call**: This is where tone,
  sensitivities, and practical reminders go — for example, that the
  customer has already escalated once before, or that a specific promise
  was made to them previously.
- **Data Gaps / Uncertainty**: Do not use this section to hedge everything
  in the briefing. Use it only for genuinely missing pieces (e.g. no usage
  data was provided at all) or genuine contradictions between sources.

## Formatting rules

- Markdown only — headers, short paragraphs, and bullet lists.
- No JSON, code fences (other than this template file itself), tables of
  raw data, database/schema language, or technical jargon.
- No numeric risk score, percentage, or risk-level label anywhere in the
  document.
- No recommended retention offer, discount, or script.
