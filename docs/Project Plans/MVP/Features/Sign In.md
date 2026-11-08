---
Date: 2026-11-08
Status: Not Started
Parent:
  - "[[MVP features]]"
---
# Sign In
# Description
Pick a server and sign in.

- User types an instance domain; validate and show basic info with `GET /api/v2/instance`
- OAuth flow: `POST /api/v1/apps` → `/oauth/authorize` (Custom Tab) → `POST /oauth/token`
- Single account only

## Subtasks
```dataview
TABLE Status
WHERE contains(Parent, this.file.link)
SORT file.name ASC
```
