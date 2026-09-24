# Implement an approved context plan

Use this action for `/context implement <spec>`.

## Input

Resolve `<spec>` as follows:

- An exact Markdown path: use that file.
- `current-context`: use `context/current-context.md` from the repository root.

Do not guess between multiple possible specification files. If the supplied file does not exist, stop and report the unresolved path.

## Preconditions

1. Read the resolved specification completely.
2. Read the repository instructions that apply to every file the plan may change.
3. Confirm that the specification contains an implementation plan and that the user approved that plan in the current conversation or the specification records its approved status.
4. Inspect the working tree and the code directly relevant to the planned changes.

If the plan is missing, unapproved, internally inconsistent, or too ambiguous to implement safely, do not invent a replacement plan. Explain the precise issue and ask for the missing decision.

## Implementation workflow

1. Extract the plan steps, acceptance criteria, constraints, and required validation from the specification.
2. Implement the steps in dependency order. Keep changes within the approved scope and preserve unrelated user work already present in the repository.
3. Follow the repository's existing architecture and conventions. Inspect adjacent code before introducing a new pattern.
4. Validate each meaningful change with the narrowest relevant checks, then run the broader tests, build, lint, or type checks required by the plan or repository.
5. Review the final diff against the specification and acceptance criteria.

Fix ordinary implementation mistakes and test failures that remain inside the approved scope. If implementation reveals that the approved plan requires a material design change, broader scope, destructive action, or new external side effect, pause and request approval before proceeding.

Do not create branches, commits, pull requests, deployments, or external messages unless the user explicitly requested them.

## Completion

Report:

- The implemented outcome.
- The files or components changed.
- The validation performed and its result.
- Any approved-plan step or acceptance criterion that remains incomplete, with the blocker.
- Any material deviation from the approved plan.

Do not claim completion while a required step or validation remains unresolved.
