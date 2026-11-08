---
Date:
Status: Not Started
Parent:
---
# Task name
# Description

## Subtasks
```dataview
TABLE Status
WHERE contains(Parent, this.file.link)
SORT file.name ASC
```