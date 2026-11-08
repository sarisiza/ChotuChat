---
Date: 2026-11-08
Status: Not Started
Parent:
  - "[[MVP features]]"
---
# Home timeline
# Description
- `GET /api/v1/timelines/home`
- Infinite scroll + pull-to-refresh

## Subtasks
```dataview
TABLE Status
WHERE contains(Parent, this.file.link)
SORT file.name ASC
```
