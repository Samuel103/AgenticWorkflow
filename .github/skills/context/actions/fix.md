## Purpose

Fix the active bug or defect using the completed investigation in `context/current-context.md`. Apply only the smallest correction supported by the recorded evidence, validate it, and record the outcome. Do not use this action for features or for speculative diagnosis.

## Preconditions

- `context/current-context.md` must describe a specific active bug or defect.
- Its `## Bug investigation` section must be complete and have a status of `Confirmed` or `Likely`.
- The investigation must contain concrete evidence, expected behavior, and either a confirmed root cause or a clearly labeled high-confidence hypothesis.
- The requested correction must fit the diagnosed scope without requiring a material design decision, broad refactor, destructive operation, or new external side effect.

If a precondition is not met, do not modify any file. Report the precise gap and direct the user to `/context investigate` or `/context plan`, whichever is appropriate.

## Fix workflow

1. Read `context/project-overview.md`, `context/rules.md`, and `context/current-context.md`.
2. Read the repository instructions that apply to the files implicated by the investigation. Inspect the working tree and relevant code so unrelated user changes are preserved.
3. Extract the observed behavior, expected behavior, evidence, root cause or hypothesis, affected areas, and open questions from `## Bug investigation`. Confirm that the intended change follows directly from those findings.
4. When feasible, add or update a focused test that demonstrates the bug before changing the implementation.
5. Implement the smallest correction that addresses the recorded cause. Avoid unrelated refactoring, cleanup, dependency changes, or behavior changes.
6. Run the narrowest relevant validation first, then any broader tests, build, lint, or type checks required by the repository rules or affected area.
7. Review the final changes against the loaded request and investigation. If validation reveals that the diagnosis is incorrect or that the fix needs materially broader scope, stop; do not continue by guessing. Preserve useful diagnostic evidence and report that `/context investigate` or `/context plan` is required.
8. Update only the fix-related entries in the existing `## Bug investigation` section of `context/current-context.md`. Preserve all investigation findings and every other context section. Set `Fix status` to the actual outcome and add concise `Fix summary` and `Fix validation` entries.

Ordinary implementation mistakes and test failures may be corrected only while they remain inside the diagnosed scope. Do not install dependencies, run migrations, deploy, modify external systems, create branches, commit, push, or open pull requests unless the user explicitly authorizes that exact action.

## Completion

Report:

- The correction made and how it addresses the recorded cause.
- The implementation and test files changed.
- The validation performed and its result.
- The updated fix status in `context/current-context.md`.
- Any unresolved behavior, failed validation, or deviation from the investigation.

Do not claim the bug is fixed unless the relevant validation passes. If no safe correction could be completed, state that clearly and leave `Fix status` as `Blocked` or `Attempted; not resolved`, as appropriate.
