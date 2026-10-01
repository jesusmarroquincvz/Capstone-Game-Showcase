# MCP servers

Two MCP servers did most of the work of turning a code-writing assistant into one that can
check its own output.

## Unity Editor MCP: hands in the live editor

Connects the agent to the running Unity editor. The calls that were used most:

| Call | Used for |
|---|---|
| `recompile` / `recompile_status` | Compile after an edit and read the errors |
| `console` | Read errors and warnings from the editor console |
| `run_tests` | Run the edit-mode suite, or one filtered group |
| `editor_play` / `editor_stop` | Enter and leave play mode |
| `eval` | Run a C# snippet inside the editor: spawn things, issue orders, read state |
| `capture_game_view` | Screenshot the game view for layout and visual checks |
| `simulate_pointer` | Tap and drag in the game view |
| `open_scene` | Switch scenes for a test |

### How much it was used

Counted from the session logs of one six-day stretch (11 sessions, late in the project):

| Call | Count |
|---|---|
| `eval` | 230 |
| `capture_game_view` | 69 |
| `recompile` | 55 |
| `console` | 52 |
| `editor_play` + `editor_stop` | 60 |
| `run_tests` | 26 |
| Subagents started | 42 |

`eval` dominates because it is the general-purpose tool: almost every "does it really work"
question became a short snippet that set up a situation in play mode and read the result back.

### Before and after

The first half of the project was built without this server. The master plan from that time
has a rule that says the assistant cannot operate the Unity GUI, so every delivery had to
include a numbered list of manual editor steps for the developer, who then ran a checklist and
reported back.

With the server, the agent compiles, runs the tests, plays the scene and looks at the result
itself. The developer's manual work shrank to things that need a human: listening, feeling a
touch gesture, and testing on a real phone.

### A verification recipe

The pattern used for play-mode checks, with project names removed:

1. `editor_play` on a test scene.
2. One `eval` that spawns the objects needed and issues the order under test.
3. A second `eval` a moment later that reads back the state that should have changed.
4. `capture_game_view` if the result is visual.
5. `console` filtered to errors. Zero is the pass condition.
6. `editor_stop`.

For long-running behaviour (an AI opponent over ten minutes of match time), one `eval`
installs a log hook that appends the relevant lines to a scratch file and raises the time
scale, and the agent reads the file afterwards. Reading the console directly did not work
there because routine log lines buried the interesting ones.

## CodeGraph MCP: a map of the codebase

Indexes every C# symbol and call edge into a local graph. One query returns the source of the
relevant symbols, the call paths between them, and what depends on them.

What it changed:

- **Finding code** became one call instead of a grep-then-read loop.
- **Blast radius before editing.** The answer includes who calls the thing being changed, so
  the agent sees what an edit will affect before making it.
- **Fewer tokens spent on reading.** Only the relevant symbols come back, not whole files.

Setup is one config file that tells the indexer what to skip. For a Unity project that means
the generated and third-party folders: see [config/codegraph.json](config/codegraph.json).
Without those excludes, the generated build output swamps the index.

## Configuration

Both servers run locally over stdio and are registered once in the Claude Code config.
A sanitised example is in [config/mcp-servers.example.json](config/mcp-servers.example.json).

A standing instruction in the user-level `CLAUDE.md` tells the agent to reach for CodeGraph
before grep whenever the repository has an index. Without that line it tends to fall back to
reading files.
