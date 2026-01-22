# Google Calendar + Tasks Direct CLI

This skill provides a lightweight Python CLI for direct Google Calendar and Google Tasks API access using OAuth 2.0.
It is useful for listing/creating/updating events and tasks without using the MCP server.

## Requirements

- Python 3.9+ recommended
- Google Cloud project with the **Google Calendar API** and **Google Tasks API** enabled
- OAuth client credentials (Desktop app)

Install dependencies:

```bash
python3 -m pip install -r .codex/skills/google-calendar/scripts/requirements.txt
```

## Credentials (OAuth client)

1. Open Google Cloud Console and select/create a project.
2. Enable **Google Calendar API** and **Google Tasks API**.
3. Configure the OAuth consent screen (External or Internal).
4. Create credentials:
   - **Create Credentials** → **OAuth client ID** → **Desktop app**
5. Download the JSON file (client secret).

Keep this file out of git and in a secure location.

## Authentication (token)

Authenticate and store a token:

- Calendar only:

```bash
python3 .codex/skills/google-calendar/scripts/gcal_auth.py \
  --credentials /path/to/client_secret.json
```

- Tasks only:

```bash
python3 .codex/skills/google-calendar/scripts/gcal_auth.py \
  --credentials /path/to/client_secret.json \
  --scopes https://www.googleapis.com/auth/tasks
```

- Calendar + Tasks (single token):

```bash
python3 .codex/skills/google-calendar/scripts/gcal_auth.py \
  --credentials /path/to/client_secret.json \
  --scopes https://www.googleapis.com/auth/calendar https://www.googleapis.com/auth/tasks
```

By default, the token is stored at:

```
~/.config/google-calendar-direct/token.json
```

You can override the token path with either:

- `--token /custom/path/token.json`
- `GCAL_TOKEN_PATH=/custom/path/token.json`

**Token management tips**

- Use different token files for different Google accounts.
- Remove the token file to force re-authentication.
- Tokens contain refresh tokens; keep them secure and out of version control.

## Environment variables

- `GCAL_CREDENTIALS`: default path to the client secret JSON.
- `GCAL_TOKEN_PATH`: default path for the OAuth token JSON.

## Common commands

List calendars:

```bash
python3 .codex/skills/google-calendar/scripts/gcal_api.py list-calendars
```

List events:

```bash
python3 .codex/skills/google-calendar/scripts/gcal_api.py list-events \
  --calendar-id primary \
  --time-min 2026-01-01T00:00:00-08:00 \
  --time-max 2026-02-01T00:00:00-08:00
```

Create an event:

```bash
python3 .codex/skills/google-calendar/scripts/gcal_api.py create-event \
  --calendar-id primary \
  --summary "Review" \
  --start 2026-01-22T10:00:00-08:00 \
  --end 2026-01-22T11:00:00-08:00
```

List task lists:

```bash
python3 .codex/skills/google-calendar/scripts/gcal_api.py list-tasklists
```

List tasks:

```bash
python3 .codex/skills/google-calendar/scripts/gcal_api.py list-tasks \
  --tasklist <tasklist_id>
```

Create a task:

```bash
python3 .codex/skills/google-calendar/scripts/gcal_api.py create-task \
  --tasklist <tasklist_id> \
  --title "Buy milk" \
  --due 2026-01-22T10:00:00-08:00
```

## Date/time rules

- Timed events/tasks use RFC3339 (e.g., `2026-01-22T10:00:00-08:00`).
- All-day events use `YYYY-MM-DD` and end on the next day (exclusive).
- Use `--time-zone` when the datetime lacks an offset.

## Safety

- Confirm intent before creating/updating/deleting events or tasks.
- Keep OAuth credentials and token files out of git.

