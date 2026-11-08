# Bish Cleanup app

Property upkeep and handyman services for Lewis, Cowlitz, Clark and Thurston counties.

`index.html` is a single-file web app with admin, team and customer logins, quote and booking requests, a daily team schedule, a time clock with payroll CSV export, alerts and messaging.

## Where it runs

This version runs as a claude.ai artifact. Its data, logins and photos are saved through claude.ai's built-in `db` storage (`window.claude`), so it does not work when opened from GitHub Pages or a local file. This repo is the source backup.

To host it on your own site, replace the data layer (the `S.db` calls in the script) with a real backend such as Supabase or Firebase.

## Notes

- Passwords are salted and hashed in the browser. Role screens are enforced by the page, not by the database.
- Reminders and alerts only fire while someone has the app open. Push notifications or SMS when the app is closed need a backend.
