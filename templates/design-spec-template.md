# <Feature name> — Design

Date: <YYYY-MM-DD>

## Goal

<Two or three sentences in plain language. What the player or user will notice.>

## Constraints and assumptions

- <Project rule this feature must keep.>
- <Decision taken during the brainstorm, stated as a fact.>
- <Assumption about the existing code that the design depends on.>

## 1. Data

<New types and fields, with defaults chosen so existing content keeps working.>

| Asset / record | <field> | <field> |
|---|---|---|
| <name> | <value> | <value> |

## 2. <Component>

<What it is responsible for. Inputs, outputs, and what it must never do.>

## 3. <Component>

<Behaviour as a numbered sequence where order matters.>

## 4. Error handling

- <What happens on a missing or invalid input.>
- <What happens when a dependency disappears mid-operation.>

## 5. Testing

- **Automated:** <what each test asserts>.
- **Manual:** <what a person has to check, and how>.

## Out of scope

- <Related thing that is deliberately not being done.>

## Files

- New: `<path>`
- Edit: `<path>`
