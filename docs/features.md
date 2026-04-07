# Feature Overview

## Vault And Notes

- Open a vault and navigate notes, folders, canvases, and files
- Read note content, frontmatter/properties, tags, tasks, wikilinks, aliases,
  and heading outlines
- Work with section trees via `note.sections()`
- Read and replace named sections from the CLI
- Parse Dataview-style inline metadata via `note.inline_properties`
- Extract URLs, inline datetime events `(@YYYY-MM-DD HH:MM)`, and emoji
- Compute word and character counts
- Search notes by exact text or fuzzy similarity
- Run structural vault queries such as:
  - missing properties
  - notes without frontmatter
  - unresolved embeds
  - duplicate titles or aliases
  - stale-but-linked notes
- Read recent files from workspace state
- Read recent note changes using flexible durations
- Detect Syncthing conflict copies
- Apply templates with variable substitution

## Note Mutations

- Create, delete, rename, and move notes
- Append and prepend note content
- Read, set, and remove individual frontmatter properties
- Batch set, remove, rename, and normalize metadata across a vault
- Apply YAML or JSON metadata schemas with preview support
- Toggle task checkboxes by line number

## Graph Analysis

- Backlinks
- Orphans
- Deadends
- Alias resolution
- Interactive HTML graph rendering with `pyvis`
- Graph export as JSON, GraphML, or GEXF

## Vault-Wide Aggregations

- Tag inventory with optional counts
- Frontmatter property inventory with optional counts
- Task listing across the vault
- Vault summary stats
- Frontmatter and inline metadata export
- Offline Dataview DQL subset queries
- Vault doctor checks
- Attachment backlink lookup, move, rename, import, and duplicate detection

## Daily Notes

- Get, create, and list daily notes
- Iterate over a date range
- Append and prepend to today's or a specified daily note

## Canvas

- Load, save, and manipulate `.canvas` files
- Add, update, remove, and search nodes and edges
- Auto-connect nodes
- Edit edges from the CLI
- Transform, auto-layout, group, and ungroup nodes
- Build canvases from structural query results
- Render to SVG
- Export to PDF

## Obsidian Bases

- Parse current YAML `.base` files
- Evaluate base filters and projections
- Run base queries and print JSON, CSV, table, or grid output
- Inspect normalized schema and unsupported expressions
- Render base views to Markdown or tabular output
- Create base files with an interactive wizard

## Plugin And Theme Management

- List installed and enabled community plugins
- Install plugins from the community registry
- Enable, disable, reload, uninstall, and upgrade plugins
- Detect plugin updates against GitHub releases
- List, install, switch, and uninstall themes

## Vault Configuration

- Bookmarks
- Commands and hotkeys
- CSS snippets
- Per-folder and per-tag statistics
- Workspace summary, tabs, recents, snapshots, and tab state updates

## Export

- Self-contained HTML export
- PDF export with math, Mermaid, page numbers, and a home page
- EPUB 3 export

## Automation

- Local browser server with structured JSON endpoints
- MCP server exposing vault, note, base, and canvas tools
- Automation-friendly CLI output with JSON, CSV, and NDJSON where relevant
