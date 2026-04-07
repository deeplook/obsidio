# Development Guide

## Local Setup

```bash
uv sync
```

## Common Commands

```bash
make test        # run tests
make coverage    # tests + HTML coverage report
make lint        # ruff + mypy
make format      # ruff format + autofix
```

## Documentation Structure

- `README.md`: short project overview and entry point
- `docs/getting-started.md`: installation and first steps
- `docs/features.md`: feature inventory
- `docs/python-api.md`: public Python-facing guidance
- `docs/cli.md`: command overview and examples
- `docs/automation.md`: MCP, HTTP, and machine-readable output guidance
- `docs/development.md`: contributor-facing setup and project layout

## Misc

The distribution includes a `py.typed` marker, so type checkers can consume
Obsidio's inline annotations when the package is installed.
