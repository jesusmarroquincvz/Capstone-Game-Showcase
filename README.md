# AI Workflow Showcase

This folder is the **process**, not the product. The game itself is still in development and
is not part of this delivery, so there is no source code, no art, no scenes and no game design
document here.

## What is in this folder

| Path | What it is |
|---|---|
| [presentation/WarFront Blitz.pptx](presentation/WarFront%20Blitz.pptx) | The 5-slide overview deck (stack, MCP servers, process, multiplayer) |
| [01-stack-and-tools.md](01-stack-and-tools.md) | Engine, AI tools, and what each one was used for |
| [02-feature-workflow.md](02-feature-workflow.md) | The spec → plan → test-first → subagent → review → play-mode loop |
| [03-mcp-servers.md](03-mcp-servers.md) | The two MCP servers, how they were configured, and how much they were used |
| [04-docs-as-agent-context.md](04-docs-as-agent-context.md) | The handoff documents and phase gates that kept the agent on track |
| [05-3d-asset-pipeline.md](05-3d-asset-pipeline.md) | Concept image → generated mesh → Blender clean-up → Unity |
| [06-lessons-learned.md](06-lessons-learned.md) | What worked, what did not, and the gotchas worth knowing in advance |
| [07-prompt-examples.md](07-prompt-examples.md) | Real prompts from the project, grouped by what they were for |
| [templates/](templates/) | Blank versions of every document the workflow uses |
| [examples/](examples/) | Scrubbed real documents: a design spec, a plan excerpt, an execution ledger, agent memory notes |
| [config/](config/) | Example MCP and CodeGraph configuration |

## The project in numbers

| | |
|---|---|
| Team | One developer plus an AI coding agent |
| Engine | Unity 6.3 LTS, URP, C# |
| Platforms | iOS, Android, desktop |
| Game code | About 135 C# scripts, roughly 30,000 lines |
| Automated tests | About 60 edit-mode tests |
| Roadmap | 11 phases (0 to 10), each gated by a manual test checklist |

## The short version

1. **Write the plan down before the code.** A master plan with a fixed phase order, a rule that
   a phase is not started until the previous one passes its tests, and a short list of
   conventions the agent must follow in every phase.
2. **Give the agent hands and eyes.** One MCP server lets it operate the live Unity editor
   (recompile, run tests, enter play mode, take a screenshot). Another gives it an indexed map
   of the code. With both, the agent checks its own work before reporting it done.
3. **Run every feature through the same loop.** Brainstorm into a spec, turn the spec into
   small tasks, write the failing test first, let a fresh subagent implement each task, have an
   independent reviewer read the result, then confirm the behaviour in play mode.
4. **Keep a record.** A hand-kept ledger of each task, what was verified, and every judgement
   call that deviated from the plan.