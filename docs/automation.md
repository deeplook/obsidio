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
