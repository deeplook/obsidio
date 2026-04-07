# Python API Guide

Obsidio is usable as a Python library, not just a CLI.

## Stable Top-Level Interface

The supported top-level API is the re-exported surface in `obsidio.__init__`:

```python
from obsidio import Vault, Note, Graph, Dailies
```

`Vault` and `Note` are the primary stable entry points for vault analysis and
note manipulation. Backwards-compatible changes to these documented public
methods are preferred; undocumented internals should be treated as private.

## Common Usage

```python
from obsidio import Vault

vault = Vault("/path/to/vault")
note = vault.note("Projects/Roadmap.md")

print(note.frontmatter)
print(note.tasks)
print(vault.search("roadmap"))
print(vault.stats())
```

## Vault Example

```python
from obsidio import Graph, Vault

vault = Vault("/path/to/vault")

for note in vault.notes():
    print(note.name, note.tags)

orphans = Graph(vault).orphans()
print("orphans:", len(orphans))

Graph(vault).render_html("graph.html")
print(vault.tags(counts=True))
```

## Notes Example

```python
from obsidio import Vault

vault = Vault("/path/to/vault")
note = vault.note("Projects/Roadmap.md")

print(note.urls)
print(note.events)
print(note.emoji)
print(note.inline_properties)
print(note.sections())
```

## Daily Notes Example

```python
import datetime

from obsidio import Dailies, Vault

vault = Vault("/path/to/vault")
daily = Dailies(vault).get(datetime.date.today())
print(daily.path if daily else "not found")
```

## Canvas Example

```python
from obsidio.canvas import JSONCanvas

c = JSONCanvas()
n1 = c.create_node(text="Start", x=0, y=0, color="4")
n2 = c.create_node(text="End", x=300, y=0, color="6")
c.connect_nodes(n1, n2)
c.save("pipeline.canvas")
c.render_svg_file("pipeline.svg")
```

## Dataview DQL

The Python API also exposes offline Dataview querying via:

```python
from obsidio.dataview import dataview_query
```

This evaluates a substantial local DQL subset and returns normalized Python
rows. It is not a render-level clone of the Dataview plugin UI.
