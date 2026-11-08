---
Date: 2026-11-08
Status: Not Started
Parent:
  - "[[MVP features]]"
---
# Local timeline
# Description
- `GET /api/v1/timelines/public?local=true`

## Subtasks
```dataview
TABLE Status
WHERE contains(Parent, this.file.link)
SORT file.name ASC
```
