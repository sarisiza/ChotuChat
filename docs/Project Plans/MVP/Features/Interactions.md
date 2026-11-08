---
Date: 2026-11-08
Status: Not Started
Parent:
  - "[[MVP features]]"
---
# Interactions
# Description
- Favourite: `POST /api/v1/statuses/:id/favourite`
- Boost: `POST /api/v1/statuses/:id/reblog`
- Reply: `POST /api/v1/statuses` with `in_reply_to_id`

## Subtasks
```dataview
TABLE Status
WHERE contains(Parent, this.file.link)
SORT file.name ASC
```
