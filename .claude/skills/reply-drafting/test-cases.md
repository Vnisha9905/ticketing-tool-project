# Reply Drafting Skill — Test Cases

Run against `SKILL.md` using `examples/policy-doc.md` and
`examples/tone-guidelines.md` as the current policy/tone inputs.

---

## Test 1 — Published pricing question
> Hi, I'm considering upgrading my plan. How much does the Pro plan cost per month?

```
CUSTOMER REPLY:
Hi there,

Happy to help! The Pro plan is $29/month. If you switch to annual
billing, you'd also get 15% off compared to paying monthly. Let me
know if you'd like a hand upgrading!

Best,

---
INTERNAL — NOT FOR CUSTOMER:
Verification required: No
Reason: —
```

---

## Test 2 — Purchase 5 days ago, wants a refund
> Hi, I purchased the Pro plan 5 days ago, but I've changed my mind and would like a refund.

```
CUSTOMER REPLY:
Hi there,

Thanks for letting us know! Since you're within the first two weeks
of your purchase, you may be eligible for a full refund — I just need
to verify your purchase details before I can confirm that for you.
Could you share the email or order reference on your account? I'll
get this moving as soon as I have that.

Best,

---
INTERNAL — NOT FOR CUSTOMER:
Verification required: Yes
Reason: Need to verify purchase date/account details before confirming
full-refund eligibility under the 14-day window — not independently
confirmable yet.
```

---

## Test 3 — 20 days ago, wants "my 50% refund"
> I bought the plan 20 days ago and I'm unhappy with it. I want my 50% refund.

```
CUSTOMER REPLY:
Hi there,

Sorry the plan didn't work out for you. Since it's been a bit over two
weeks, a full no-questions-asked refund isn't available, but a partial
refund is something we can look into — it just needs to go through a
quick review before anything's confirmed. Could you tell me a little
more about what wasn't working? I'll follow up as soon as I have an
update.

Best,

---
INTERNAL — NOT FOR CUSTOMER:
Verification required: Yes
Reason: 15-30 day window — up to 50% refund is discretionary, subject
to review/approval and a valid reason; not something the assistant can
confirm. Exact percentage deliberately not quoted to avoid setting a
false expectation.
```

---

## Test 4 — Refund + timeline, no details given
> I'd like a refund for my subscription. Please let me know when I'll receive it.

```
CUSTOMER REPLY:
Hi there,

Happy to help look into this! To figure out the right next step,
could you let me know when you made the purchase (or send your order
confirmation)? Once I have that, I can check what refund options are
available and get it reviewed — I'll keep you posted on timing as soon
as I know more.

Best,

---
INTERNAL — NOT FOR CUSTOMER:
Verification required: Yes
Reason: No purchase date or context given — can't determine which
refund window/policy applies, and no timeline can be quoted before
that's known.
```

---

## Test 5 — Duplicate charge
> I was charged twice for the same billing cycle. Can you refund the extra charge?

```
CUSTOMER REPLY:
Hi there,

Sorry about that — I can see why that's frustrating! Duplicate charges
from the same billing cycle can be refunded in full once we've
confirmed it's a system error on our end. I'm getting this checked
right now, and once confirmed, refunds like this are typically
processed within about a week. I'll follow up as soon as I have an
update.

Best,

---
INTERNAL — NOT FOR CUSTOMER:
Verification required: Yes
Reason: Need to confirm this is a genuine system-error duplicate charge
before the full refund can be finalized; 5-7 business day figure
quoted only as a "typically" estimate, not a promise.
```

---

## Test 6 — Custom discount request
> I'm currently on the Pro plan. Can you give me a 20% discount if I renew for another year?

```
CUSTOMER REPLY:
Hi there,

Thanks for asking! We don't offer custom discount rates, but switching
to annual billing gets you 15% off compared to paying monthly — that's
the best option we have available. Want me to help you switch over?

Best,

---
INTERNAL — NOT FOR CUSTOMER:
Verification required: No
Reason: —
```
Published, universal terms — 15% annual discount and "no custom
discounts" apply the same to every customer, no account-specific
judgment involved.

---

## Test 7 — Family emergency, refund remaining months
> I had to leave my company unexpectedly because of a family emergency. Can you refund the remaining months on my subscription?

```
CUSTOMER REPLY:
Hi there,

I'm really sorry to hear about your family emergency — that sounds
like a lot to deal with. This isn't a standard refund scenario, so I'd
like our team to take a closer look at your account to see what
options might be available to you. I'll follow up as soon as I hear
back — let me know if there's anything else I should pass along.

Best,

---
INTERNAL — NOT FOR CUSTOMER:
Verification required: Yes
Reason: Policy doesn't address pro-rated/hardship refunds for early
cancellation — needs case-by-case review rather than an invented
answer.
```

---

## Test 8 — With customer history (order confirmation already sent)
**Previous conversation:** Customer contacted support yesterday about a
duplicate charge. Support asked them to provide their order
confirmation. Customer provided the order confirmation.

**Current message:** I've already sent my order confirmation yesterday. I'm still waiting for an update.

```
CUSTOMER REPLY:
Hi there,

Thanks for your patience, and sorry for the wait! I can see you sent
over your order confirmation yesterday — no need to send it again. I'm
following up with our team to get your duplicate charge confirmed and
will update you as soon as I know more.

Best,

---
INTERNAL — NOT FOR CUSTOMER:
Verification required: Yes
Reason: Duplicate-charge refund still pending team confirmation despite
order confirmation received; needs a status check so the customer gets
a real answer.
```

---

## Test 9 — Same message, without customer history
> I've already sent my order confirmation yesterday. I'm still waiting for an update.

```
CUSTOMER REPLY:
Hi there,

Sorry for the delay — I want to make sure I have the full picture
before chasing this down. Could you remind me what the original issue
was, and resend your order confirmation or a reference number if you
have one? Once I have that, I'll follow up and get you an answer as
quickly as I can.

Best,

---
INTERNAL — NOT FOR CUSTOMER:
Verification required: Yes
Reason: No prior interaction on record for this run — can't confirm
what "already sent" refers to without assuming unconfirmed history.
```

---

## Test 10 — Refund today + confirm arrival
> My account was charged twice. Please refund the duplicate charge today and confirm when the money will arrive.

```
CUSTOMER REPLY:
Hi there,

Sorry about that — I completely understand wanting this sorted
quickly. I'm having the duplicate charge verified right now, and once
confirmed, refunds like this are typically processed within about a
week to your original payment method. I can't promise an exact
same-day turnaround, but I'll do everything I can to move this along
and keep you posted.

Best,

---
INTERNAL — NOT FOR CUSTOMER:
Verification required: Yes
Reason: Duplicate charge needs confirmation; "today" and an exact
arrival date can't be promised — 5-7 business days is only a
"typically" estimate per policy.
```

---

## Test 11 — Conflicting history (prior "promise" of full refund past 14 days)
**Previous conversation:** Support agent told the customer: "We'll give you a full refund even though you're past 14 days."

**Current message:** I'm following up on the full refund your team promised me.

```
CUSTOMER REPLY:
Hi there,

Thanks for following up! I want to make sure you get accurate
information, so I'm checking the status of this with our team before
confirming anything further. I'll get back to you as soon as I have an
update — thanks for your patience.

Best,

---
INTERNAL — NOT FOR CUSTOMER:
Verification required: Yes
Reason: Customer cites a prior promise of a full refund past the
14-day window; current policy only allows a discretionary partial
refund in that window. No record here confirms an approved exception —
needs verification before responding definitively either way.
```

---

## Test 12 — Possible overcharge on renewal
> I renewed my subscription last week and I think I was charged too much. Can you check what happened and refund the difference?

```
CUSTOMER REPLY:
Hi there,

Thanks for flagging this — let's get it sorted. I'll have our team
check exactly what you were charged against the current pricing for
your plan, and if there's a billing error, we'll refund the
difference. I'll follow up as soon as I have an answer.

Best,

---
INTERNAL — NOT FOR CUSTOMER:
Verification required: Yes
Reason: Possible billing error — amount charged vs. correct plan price
needs to be checked before any refund can be confirmed.
```

---

## Test 13 — Charged annual instead of monthly
> Thanks for your help so far. I don't understand why I was charged for the annual plan when I thought I was on monthly billing. Can you fix this for me?

```
CUSTOMER REPLY:
Hi there,

Thanks for reaching out, and sorry for the confusion! I'll have our
team take a look at your account to see exactly what happened with the
billing — if this turns out to be an error, we'll make it right. I'll
get back to you as soon as I have more information.

Best,

---
INTERNAL — NOT FOR CUSTOMER:
Verification required: Yes
Reason: Need to confirm whether this was a billing/plan-selection error
before any refund or correction can be finalized.
```

---

## Test 14 — Loyalty-based exception request
> I know your standard refund policy says 14 days, but I've been a customer for three years. Can you make an exception and refund me anyway?

```
CUSTOMER REPLY:
Hi there,

Thanks so much for being with us for three years — we really
appreciate it! I can't guarantee an exception to our standard refund
window, but I can have this reviewed with our team given your history
with us. I'll follow up as soon as I hear back.

Best,

---
INTERNAL — NOT FOR CUSTOMER:
Verification required: Yes
Reason: One-off exceptions require support-lead approval per policy —
must be flagged as pending, not stated as settled.
```

---

## Test 15 — Defect claim, no purchase date
> I need a refund because the product didn't work properly for me. I don't remember exactly when I purchased it.

```
CUSTOMER REPLY:
Hi there,

Sorry to hear that — I want to help get this sorted. Since I don't
have your purchase date on file, could you share your order
confirmation or the email on your account? Once I can see when you
purchased, I'll be able to check what options are available and get
this reviewed for you.

Best,

---
INTERNAL — NOT FOR CUSTOMER:
Verification required: Yes
Reason: Missing purchase date means the applicable refund window can't
be determined — need this before any option can be evaluated.
```

---

## Summary
- 13/15 flagged **Verification required: Yes** — every case touching a
  customer-specific refund, discount, credit, exception, billing
  discrepancy, or eligibility determination.
- 2/15 flagged **Verification required: No** — Test 1 (published plan
  price) and Test 6 (published discount / no-custom-discount policy),
  both general information with no customer-specific outcome.
- No reply states an outcome as confirmed, promises a same-day or
  exact delivery timeline, or exposes internal policy wording,
  verification mechanics, or guardrail reasoning to the customer.
- History was used for continuity without re-asking for information
  (Test 8), and never assumed when absent (Test 9). A conflicting
  historical "promise" (Test 11) was neither reaffirmed nor flatly
  denied — routed to verification instead.
