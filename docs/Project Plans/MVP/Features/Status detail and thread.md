---
Date: 2026-11-08
Status: Not Started
Parent:
  - "[[MVP features]]"
---
# Status detail and thread
# Description
- `GET /api/v1/statuses/:id/context`

## Subtasks
```dataview
TABLE Status
WHERE contains(Parent, this.file.link)
SORT file.name ASC
```
