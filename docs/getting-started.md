# Getting Started

Obsidio is a headless Python and CLI interface to Obsidian vaults. You can use
it as:

- a Python library
- a local CLI
- a local HTTP server
- an MCP server for AI clients

## Requirements

- Python `3.12+`
- [uv](https://docs.astral.sh/uv/) for dependency management

## Install From Source

```bash
git clone https://github.com/deeplook/obsidio
cd obsidio
uv sync
```

Install the CLI into your tool environment:

```bash
uv tool install .
```

Build a wheel locally:

```bash
uv sync
uv build --wheel
```

## Quick Python Example

```python
import datetime

from obsidio import Dailies, Graph, Vault

vault = Vault("/path/to/vault")

for note in vault.notes():
    print(note.name, note.tags)

orphans = Graph(vault).orphans()
print("orphans:", len(orphans))

for mtime, note in vault.last_changes("7d"):
    print(mtime.strftime("%Y-%m-%d %H:%M"), note.name)

daily = Dailies(vault).get(datetime.date.today())
print(daily.path if daily else "no daily note yet")
```

## Quick CLI Example

```bash
# Vault summary
obsidio vault info /path/to/vault

# All tags with counts
obsidio vault tags /path/to/vault --counts

# Pending tasks across the vault
obsidio vault tasks /path/to/vault --no-done

# Dead wikilinks
obsidio vault deadends /path/to/vault

# Recently changed notes
obsidio vault last-changes /path/to/vault --duration 3d

# Health-check the vault
obsidio vault doctor /path/to/vault --format grid
```

## Where To Go Next

- [Feature Overview](./features.md)
- [Python API Guide](./python-api.md)
- [CLI Guide](./cli.md)
- [Automation Guide](./automation.md)
- [Development Guide](./development.md)
