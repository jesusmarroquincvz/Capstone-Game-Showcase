# Documents as agent context

An agent starts every session knowing nothing about the project. The documents below are what
it read first, and they are why work could be picked up weeks later, on a different machine,
without re-explaining anything.

## The document set

| Document | Purpose | Who writes it |
|---|---|---|
| **Design specification** | What the game is. The source of truth for content. | Developer |
| **Architecture document** | The few decisions that shape everything, with reasoning and alternatives, each marked as signed off. | Agent proposes, developer approves |
| **Master plan** | One self-contained handoff file: snapshot, conventions, phase roadmap, current status, "how to continue". | Agent, updated after every phase |
| **Per-phase test plan** | A checklist of manual checks with explicit pass conditions. | Agent |
| **Editor steps** | Numbered manual wiring the developer does in the engine. | Agent |
| **Feature specs and plans** | One dated pair per feature (see [02-feature-workflow.md](02-feature-workflow.md)). | Agent, from a brainstorm with the developer |
| **Agent memory notes** | Short facts the agent should not rediscover. | Agent |

Only the structure of these is shared here. Blank versions are in [templates/](templates/).

## The master plan

The most useful single file. Its sections:

1. **Snapshot table.** Engine version, targets, hard performance targets, code root, and a
   *current status* row that says which phases are complete and what is next.
2. **Working conventions.** A short numbered list that applies to every phase.
3. **Confirmed decisions.** The architecture choices that are no longer open.
4. **Layering.** Which part of the code may depend on which.
5. **Performance contract.** The rules that keep the frame rate target reachable.
6. **Phase roadmap.** For each phase: goal, code to write, manual editor steps, test to pass.
7. **Current status.** What exists, what is waiting on verification.
8. **How to continue.** Five steps telling a new assistant what to read and what to do next.

Template: [templates/master-plan-template.md](templates/master-plan-template.md).

### Conventions that earned their place

These are the ones that were general enough to reuse on any project:

- **Ask, do not assume.** When a feature is ambiguous, ask the developer before building.
- **Phase gate.** Do not start a phase until the previous one passes all of its tests.
- **Deliver the manual steps.** Anything the developer must do by hand arrives as an exact
  numbered list with real names.
- **State the invariants as rules.** The project's architectural invariants (one-way data flow
  between simulation and presentation, one entry point for all gameplay actions, determinism)
  were written as short imperative rules, so the agent could be held to them in review.
- **Record decisions with dates.** Sections are stamped "signed off" or "complete, verified"
  with the date. Cuts are recorded too, with who decided.

### The roadmap is dependency-ordered

Each phase builds only on things already proven, and the plan says why the order is what it
is. Networking came late on purpose: the architecture made multiplayer a transport problem,
so it could wait until the single-player game worked end to end.

Each phase had the same four parts, which made progress easy to judge:

```
Goal · Code to write · Manual editor steps · Test to pass
```

### "As built" notes

After a phase shipped, its section was rewritten from "what we plan to do" to "what was
actually built", including what changed during playtesting and what was cut. That is what made
the plan trustworthy months later. A plan that still describes the original intent misleads
the next session.

## Phase test checklists

One checkbox per behaviour, each with its pass condition in bold. Written before the phase
is built, expanded when the code lands.

```
▢ <action to perform>. PASS: <what must be observed>.
```

Template: [templates/phase-test-checklist-template.md](templates/phase-test-checklist-template.md).

## Agent memory

A handful of notes, each one fact with a "why" and a "how to apply". The ones that paid off
were about the editor tooling rather than the game:

- how to drive a play-mode check through `eval` (it rejects `using` directives, so types must
  be fully qualified);
- that a setting applied through MCP was being overwritten every frame by the game's own
  bootstrap, and what to call instead;
- that the MCP connection drops briefly after every recompile and how to wait for it.

Each of these cost time to find the first time and no time afterwards.
Template: [templates/memory-note-template.md](templates/memory-note-template.md).
