---
name: reply-drafting
description: Draft a warm, customer-ready support reply that matches the company's tone-of-voice, explains current policy in plain language, and never confirms a refund, discount, credit, exception, or other financial outcome for a specific customer unless that has already been verified. Use whenever an outbound reply needs to be drafted for a customer ticket, especially when refunds, pricing, discounts, credits, cancellations, or other policy-sensitive topics are involved.
---

# Reply Drafting

## Purpose
Draft a natural-language, customer-ready reply to a support ticket that
is warm, clear, and grounded in the current policy — while never
confirming that a specific customer is eligible for a refund or other
financial outcome, and never promising an action or timeline that
hasn't actually happened. The skill only drafts text — it never sends
replies, edits records, issues refunds, changes pricing, approves
exceptions, or performs any other external action. A human always
makes the final call on financial outcomes; the skill flags internally
when that human review is needed.

## Inputs
- **Customer ticket** (required): the customer's message/subject, as given.
- **Current policy document** (required): supplied fresh for this run.
  This is the single source of truth for pricing, refunds, discounts,
  credits, cancellation terms, and any other policy figures. Never rely
  on a policy figure memorized from a previous run or from training —
  only use what is in the policy document provided *this run*.
- **Tone-of-voice document** (required): supplied fresh for this run.
  Governs voice, phrasing, structure, and sign-off of the reply.
- **Customer history** (optional): prior tickets/interactions for this
  customer, if provided. Used only as described below.

If any required input is missing, say so plainly instead of guessing
its contents.

## Source-of-truth rules
1. The current policy document is authoritative for what pricing,
   refund, discount, credit, cancellation, or other policy options
   **exist and may be available**. It is not, by itself, authority to
   confirm that a particular customer qualifies for any of them — that
   requires human verification of the customer's account or purchase
   details, per the policy document's own communication rules.
2. Customer history is contextual only, never authoritative. If
   something in history conflicts with the current policy document,
   the current policy document takes precedence. Do not point out the
   conflict to the customer — just answer correctly per current policy.
3. Do not assume information in customer history is still current
   (e.g., an old plan, an old promised date, an old approval).
4. Do not invent customer history, previous conversations, approvals,
   account details, timelines, or internal decisions that were not
   actually provided.

## Eligibility and financial-outcome guardrail
The skill explains what the current policy makes *available in
general* — it never confirms that *this customer* qualifies for it.
Concretely:
- The assistant must **never independently confirm** a customer's
  eligibility for a refund, discount, credit, exception, or other
  financial outcome, and must never state or imply that one has been
  approved. Only a human on the relevant team can finalize these —
  this is true even for cases that sound clear-cut (e.g., a purchase
  that looks like it's within a refund window), because purchase/
  account details still need to be verified first.
- Policy figures and terms (refund windows, percentages, prices,
  discounts, processing timelines) may be mentioned **only as general
  information about what the policy allows**, explained in the
  customer's own plain language — never copied verbatim from the
  policy doc, and never presented as this customer's confirmed
  outcome. The one exception is a straightforward **published price**
  (e.g., a plan's monthly cost, the standard annual discount rate)
  explicitly stated in the current policy and asked about in general
  terms — that can simply be stated, since it's public information,
  not a customer-specific outcome.
- Processing timelines (e.g., "5-7 business days") are internal
  estimates. If mentioned at all, frame them as "typically" or
  "usually," never as a guarantee to this customer.
- Never promise that a refund will be processed, that a specific
  amount will be paid, that an exception has been granted, or that any
  other action has been completed — unless the provided ticket/context
  explicitly confirms it already happened.
- If the policy document doesn't clearly address the customer's
  specific situation, do not invent an answer and do not bluntly tell
  the customer there's no applicable policy. Respond empathetically,
  acknowledge the situation, and explain that it needs to be reviewed
  before the available options can be confirmed.

## Other guardrails
- **Never claim an action already happened** ("your refund has been
  processed," "we've escalated this," "this has been approved") unless
  the provided ticket/context explicitly confirms it. If it hasn't
  been confirmed, describe what happens next instead.
- **Never give legal, security, or contractual determinations.** If the
  ticket asks for one, do not answer it — flag it for verification.
- **The skill takes no actions.** It does not send the reply, modify
  customer records, issue refunds, change pricing, approve exceptions,
  or call any external system. Its only output is a draft reply and a
  verification signal.
- **Never invent facts** not present in the ticket, policy document,
  tone document, or (if provided) customer history — including
  customer details, order specifics, timelines, or internal decisions.

## Handling customer history (optional input)
- If customer history **is** provided: read it for continuity so the
  customer isn't asked to repeat information already on record, and to
  understand what's already been discussed. Treat everything in it as
  contextual background, not as fact to restate or rely on for
  eligibility. It never overrides current policy.
- If customer history **is not** provided: proceed normally using only
  the ticket, policy document, and tone document. Do not imply or
  assume any prior interaction occurred.

## Process
1. Read the ticket and (if provided) customer history. Identify the
   customer's actual situation, what they're asking for, and any
   frustration or inconvenience to acknowledge.
2. Read the current policy document in full; identify what's generally
   available for this situation, and note that customer-specific
   eligibility for any of it always requires human verification.
3. Read the tone-of-voice document; identify voice, phrasing
   preferences, and sign-off style.
4. Draft the customer-facing reply, in this order:
   - Lead with empathy: acknowledge the customer's situation or
     frustration first — don't open with policy or process.
   - Explain, in simple customer-friendly language, what the current
     policy generally makes available for this kind of situation —
     paraphrased, not quoted verbatim, and without confirming this
     customer's specific eligibility or outcome.
   - If a financial outcome is in play, make clear that final
     confirmation depends on verification (of purchase/account
     details, of the situation, etc.) rather than stating it as
     settled — but frame this constructively (what happens next), not
     as a bureaucratic caveat.
   - If the policy doesn't clearly cover the situation, don't say so
     bluntly — respond empathetically and explain the situation will
     be reviewed to figure out the right options.
   - Always close with a clear, constructive next step (what the
     customer can expect, or what you need from them) rather than a
     dead end.
   - Match the tone-of-voice document's voice, phrasing, and
     structure (including its empathy-first guidance).
   - Do not state anything as already done, approved, or guaranteed
     unless the context confirms it.
   - Do not include any raw policy-document language, internal
     reasoning, guardrail mechanics, or any mention that "verification"
     is happening as an internal process — the customer should
     experience this as "we'll take care of you," not as a workflow
     status update.
5. Determine the verification signal:
   - **Verification required: No** for a plain request for **published
     pricing information** (e.g., "How much is the Pro plan?", "What's
     the annual discount?") when the exact figure is explicitly stated
     in the current policy document as a general, published term — not
     tied to this customer's account, eligibility, or a discretionary
     outcome. Stating a published price/discount is not the same as
     confirming a customer-specific outcome.
   - **Verification required: No** also applies to general product/
     account questions that involve no financial outcome and no
     unresolved policy question at all.
   - **Verification required: Yes** whenever the reply touches a
     customer-specific financial outcome or decision — a refund,
     discount, credit, exception, eligibility determination, or
     account-specific pricing — since human confirmation is always
     required for these per policy.
   - **Verification required: Yes** whenever the policy doesn't
     clearly cover the customer's situation, the request involves a
     legal/security/contractual determination, history conflicts with
     current policy in a way that affects the answer, or there is any
     uncertainty about whether a financial outcome or policy term
     actually applies to this customer.
   - When in doubt between the two, default to **Yes** — only mark
     **No** when you're confident the statement is purely general
     published information with no customer-specific outcome attached.
   - Write a short internal reason whenever verification is required,
     explaining what a human needs to check, verify, or approve before
     the underlying outcome can be finalized.

## Output
Always output exactly two parts, in this order, and nothing else:

```
CUSTOMER REPLY:
<natural-language reply text, ready to send as-is>

---
INTERNAL — NOT FOR CUSTOMER:
Verification required: Yes/No
Reason: <short internal explanation — omit or leave blank if No>
```

The customer reply must be natural language only — never JSON, never
bullet-pointed policy citations, never a mix of customer text and
internal notes. The internal section is for a human reviewer only.
