# ChotuChat Knowledge Base

This Obsidian vault is the knowledge base for ChotuChat, an Android client for Mastodon. Use `[[wikilinks]]` for links between notes.

## Vault layout

- `Product/` - product vision, competitors, app design, and any other product design files
- `Architecture/` - documentation of the architecture decisions for each feature
- `Project Plans/` - one folder per version, with its plan and features
- `Templates/` - Obsidian templates

## Project Plans

Each version has this structure, using `Project Plans/MVP/` as the reference example:

```
Project Plans/
  <Version>/
    ChotuChat <Version>.md    # Plan note: the new features in this version
    <Version> features.md     # Kanban board listing those features
    Features/
      <Feature name>.md       # One note describing each feature
    Subtasks/
      <Subtask name>.md       # One note per subtask of a feature
```

### Creating a new version

1. Create the folder `Project Plans/<Version>/` with `Features/` and `Subtasks/` subfolders.
2. Create the plan note `ChotuChat <Version>.md`, following `ChotuChat MVP.md`: frontmatter with `Date` and `tags`, a goal callout, and the list of new features.
3. Create the board `<Version> features.md` from `Templates/Project board.md`.
   - In the `%% kanban:settings %%` block, add `"new-note-folder":"Project Plans/<Version>/Features"` so new cards create their notes in the right folder.
   - Add one card per feature from the plan note to `Not Started`.
4. Create a feature note for each feature, as described below.

### Feature notes

Every feature note lives in `Project Plans/<Version>/Features/` and follows `Templates/Feature.md`:

```markdown
---
Date: YYYY-MM-DD
Status: Not Started
Parent:
  - "[[<Version> features]]"
---
# <Feature name>
# Description

## Subtasks
```

- `Parent` must link back to the version's Kanban board.
- `Status` must match the board column: `Not Started`, `In Progress`, `Blocked`, or `Done`.
- The note's filename must match its board card, written as `- [ ] [[<Feature name>]]`.

The `## Subtasks` section of every feature note contains this Dataview query, as in `Templates/Feature.md`. Keep it intact:

`TABLE Status WHERE contains(Parent, this.file.link) SORT file.name ASC`

### Subtask notes

Every subtask note lives in `Project Plans/<Version>/Subtasks/` and follows `Templates/Task.md`.

- `Parent` must link to its feature note, as a list: `- "[[<Feature name>]]"`. The feature note's Dataview table finds subtasks through this link.
- `Status` uses the same values as feature notes.

## Kanban boards

Every Kanban board must follow `Templates/Project board.md`. Boards are Markdown files managed by the Obsidian Kanban plugin. When editing one by hand:

- Keep the `kanban-plugin: board` frontmatter and the `%% kanban:settings %%` block intact.
- Keep the columns `Not Started`, `In Progress`, `Blocked`, and `Done`, including the `**Complete**` marker under `Done`.
- When moving a card, update the feature note's `Status` too.
