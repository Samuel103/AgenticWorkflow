# Close the current context

Use this action for `/context end`.

Closing a context generates the project's configured closeout artifacts, resets `context/current-context.md`, and runs the repository-specific GitHub closeout process. It does not by itself prove that the work item is complete.

`<skill-root>` means the directory containing the `SKILL.md` that routed to this action. This keeps the workflow valid whether the skill is installed under `.codex`, `.github`, or another supported location.

## Preconditions

1. Locate the repository root.
2. Read `context/current-context.md` when it exists.
3. Read `<skill-root>/assets/current-context-template.md` and confirm that it exists and is not empty.
4. Read the `Release notes and resolution summary configuration` and `GitHub closeout process` sections in `<skill-root>/SKILL.md`.

If the canonical template is missing or empty, stop without changing the current context and report the problem. Do not reconstruct the template from memory.

If either configuration section is missing, still contains its angle-bracket placeholder, or does not state an exact action, stop before generating artifacts or resetting the context. Ask the skill's user to configure that section. An explicit instruction to perform no GitHub operation is valid configuration.

## Closing workflow

1. Determine whether `context/current-context.md` contains an active context or already matches the canonical template.
2. Before resetting an active context, retain the work-item reference, title, known implementation status, validation results, and unresolved items for the completion report.
3. Generate and validate the release notes and resolution summary exactly as specified by `Release notes and resolution summary configuration`. Use the active context before resetting it. If generation or validation fails, stop without resetting the context or starting the GitHub closeout process.
4. Replace `context/current-context.md` with the exact contents of `<skill-root>/assets/current-context-template.md`. If the current-context file is missing, recreate it from that template.
5. Verify that the resulting current-context file matches the canonical template.
6. As the final closeout step, follow `GitHub closeout process` exactly. Respect repository rules, authorization boundaries, required checks, and stopping conditions; do not infer missing Git or GitHub operations.

Do not modify `context/project-overview.md`, `context/rules.md`, implementation files, persisted specifications, or external work items unless a configured closeout section explicitly requires that exact change. Do not create an archive unless the user explicitly requested one.

If the current-context file already matches the template, make no write, do not generate artifacts or run the GitHub process, and report that no active context was found.

## Completion

Report:

- The work item or context that was closed, when available.
- The release notes and resolution summary created or updated, including their locations.
- Whether `context/current-context.md` was reset or was already empty.
- The last known implementation and validation status.
- The configured GitHub closeout operations performed and their result.
- Any unresolved work that existed when the context was closed.

Clearly distinguish "context closed" from "work completed."
