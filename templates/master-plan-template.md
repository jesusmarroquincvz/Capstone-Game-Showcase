# <Project> — Master Build Plan (Handoff Document)

> **Purpose:** a single, self-contained plan for building this project end to end. Written so
> a developer or an AI assistant can pick up at any phase and continue without needing other
> documents.
>
> **Source of truth for content:** `<design spec file>`. Re-read it before building any feature.

---

## 0. Snapshot

| | |
|---|---|
| **Product** | <one line> |
| **Engine / stack** | <versions> |
| **Targets** | <platforms> |
| **Hard targets** | <measurable performance and feature targets> |
| **Version control** | <system> |
| **Code root** | `<path>` |
| **Current status** | **Phases 0–N COMPLETE** (verified <date>). **Now: Phase N+1 — <name>.** |

### Working conventions (apply to every phase)

1. **Ask, don't assume.** When a feature is ambiguous, ask before building.
2. **Phase gate.** Do not start a phase until the previous phase passes all its tests.
3. **Manual steps.** Every delivery includes an exact, numbered list of anything the developer
   must do by hand, with real names.
4. <Architectural invariant written as a rule.>
5. <Architectural invariant written as a rule.>
6. <Architectural invariant written as a rule.>

---

## 1. Confirmed architecture decisions (signed off <date>)

- **A. <Decision>:** <what was chosen, and what was rejected>.
- **B. <Decision>:** <...>.
- **C. <Decision>:** <...>.

---

## 2. Layering

```
<layer>
   └─> <layer>
          ├─ <layer>
          └─ <layer>
```

**Invariant:** <the one rule about dependency direction>.

---

## 3. Folder structure

```
<root>/
  <folder>/   <what lives here>
  <folder>/   <what lives here>
```

---

## 4. Performance contract

- <Rule that keeps the hard target reachable.>
- <Rule.>
- **Verification:** <the stress test and the device it runs on>.

---

## 5. One-time project setup

1. <Setting and where to find it.>

---

## 6. Phase roadmap

Each phase has: **Goal · Code to write · Manual steps · Test to pass.** Order is
dependency-driven. A phase is done only when its test passes.

### Phase 0 — <name>  *(status)*
- **Goal:** <one sentence>.
- **Code:** <components to write>.
- **Manual steps:** <what the developer wires by hand>.
- **Test:** <observable pass conditions>.

### Phase 1 — <name>  *(COMPLETE — verified <date>)*
- **Goal:** <...>.
- **Code (as built):** <rewrite this after shipping to describe what actually exists>.
- **Playtest changes (<date>, signed off):** <what changed after playing, what was cut and
  who decided>.
- **Known simplifications (on purpose):** <...>.
- **Test:** <...>.

<!-- repeat per phase -->

**Why this order:** <one paragraph on the dependency reasoning>.

---

## 7. Current status

**Written:** <what exists>.
**Awaiting verification:** <what the developer still has to check>.
**Next:** <the next phase, and the condition for starting it>.

---

## 8. How an assistant should continue

1. Read the design spec and this file.
2. Confirm the current phase from §7 and the test plan.
3. Implement the next phase's **Code**, keeping the layering (§2) and conventions (§0).
4. Deliver, alongside the code, the exact manual steps and the test steps for that phase.
5. Do not advance until the developer confirms the phase's tests pass. Ask when anything is
   ambiguous.
