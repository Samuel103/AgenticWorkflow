## Purpose

Diagnose the bug or defect currently loaded in `context/current-context.md` and record the investigation there. Stop after documenting the findings. Never implement, apply, or attempt a fix.

## Preconditions

- `context/current-context.md` must describe a specific active bug or defect.
- The objective and request must identify observable incorrect behavior or provide enough information to investigate it.
- If the context is missing, is not bug-related, or lacks essential diagnostic information, report the gap and stop without modifying any file.

## Investigation workflow

1. Read `context/project-overview.md`, `context/rules.md`, and `context/current-context.md`.
2. Inspect only the repository code, configuration, tests, logs, documentation, and version history needed to understand the reported behavior.
3. Reproduce or trace the issue when this can be done safely. Diagnostic commands must not intentionally alter tracked files, install dependencies, run migrations, update external systems, or invoke auto-fix or formatting behavior.
4. Distinguish verified facts from hypotheses. Support conclusions with concrete evidence such as reproduction results, relevant execution paths, logs, test output, or exact file locations. Record unresolved questions instead of inventing an explanation.
5. Add or replace only the `## Bug investigation` section in `context/current-context.md`, using the structure below. Preserve every other section exactly as it is.
6. Report the investigation result, evidence, confidence, and unresolved questions. Explicitly state that no fix was made.

## Bug investigation structure

Use these fields in the `## Bug investigation` section:

- **Status:** `Confirmed`, `Likely`, `Inconclusive`, or `Blocked`.
- **Observed behavior:** What currently happens.
- **Expected behavior:** What should happen, based on the loaded context or repository evidence.
- **Reproduction or trace:** The steps, command, input, or code path used to examine the issue, including whether it reproduced.
- **Evidence:** Concrete findings with relevant file paths, symbols, logs, or test results.
- **Root cause:** The confirmed cause, or a clearly labeled hypothesis with its confidence level.
- **Affected areas:** Components or behavior known or likely to be affected.
- **Open questions:** Remaining unknowns, or `None identified`.
- **Fix status:** `No fix attempted; investigation only.`

## Hard boundary

The only file this action may modify is `context/current-context.md`, and the only content it may change is the `## Bug investigation` section. Do not edit source code, tests, configuration, dependencies, generated artifacts, plans, or external work items. Do not propose an implementation plan; `/context plan` owns that work.
