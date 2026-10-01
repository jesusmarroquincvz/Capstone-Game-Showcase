# The feature workflow

Every non-trivial feature went through the same five steps. Small fixes skipped straight to
"describe the bug, let the agent reproduce it, fix, verify".

```
 1 Spec          2 Plan            3 Test first      4 Implement         5 Review
 brainstorm  →   small tasks   →   failing test  →   fresh subagent  →   independent reviewer
 into a doc      with files        before code       per task            + play-mode check
```

## 1. Spec

Start with a rough request in plain language. The brainstorming skill makes the agent ask
questions one at a time until the open decisions are closed, then write a dated design
document.

What a good spec contained:

- **Goal** in two or three sentences, in the developer's words.
- **Constraints and assumptions**, including the ones that came out of the questions.
- A numbered section per component: data, behaviour, error handling.
- **Testing**: what is covered by an automated test and what has to be checked by hand.
- **Out of scope**, stated explicitly.
- **Files** that will be created or edited.

Template: [templates/design-spec-template.md](templates/design-spec-template.md).
Scrubbed real one: [examples/design-spec-example.md](examples/design-spec-example.md).

## 2. Plan

The plan-writing skill turns the spec into tasks an agent with no prior context can execute.
Each plan has:

- A header: goal, architecture in one paragraph, tech stack, link to the spec.
- **Global constraints** that apply to every task (engine version, where tests live, rules that
  must not be broken, numbers that must not change).
- **Review focus**: the four or five situations most likely to go wrong, each with the expected
  behaviour and the task that pins it down. This list is what the reviewer reads first.
- **Tasks**, each with the exact files, the interfaces it consumes and produces, and
  checkbox steps.

The "interfaces" lines matter more than they look. Before execution, the agent walks every
task-to-task handoff and confirms that the names one task produces are the names the next
task uses. That check caught mismatches before any code was written.

Template: [templates/implementation-plan-template.md](templates/implementation-plan-template.md).
Scrubbed excerpt: [examples/implementation-plan-excerpt.md](examples/implementation-plan-excerpt.md).

## 3. Test first

Each task that can be tested starts by writing the test and confirming it fails (in Unity,
usually by failing to compile). Only then is the implementation written.

What made this practical in a Unity project:

- **Pull the pure logic out of MonoBehaviours.** Layout maths, AI decision arithmetic and audio
  clip generation each live in plain C# that an edit-mode test can call with no scene loaded.
  The component only wires that logic to the engine.
- **Know where tests can live.** Code in the default assembly cannot be referenced from a test
  assembly definition, so tests for it sit in an `Editor` folder. New, self-contained modules
  get their own assembly definition and a matching test assembly.
- **Test invariants, not pixels.** For UI: "no two rows overlap" and "the grid has the right
  number of columns". For audio: "every loop is exactly one second and the seam does not
  click". For data: "each definition asset carries the expected value".

## 4. Implement with a fresh subagent per task

The main session acts as coordinator. For each task it starts a new subagent with only that
task's text and the global constraints. The subagent writes the code, recompiles through MCP,
runs the task's tests, and reports back.

Why a fresh agent each time: it has no memory of the previous task's dead ends, it cannot
quietly depend on something that is not written in the plan, and the coordinator's context
stays small enough to keep the whole feature in view.

The coordinator keeps a ledger: one line per task with what changed and what was verified, plus
a "Ruling" line whenever something deviated from the plan, stating the cost if the ruling
turns out to be wrong. Scrubbed real one: [examples/execution-ledger-example.md](examples/execution-ledger-example.md).

## 5. Review, then verify in the running game

After the last task, a reviewer subagent that has seen none of the implementation
conversation reads the full set of changed files against the spec and grades findings as
Critical, Important or Minor. Critical and Important findings get fixed. Minor ones are
written into the ledger as deferred, with the reason.

Last, the coordinator checks behaviour in play mode through the Unity Editor MCP: enter play
mode, set up the situation, read back state, take a screenshot. Anything it cannot check
(how something sounds, how a gesture feels on a phone) is listed for the developer.

## When the loop was skipped

- **Bug reports** with a screenshot or log: the agent reproduces, finds the cause, fixes,
  verifies. No spec.
- **Feel tweaks** ("I prefer the minimap at the bottom in portrait"): direct change plus a
  screenshot.
- **Investigations** ("the phone gets hot, tell me what the issues are before changing
  anything"): findings first, developer chooses which fixes to apply.
