# Bug-Triage Agent Test Results

Two test runs of the `bug-triage` agent (`.claude/agents/bug-triage.md`), each
given a customer bug report to check against `sample-data/changelog.md`.

---

## Test 1: Known Issue Match

**Input:** `sample-data/bug_report_known_reworded.md` (Priya, Ops Lead)

**Tools used:** Read, Grep, Glob only — consistent with the agent's declared
`tools: Read, Grep, Glob` (read-only, no Edit/Write/Bash access).

**Full agent output:**

```
Status: known_issue
Matched entry: v4.12.3 (2026-08-14) — "Known Issue: Dashboard fails to fully
render for accounts with 10+ active integrations connected"

Confidence note: High confidence match. Customer describes a dashboard that
spins/hangs indefinitely on load, persistent across browsers and devices,
started recently, and explicitly notes 10+ connected tools (Slack,
Salesforce, Zendesk, Jira, etc.). This lines up precisely with the changelog
entry's root cause (timeout in the integrations summary widget for accounts
with 10+ active integrations) — same trigger condition (10+ integrations)
and same symptom (dashboard fails to render/hangs), just described in
customer language ("spins forever") vs. engineering language ("fails to
fully render... timeout").

Details from matched entry:
- Status: Known Issue (not yet fixed; root cause identified)
- Version: reported in v4.12.3 (2026-08-14); fix targeted for v4.13
- Workaround: Disabling the "Integrations Overview" widget on the dashboard
  prevents the hang

Searches tried:
- Read full changelog directly (file is small, ~4 releases) covering all
  entries
- Matched on symptom terms: "dashboard," "loading/spinner/hang," "fails to
  render"
- Matched on contextual detail: "10+ integrations" / "integrations summary
  widget"
- Considered alternative candidates (mobile app unresponsiveness in v4.11.8,
  SSO session expiry in v4.12.1) and ruled them out as unrelated to this
  symptom

Recommendation: Since this is a known, unfixed issue, suggest the customer
apply the workaround now — disable the "Integrations Overview" widget on
their dashboard — until v4.13 ships the fix. No new engineering ticket
needed.
```

**Correct against changelog?** ✅ Yes. `changelog.md` v4.12.3 contains exactly
this Known Issue entry (10+ integrations, integrations summary widget
timeout, workaround = disable "Integrations Overview" widget, fix targeted
for v4.13). The agent correctly matched despite zero literal keyword overlap
between "spins forever, can't get in" and "fails to fully render... timeout,"
and correctly ruled out the two other plausible-looking entries (mobile
unresponsiveness, SSO session expiry).

---

## Test 2: New Issue Write-up

**Input:** `sample-data/bug_report_new.md` (Marcus)

**Tools used:** Read, Grep, Glob only — consistent with the agent's declared
`tools: Read, Grep, Glob` (read-only, no Edit/Write/Bash access).

**Full agent output:**

```
Status: new_issue

Confidence note: The changelog (/Users/nisha/bug-triage-agent/sample-data/changelog.md)
contains only 4 releases (v4.12.3, v4.12.1, v4.11.8, v4.11.5) and none
mention bulk delete, row selection, checkboxes, or a Reports table deleting
the wrong item. The closest keyword hit — "Exported CSV reports occasionally
contained duplicate rows" (v4.12.3, Fixed) — is about CSV export
duplication, not about deletion or wrong-row targeting, so it's not a
meaningful match. No other entry relates to selection/index logic,
off-by-one behavior, or data loss in the Reports table.

Searches tried:
- Literal terms: "delete", "bulk", "select", "checkbox", "row"
- Broader/synonym terms: "report", "table", "index", "off-by-one", "wrong
  item"
- Full manual read of the changelog (only 4 entries total, so exhaustive)

Repro steps:
1. Open the Reports table (web app, Chrome, Windows 11).
2. Select multiple rows via checkboxes.
3. Click "Delete Selected."
4. Intermittently (~1 in 5 attempts, per reporter's estimate), a report
   immediately above the checked rows is also deleted, with no error shown,
   in addition to the intended selections.

Missing info:
- Exact number/position of rows selected when the extra deletion occurred
  (e.g., was the wrongly-deleted row adjacent, or could it be off-by-one in
  a paginated/sorted list?)
- Whether the table was sorted or filtered at the time (sorting/filtering +
  stale row index is a common cause of this class of bug)
- Whether pagination was involved (e.g., deleting near a page boundary)
- Browser/app version and account/workspace details
- Whether the issue reproduces in other browsers or only Chrome
- Whether other users on the team have seen the same issue
- Any relevant timestamps/report IDs for the two incidents (Tuesday and this
  morning) that engineering could correlate with backend delete logs
```

**Correct against changelog?** ✅ Yes. None of the 4 entries in
`changelog.md` relate to bulk delete, row selection, or wrong-item deletion
in the Reports table. The only entry with surface-level keyword overlap
("report") — the CSV export duplicate-rows fix in v4.12.3 — is a genuinely
different bug (export-time duplication vs. delete-time wrong-row removal),
and the agent correctly declined to force that match. Treating this as
`new_issue` with extracted repro steps and an explicit missing-info list
(rather than inventing details) is the correct outcome.

---

## Summary

| Test | Verdict | Tools used | Correct? |
|---|---|---|---|
| 1 — Priya (dashboard spinner) | `known_issue` → v4.12.3 | Read, Grep, Glob | ✅ |
| 2 — Marcus (bulk delete) | `new_issue` | Read, Grep, Glob | ✅ |

Both runs stayed within the agent's read-only tool scope and produced
verdicts that hold up against a manual read of `sample-data/changelog.md`.
