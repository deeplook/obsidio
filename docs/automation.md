# Automation Guide

Obsidio is designed for scripting and local automation, not just interactive
terminal use.

## Stable Output Shapes

For scripting and MCP-style automation, prefer `--format` over parsing text
output.

- most read, list, and query commands support `--format json`
- row-shaped commands additionally support `--format csv` and `--format ndjson`
  where useful
- text remains the default for human terminal use

Stability expectations:

- path-bearing rows use `path`
- count-bearing rows use `count`
- note and title identifiers use `title` or a more specific field such as
  `tag`, `alias`, or `command`
- JSON and NDJSON schemas are intended to be automation-stable unless
  documented otherwise

## MCP Server

`obsidio-mcp` exposes vault and canvas operations as tools for AI clients via
the [Model Context Protocol](https://modelcontextprotocol.io).

Example:

```bash
obsidio-mcp
```

Claude Desktop configuration example:

```json
{
  "mcpServers": {
    "obsidio": {
      "command": "uv",
      "args": ["run", "obsidio-mcp"]
    }
  }
}
```

Current tool areas include:

- canvas nodes, edges, and rendering
- note read, section read/write, and property updates
- vault search, search-context, tasks, doctor, conflicts, orphans, and deadends
- structural queries
- bookmarks, snippets, and Bases helpers

## Skills

- `vault-doctor`, a maintenance skill that runs `obsidio vault doctor`, `missing-property`, `unresolved-embeds`, `duplicate-titles-aliases`, and `stale-linked`, then turns findings into a prioritized remediation report.
- `meeting-processor`, a workflow skill that reads a fresh meeting note, extracts tasks/decisions/follow-ups, normalizes frontmatter, updates a project base, and writes sections back into the note with `notes section-write`.
- `attachment-refactor`, a cleanup skill that finds orphan attachments, duplicate assets, and scattered media, then proposes or performs `attachment-move`, `attachment-rename`, and `attachment-dedupe`.
- `project-dashboard-builder`, a skill that inspects `.base` files, generates or updates Bases, runs `base-render`, and creates canvases from structural queries with `canvas from-query`.
- `workspace-curator`, a session-management skill that snapshots workspaces, opens the right tabs for a task, restores saved contexts, and prepares focused panes for writing/review.
- `research-vault-publisher`, a publishing/export skill that validates a vault, renders specific bases, exports EPUB/HTML/PDF bundles, and packages a shareable artifact.
- `schema-migrator`, a metadata-governance skill that applies schema files, renames properties, coerces types, normalizes tags, and produces before/after summaries.
- `agent-memory-bridge`, a Claude skill specifically for AI-assisted work: store tasks, prompts, results, logs, and status in notes; query them later via Bases, structural queries, and MCP tools.


## HTTP Server

The local browser server is also useful for automation. In addition to HTML
note pages, it exposes JSON endpoints such as:

- `/api/notes`
- `/api/note/<vault-relative-path>`
- `/api/tasks`
- `/api/search?q=<query>`
- `/api/graph`
- `/api/doctor`
- `/api/preview/<note-stem>`

## Good Automation Patterns

- use JSON or NDJSON output instead of scraping text tables
- prefer vault-relative paths when storing note references
- use the DQL and Base query commands for row-oriented workflows
- keep Obsidio as the source of truth for workspace, bookmark, and plugin state
  instead of editing `.obsidian` files directly
