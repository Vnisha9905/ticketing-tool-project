# Synthesis Guide

Guidance for connecting signals across the three sources into a coherent
picture, keeping facts and inferences clearly distinct, and handling
contradictions or unresolved issues honestly.

## Connecting patterns across sources

The most useful insights come from signals in different sources that point
at the same underlying story. When drafting, actively check billing, usage,
and support against each other:

- Did a usage decline start around the same time as a billing problem or a
  support ticket?
- Did a support ticket go unresolved, and did usage or payment behavior
  change afterward?
- Did a plan downgrade or failed payment follow a period of declining
  usage, or precede one?
- Do the customer's own words in a support ticket explain *why* a usage or
  billing pattern happened?

When two or more sources reinforce the same story, that combination is
almost always one of the strongest points in "Why the Customer May Be at
Risk" — it is stronger evidence than any single source alone.

## Fact vs. reasonable synthesis vs. correlation

Always be able to tell, sentence by sentence, whether a statement in the
briefing is a documented fact, an evidence-supported synthesis, a mere
correlation, or a genuine uncertainty (see "Correlation vs. causation"
below, and "Handling contradictions" and "Identifying unresolved issues"
for uncertainty). Do not let a correlation read as if it were an
evidence-supported synthesis, and do not let either read as a plain fact.

- **A fact** is directly stated in the source data: a date, an amount, a
  ticket status, a login count, a quoted or paraphrased customer comment.
- **A reasonable synthesis** is a conclusion drawn from connecting two or
  more facts, and should be phrased so the reader can tell it is an
  interpretation, not a certainty. Use language like "this suggests,"
  "this may indicate," "combined with," or "which coincided with," rather
  than stating the interpretation as settled fact.

Example:

- Fact: "The account had two failed payments in the last 60 days."
- Fact: "Logins dropped by roughly half over the same period."
- Reasonable synthesis: "The drop in usage coinciding with repeated failed
  payments suggests the account may be disengaging around the same time
  billing friction increased."

Do not present the synthesis sentence as if it were a fact on its own
("The customer is disengaging because of billing friction.") — keep the
hedge language that shows it is a connection you drew, not something the
data states outright.

## Correlation vs. causation

Two signals occurring in the same period does not, by itself, mean one
caused the other. Before writing any causal language, check whether the
source data itself states or clearly implies the causal link — not just
that the two things happened around the same time.

- **If the data explicitly supports the causal link** — a customer says
  they cut back "because of" something, a resolution note explains that a
  bug caused incorrect charges, a ticket comment directly ties one event
  to another — it is fair to state that connection as evidence-supported
  synthesis, using the hedge language described above ("suggests,"
  "appears to be connected to").
- **If the data only shows the two things happened around the same time,
  with nothing in the source connecting them** — treat it as a
  correlation, not a cause. Describe the signals as "coinciding,"
  occurring "during the same period," or "alongside" one another. Do not
  say one "caused," "drove," "led to," or is the "root cause" of the
  other.

Do not use causal language — including "root cause," "driver," "because
of," "led to," "resulted in," or "caused" — unless the source data itself
supports that specific causal claim. When in doubt, default to
correlation language: it is always defensible, while an unsupported
causal claim is not.

Example, given only that active users declined and payments became late
in the same two months, with no source statement connecting the two:

- Correlation (correct): "Active users declined the same two months that
  payments began arriving late. The two trends coincide, though the data
  does not indicate that one caused the other."
- Unsupported causal claim (avoid): "The decline in usage is the root
  cause of the late payments."

If a support ticket or customer comment later ties the two together
explicitly (e.g. the customer states billing problems are why their team
stopped logging in), that specific link can then be stated as
evidence-supported synthesis rather than mere correlation.

## Handling contradictions

Sources will sometimes appear to disagree — for example, billing shows the
account current while a support ticket references a failed payment, or
usage is climbing while ticket sentiment is negative. When this happens:

- Do not silently pick the source you think is more reliable.
- Do not average or blend the two into a single claim.
- State both facts plainly and flag the contradiction in "Data Gaps /
  Uncertainty," so the representative knows to verify before the call.

## Identifying unresolved issues

Treat an issue as unresolved when any of the following is true:

- A ticket's status is not "resolved" or "closed" in the source data.
- A ticket was marked resolved, but the customer's last comment expresses
  continued dissatisfaction or asks for further follow-up.
- The same underlying problem appears in more than one ticket, even if
  each individual ticket was closed.
- A dispute or refund request has no recorded outcome.

Unresolved issues belong in "Key Unresolved Issues / Concerns" even if they
seem minor — an unresolved issue is exactly the kind of thing a
representative needs to be aware of before opening a retention
conversation, so the customer is not surprised the rep doesn't know about
it.

## Keeping it actionable

For every point included in the briefing, ask: does this help the
representative going into the call? If a fact does not change what the
representative should say, ask, or watch out for, it likely belongs at most
in "Customer History That Matters" as brief context, not as a headline
signal.
