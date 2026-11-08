---
Date: 2026-11-08
Status: Not Started
Parent:
  - "[[MVP features]]"
---
# Profiles
# Description
- View account + its posts: `GET /api/v1/accounts/:id`, `GET /api/v1/accounts/:id/statuses`
- Follow / unfollow: `POST /api/v1/accounts/:id/follow`, `/unfollow`
- Relationship state: `GET /api/v1/accounts/relationships`

## Subtasks
```dataview
TABLE Status
WHERE contains(Parent, this.file.link)
SORT file.name ASC
```
