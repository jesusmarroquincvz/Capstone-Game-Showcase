# <Feature name> Implementation Plan

> **For agentic workers:** execute this plan task by task, one fresh subagent per task.
> Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** <one sentence>.

**Architecture:** <one paragraph: the new pieces, what each owns, how they connect>.

**Tech stack:** <engine and framework versions, test framework, version control>.

**Spec:** `<path to the design spec>`

## Global constraints

- <Engine or tool version to use, and versions not to use.>
- <Where tests live and how to run them.>
- <Project rules every task must keep.>
- <Existing values or behaviour that must not change.>
- <Files that must not be edited for this feature.>

## Review focus

1. **<Situation likely to go wrong>**: <expected behaviour>. Pinned by <task and step>.
2. **<Situation>**: <expected behaviour>. Pinned by <task and step>.
3. **<Situation>**: <expected behaviour>. Pinned by <task and step>.

---

### Task 1: <name>

**Files:**
- Create: `<path>`
- Modify: `<path>` (<where in the file>)
- Test: `<path>`

**Interfaces:**
- Consumes: <names this task relies on, and which task produces them>.
- Produces: <names later tasks will use, spelled exactly>.

- [ ] **Step 1: Write the failing test**

  <Full test code.>

- [ ] **Step 2: Confirm it fails**

  <Command or tool call, and the failure to expect.>

- [ ] **Step 3: Implement**

  <Full code or an exact diff.>

- [ ] **Step 4: Recompile and run the tests**

  <Command or tool call, and the expected count.>

- [ ] **Step 5: Manual or play-mode check** (if any)

  <What to do and what to observe.>

- [ ] **Step 6: Commit**

---

### Task 2: <name>

<!-- same shape -->
