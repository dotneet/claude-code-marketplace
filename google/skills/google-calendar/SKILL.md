---
name: google-calendar
description: Google Calendar + Tasks API access without MCP. Use when you need to read or modify calendars/events or tasklists/tasks using OAuth 2.0 and the bundled scripts.
---

# Google Calendar + Tasks Access

## Quick start

- Create a Google Cloud OAuth client (Desktop app) and save the credentials JSON to `~/.config/google-calendar/credentials.json`.
- Install dependencies: `python3 -m pip install -r <skill_dir>/scripts/requirements.txt`.
- Authenticate and store a token:
  - Calendar only:
    - `python3 <skill_dir>/scripts/gcal_auth.py`
  - Tasks only:
    - `python3 <skill_dir>/scripts/gcal_auth.py --scopes https://www.googleapis.com/auth/tasks`
  - Calendar + Tasks (single token):
    - `python3 <skill_dir>/scripts/gcal_auth.py --scopes https://www.googleapis.com/auth/calendar https://www.googleapis.com/auth/tasks`
- Call the API:
  - `python3 <skill_dir>/scripts/gcal_api.py list-calendars`

## Credentials and tokens

- Credentials are expected at `~/.config/google-calendar/credentials.json` by default.
- Tokens are stored at `~/.config/google-calendar/token.json` by default.
- Use `--token` or `GCAL_TOKEN_PATH` to switch accounts or isolate environments.

## Date/time rules

- Use RFC3339 for timed events (e.g., `2026-01-22T10:00:00-08:00`).
- Use `YYYY-MM-DD` for all-day events and set `end` to the next day (exclusive).
- Set `--time-zone` when the datetime has no offset.

## Common commands

- List calendars:
  - `python3 <skill_dir>/scripts/gcal_api.py list-calendars`
- List events:
  - `python3 <skill_dir>/scripts/gcal_api.py list-events --calendar-id primary --time-min 2026-01-22T00:00:00-08:00 --time-max 2026-01-22T23:59:59-08:00`
- Search events:
  - `python3 <skill_dir>/scripts/gcal_api.py list-events --calendar-id primary --q "standup" --time-min ... --time-max ...`
- Create event (simple):
  - `python3 <skill_dir>/scripts/gcal_api.py create-event --calendar-id primary --summary "Review" --start 2026-01-22T10:00:00-08:00 --end 2026-01-22T11:00:00-08:00`
- Update event (simple):
  - `python3 <skill_dir>/scripts/gcal_api.py update-event --calendar-id primary --event-id <id> --summary "New title"`
- Delete event:
  - `python3 <skill_dir>/scripts/gcal_api.py delete-event --calendar-id primary --event-id <id>`
- Free/busy:
  - `python3 <skill_dir>/scripts/gcal_api.py freebusy --calendars primary,team@company.com --time-min ... --time-max ...`
- List task lists:
  - `python3 <skill_dir>/scripts/gcal_api.py list-tasklists`
- List tasks:
  - `python3 <skill_dir>/scripts/gcal_api.py list-tasks --tasklist <tasklist_id>`
- Create task:
  - `python3 <skill_dir>/scripts/gcal_api.py create-task --tasklist <tasklist_id> --title "Buy milk" --due 2026-01-22T10:00:00-08:00`
- Update task:
  - `python3 <skill_dir>/scripts/gcal_api.py update-task --tasklist <tasklist_id> --task-id <id> --notes "Bring receipt"`
- Delete task:
  - `python3 <skill_dir>/scripts/gcal_api.py delete-task --tasklist <tasklist_id> --task-id <id>`

## Advanced usage

- Use `call` to hit any Calendar API endpoint:
  - `python3 <skill_dir>/scripts/gcal_api.py call GET /users/me/calendarList`
  - `python3 <skill_dir>/scripts/gcal_api.py call POST /calendars/primary/events --body-file /path/to/event.json`
- Use `--body-file` or `--body` (JSON string) for complex payloads (attendees, recurrence, conferenceData).
- Run multiple accounts by using different token files with `--token`.

## Safety

- Confirm intent before creating, updating, or deleting events.
- Keep OAuth credentials and token files out of git.
