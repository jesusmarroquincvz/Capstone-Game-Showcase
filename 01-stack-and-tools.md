# Stack and tools

## Building the game

| Tool | Role |
|---|---|
| **Claude Code** | AI coding agent. Wrote and tested most of the C#, ran the editor through MCP, wrote plans and specs. |
| **VS Code** | Editor for the C# written by hand and for reading the agent's changes. |
| **Unity 6.3 LTS** (URP) | Game engine. One mobile and one desktop render pipeline asset as quality tiers. |
| **Unity Test Framework** | Edit-mode NUnit tests, run from the Test Runner or by the agent through MCP. |
| **Unity Relay** | Join codes for online play, so players never open ports or create accounts. |
| **Unity Version Control** (Plastic SCM) | Source control. The agent checked in through the `cm` CLI when asked. |
| **Xcode** | Signs and installs the iOS build; its gauges were the source of the thermal data in [case study 4](06-case-studies.md). |

## Agent tooling

| Tool | Role |
|---|---|
| **Unity Editor MCP** | Lets the agent operate the running editor. See [03-mcp-servers.md](03-mcp-servers.md). |
| **CodeGraph MCP** | Indexed symbol and call graph of the C# code, queried instead of grep-and-read. |
| **Superpowers skills** | Packaged workflows for brainstorming, plan writing, test-driven development, subagent-driven development and code review. See [02-feature-workflow.md](02-feature-workflow.md). |
| **Subagents** | A fresh agent per plan task, plus an independent reviewer at the end. |
| **Agent memory** | Short notes the agent keeps between sessions, mostly editor quirks it should not rediscover. |

## Making the 3D models

| Step | Tool |
|---|---|
| Concept image | ChatGPT image generation |
| Image to mesh | Meshy AI and Rodin AI |
| Clean-up | Blender |
| In game | Unity import |

Details in [05-3d-asset-pipeline.md](05-3d-asset-pipeline.md).

## Division of labour

The split that worked:

- **The developer** owns the game design, makes every design decision, does the art direction,
  plays the build on a real phone, and reports what feels wrong.
- **The agent** proposes architecture with reasoning for sign-off, writes code and tests,
  verifies in the editor, and writes down what it did.

The agent was never asked to decide what the game should be. Every ambiguous feature went back
to the developer as a question first; that rule is written into the master plan
(see [04-docs-as-agent-context.md](04-docs-as-agent-context.md)).
