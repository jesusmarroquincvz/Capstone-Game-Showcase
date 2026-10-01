# Execution ledger — plan: <path to plan>

Setup: <anything about the environment that changes how the plan runs. If it deviates from
the plan, write it as a Ruling.>

Pre-flight (shared interfaces):
- T1→T2: <names> — <match / mismatch and what was done>.
- T2→T3: <names> — <...>.

Task 1: complete (<files touched>; tests: <filter> → <n>/<n> pass)
Task 2: complete (<files touched>; tests: <...>). Ruling: <what was decided that the plan did
not say> — <reason> — cost if wrong: <what breaks and how bad>.
Task 3: <...>

Final review: <who reviewed, against what> — <n> Critical, <n> Important, <n> Minor;
verdict "<...>".
Final: Ruling: <finding that was declined, and why> — cost if wrong: <...>.
Final: minor (deferred): <finding, with the fix that would address it>.

Runtime evidence: <what was checked in the running product, and the observed values>.
Left to the developer: <checks that need a human>.
