# Product Changelog

## v4.12.3 — 2026-08-14
- **Fixed:** Exported CSV reports occasionally contained duplicate rows
  when filters were applied and the report exceeded 5,000 rows.
- **Known Issue:** Dashboard fails to fully render for accounts with
  10+ active integrations connected. Root cause identified as a
  timeout in the integrations summary widget. Workaround: disabling
  the "Integrations Overview" widget on the dashboard prevents the
  hang. Fix targeted for v4.13.

## v4.12.1 — 2026-08-02
- **Fixed:** Slack notifications were sent twice for comment mentions
  in shared workspaces.
- **Fixed:** Login session expired prematurely (~10 min) for SSO users
  on Safari.

## v4.11.8 — 2026-07-20
- **In Progress:** Some users report the mobile app becoming
  unresponsive after backgrounding it for extended periods on iOS 18.
  Engineering has reproduced intermittently; investigating memory
  handling on resume. No workaround yet.
- **Fixed:** Team member invites sent to email addresses with a "+"
  alias (e.g. user+test@domain.com) failed silently.

## v4.11.5 — 2026-07-05
- **Fixed:** API rate limit headers were missing from 429 responses,
  making client-side retry logic unreliable.
- **Fixed:** Custom report templates were not saving column reordering.
