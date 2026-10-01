# <Project> — Per-Phase Test Plan

> Rule: **do not advance to the next phase until the current phase passes every test below.**
> These are manual tests run in the editor and, where noted, on a device.

Legend: ▢ = a check to perform · **PASS** condition in bold.

---

## Phase 0 — <name>

▢ <Action>. **PASS: <what must be observed>.**
▢ <Action that stresses the design, e.g. force a low frame rate>. **PASS: <the property that
  must hold anyway>.**
▢ <Action>. **PASS: <...>.**

---

## Phase 1 — <name>

▢ <Action>. **PASS: <...>.**

---

## How to use this document

1. Build the phase.
2. Run every ▢ check for that phase. Anything failing → fix and re-test before continuing.
3. Only when all checks **PASS**, fine-tune if desired, then start the next phase.

## <Cross-cutting feature> (added with the feature)

<One paragraph on how it works.>

Test procedure:
1. Automated: <test group and count>.
2. Manual: <steps and what to look for>.
