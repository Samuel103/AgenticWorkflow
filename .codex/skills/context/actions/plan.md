## Purpose

Turn the work item loaded in `context/current-context.md` into a clear, ordered, and explicitly approved implementation plan. Planning must take place in Codex or Copilot Plan mode. After approval, let the user choose how the plan is stored.

## Required Codex or Copilot mode

- The planning and approval phases may run only when Codex or Copilot is already in Plan mode.
- If Plan mode is not active when starting or revising a plan, stop immediately. Do not inspect the repository and do not modify files.
- Tell the user to run `/plan` to enable Plan mode, then run `/context plan` again.
- Do not claim to switch modes on the user's behalf. The user must activate Plan mode through the coding assistant's interface.
- The only exception is the persistence phase described under **Mode and write limitations**. That phase may run outside Plan mode because it stores an already-approved plan without performing further planning.

## Preconditions

- `context/current-context.md` must describe a specific work item.
- The objective and request must contain enough information to plan the work responsibly.
- The work item must provide enough acceptance criteria or expected outcomes to determine when implementation is complete.
- If the work item is a bug or defect, its `## Bug investigation` section must contain completed findings from `/context investigate`, including evidence and a root cause or clearly labeled hypothesis. A template, `Not performed`, `Blocked`, or otherwise incomplete investigation does not satisfy this precondition.
- If essential information is missing or contradictory, present it to the user under `Open questions` and stop before drafting speculative steps. Do not modify any file while waiting for the answers.

## Workflow

1. Verify that Codex or Copilot is in Plan mode before starting or revising a plan. Apply the hard stop described above if it is not.
2. Read `context/project-overview.md`, `context/rules.md`, and `context/current-context.md`.
3. Inspect only the repository files needed to understand the affected behavior, architecture, conventions, and existing tests.
4. Check the preconditions. If information is missing or contradictory, present a concise `Open questions` list and wait for the user's answers.
5. Draft the complete solution. It must satisfy the objective, requirements, and acceptance criteria, and must distinguish confirmed decisions from assumptions.
6. Present the draft in the plan structure defined below. Do not write it to a file yet.
7. Ask the user either to approve the plan explicitly or request changes. Apply requested changes and present the revised plan for approval. Approval must be an unambiguous affirmative response; silence or a request for changes is not approval.
8. After approval, ask the user to choose exactly one storage format:
   - **Multiple step files:** one ordered Markdown file per independently implementable step in `context/steps/`.
   - **Single plan file:** the complete plan in one Markdown file in `context/steps/`.
   - **Current context:** an `## Implementation plan` section in `context/current-context.md`.
9. Use a structured user-input control for the storage choice when one is available; otherwise ask one concise question listing the three choices.
10. Persist only the approved plan in the selected format. Do not revise its scope while storing it.
11. Report the exact path of every file written and the `/context implement <spec>` invocation for each implementation target.

## Plan structure

Every plan, whether displayed in the conversation or written to a file, must contain:

1. **Objective:** the implementation outcome.
2. **Confirmed decisions:** requirements and choices established by the work item or the user.
3. **Assumptions:** non-confirmed details used by the plan. Use `None` when there are none.
4. **Affected areas:** expected components, files, integrations, and tests.
5. **Implementation steps:** ordered, independently verifiable changes.
6. **Acceptance criteria:** observable conditions that establish completion.
7. **Validation:** specific tests, commands, or manual checks for each relevant step.
8. **Risks and mitigations:** material implementation risks and how they will be controlled. Use `None identified` when appropriate.

Each step in **Implementation steps** must include:

- The intended outcome.
- Its dependencies on earlier steps, or `None`.
- The expected files or components to change.
- Concrete implementation tasks.
- Step-specific validation.

## Storage contract

### Multiple step files

- Create files in implementation order using `NN-<kebab-case-step-title>.md`, starting with `01` (for example, `01-add-domain-model.md`).
- Each file must be independently actionable and use the plan structure above, scoped to that step.
- Express cross-step dependencies using the exact filenames.
- The implementation target is the exact relative path, for example `/context implement context/steps/01-add-domain-model.md`.

### Single plan file

- Write the plan to `context/steps/01-implementation-plan.md`.
- The implementation target is `/context implement context/steps/01-implementation-plan.md`.

### Current context

- Add or replace one `## Implementation plan` section in `context/current-context.md`.
- Preserve every other section in the file.
- The implementation target is `/context implement current-context`.

### Existing targets

- Never silently overwrite an existing plan file or an existing `## Implementation plan` section.
- If a selected target already exists, show the collision and ask the user whether to replace it or choose another storage format or filename.
- Do not delete stale step files unless the user explicitly asks for their removal.

## Mode and write limitations

If the active Plan mode does not permit file edits, keep the approved plan and storage choice in the conversation and tell the user which target path or section would be written. Ask the user to exit Plan mode and run `/context plan persist` in the same conversation. This is the sole exception to the Plan-mode gate. During the persistence pass:

- Use only the explicitly approved plan and storage choice already present in the conversation.
- Do not inspect additional repository files, regenerate the plan, or revise its scope.
- If the approved plan or storage choice is not available in the conversation, stop and require the user to return to Plan mode.
- Check for existing-target collisions, write the approved content, and report the resulting implementation target.
