# Obsidio

(... coming soon... )

A headless Python interface to [Obsidian](https://obsidian.md) vaults, with a
CLI, local automation endpoints, and MCP support.

Obsidio lets you read, analyze, and manipulate an Obsidian vault without
running the Electron app. It is designed for Python workflows, terminal use,
and local AI tooling.

## Highlights

- Read and mutate notes, frontmatter, tags, tasks, links, sections, and daily
  notes
- Search and analyze vault structure, backlinks, conflicts, recent changes, and
  graph relationships
- Run offline Dataview DQL subset queries and Obsidian Base queries
- Manage plugins, themes, bookmarks, snippets, and workspace state
- Render and export canvases, plus export the vault as HTML, PDF, or EPUB
- Automate the vault through JSON-capable CLI commands, a local HTTP server, and
  an MCP server

## Install

Requires Python `3.12+` and [uv](https://docs.astral.sh/uv/).

```bash
git clone https://github.com/deeplook/obsidio
cd obsidio
uv sync
```

Install the CLI:

```bash
uv tool install .
```

## Quick Examples

Python:

```python
from obsidio import Graph, Vault

vault = Vault("/path/to/vault")
print(vault.tags(counts=True))
print(Graph(vault).orphans())
```

CLI:

```bash
obsidio vault info /path/to/vault
obsidio vault tags /path/to/vault --counts
obsidio vault doctor /path/to/vault --format grid
```

## Documentation

- [Getting Started](./docs/getting-started.md)
- [Feature Overview](./docs/features.md)
- [Python API Guide](./docs/python-api.md)
- [CLI Guide](./docs/cli.md)
- [Automation Guide](./docs/automation.md)
- [Development Guide](./docs/development.md)

## Development

```bash
make test
make lint
make format
```

## License

MIT
