# CLI Guide

The `obsidio` CLI covers vault analysis, note mutation, canvas operations,
exports, plugin and theme management, and automation-oriented queries.

Every listing command supports `--total` to return a count instead of a list.
Pass the vault path as a positional argument or set `OBSIDIAN_VAULT_PATH`.

## Command Map

```text
obsidio vault   info / files / folders / orphans / deadends
                tags / tasks / properties / property-set / property-remove
                property-rename / tags-normalize / schema-apply
                aliases / backlinks / attachment-backlinks / attachment-move
                attachment-rename / attachment-dedupe / attachment-import
                search / search-context / stats / export-meta / dataview
                templates / bookmarks / bookmark-add
                workspace / tabs / recents / workspace-open / tabs-set
                workspace-save / workspace-load / last-changes / conflicts / doctor
                plugins / plugin-enable / plugin-disable
                plugin-install / plugin-uninstall / plugin-reload
                plugin-updates / plugin-upgrade
                themes / theme-install / theme-set / theme-uninstall
                snippets / snippet-enable / snippet-disable
                commands / hotkey / folder / tag
                graph / serve / watch
                bases / base-views / base-query / base-inspect / base-render / base-create
                query / missing-property / no-frontmatter / unresolved-embeds
                duplicate-titles-aliases / stale-linked

obsidio notes   list / read / info / random
                append / prepend / create / delete / rename / move
                links / backlinks / tags / tasks
                aliases / properties / outline / sections / section-read / section-write / wordcount
                property-read / property-set / property-remove
                task-toggle
                urls / events / emoji

obsidio canvas  nodes / render / add-edge / remove-edge / edit-edge
                transform / layout / group / ungroup / from-query / to-pdf

obsidio daily   list / today / read / append / prepend

obsidio vaults     - list all Obsidian vaults registered on this machine
obsidio overview   - print a full map of all commands and their options
```

## Common Examples

```bash
# Vault summary
obsidio vault info /path/to/vault

# All tags with counts
obsidio vault tags /path/to/vault --counts

# Pending tasks across the vault
obsidio vault tasks /path/to/vault --no-done

# Dead wikilinks
obsidio vault deadends /path/to/vault

# Recently opened files
obsidio vault recents /path/to/vault

# Render an interactive link graph
obsidio vault graph /path/to/vault -o graph.html

# Notes changed in the last 3 days
obsidio vault last-changes /path/to/vault --duration 3d

# Full-text search with surrounding context
obsidio vault search-context /path/to/vault "machine learning" --context 2

# Query an Obsidian Base
obsidio vault base-query /path/to/vault -f "Book Library.base"

# Health-check the vault
obsidio vault doctor /path/to/vault --format grid

# Normalize metadata across the vault
obsidio vault tags-normalize /path/to/vault --lower --sort --dry-run

# Replace a single note section
obsidio notes section-write Projects/Roadmap.md "Next Steps" "## Next Steps\nUpdated\n"

# Build a canvas from a structural query
obsidio canvas from-query stale.canvas stale-linked --vault /path/to/vault --duration 30d

# Check for plugin updates
obsidio vault plugin-updates /path/to/vault --outdated

# Install a community plugin
obsidio vault plugin-install /path/to/vault dataview

# Browse notes as rendered HTML in the browser
obsidio vault serve /path/to/vault

# Export vault to HTML / PDF / EPUB
obsidio export /path/to/vault ./site
obsidio export /path/to/vault vault.pdf --format pdf
obsidio export /path/to/vault vault.epub --format epub
```

## Dataview DQL

`obsidio vault dataview` runs the supported offline Dataview DQL subset against
the vault. Supported query types are `LIST`, `TABLE`, `TASK`, and `CALENDAR`.
The output is a normalized row model, not Dataview's rendered UI.

Use `obsidio vault dataview --help` for the current command-level interface.

## Generated Command References

The `obsidio overview` command provides a comprehensive overview of the entire obsidio CLI, useful when you need to pass that information to the AI of your choice (below only the first few lines are shown):

```bash
$ obsidio overview
Application Overview
================================================================================

Application
  Name : obsidio
  Help : Headless Python interface to Obsidian vaults.

Global Options
Global       --install-completion : boolean  — Install completion for the current shell.
Global       --show-completion  : boolean  — Show completion for the current shell, to copy it or customize the installation.

Commands

  canvas [group]
    Help : Canvas operations.
    Sub-commands:

      add-edge
        Help : Add an edge between two canvas nodes.
        Arguments:
          canvas             : path [required]
          from_node          : text [required]
          to_node            : text [required]
        Options:
          --from-side        : text  — Source side.
          --to-side          : text  — Target side.

      edit-edge
        Help : Edit an edge in a canvas file.
        Arguments:
          canvas             : path [required]
          edge_id            : text [required]
        Options:
          --color            : text
          --from-end         : text
          --to-end           : text
          --from-side        : text
          --to-side          : text
[...]
````
