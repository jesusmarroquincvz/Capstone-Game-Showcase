# CLAUDE.md snippet

Placed in the user-level `CLAUDE.md` so it applies to every project:

```markdown
## CodeGraph

In repositories indexed by CodeGraph (a `.codegraph/` directory exists at the repo root),
reach for it BEFORE grep/find or reading files when you need to understand or locate code:

- MCP tool (when available): `codegraph_explore` answers most code questions in one call:
  the relevant symbols' source plus the call paths between them. Name a file or symbol in the
  query to read its current line-numbered source.
- Shell (always works): `codegraph explore "<symbol names or question>"` prints the same output.

If there is no `.codegraph/` directory, skip CodeGraph entirely. Indexing is the user's decision.
```
