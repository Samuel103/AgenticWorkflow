## Purpose

Turn the request loaded in `context/current-context.md` into a clear, ordered, and explicitly approved implementation plan in `context/steps/01-implementation-plan.md`. Planning must take place in Codex or Copilot Plan mode.

## Required Codex or Copilot mode

- The planning and approval phases may run only when Codex or Copilot is already in Plan mode.
- If Plan mode is not active when starting or revising a plan, stop immediately. Do not inspect the repository and do not modify files.
- Tell the user to run `/plan` to enable Plan mode, then run `/context plan` again.
- Do not claim to switch modes on the user's behalf. The user must activate Plan mode through the coding assistant's interface.
- The only exception is the persistence phase described under **Mode and write limitations**. That phase may run outside Plan mode because it stores an already-approved plan without performing further planning.

## Preconditions

- `context/current-context.md` must describe a specific request.
- The objective and request must contain enough information to plan the work responsibly.
- The request must provide enough acceptance criteria or expected outcomes to determine when implementation is complete.
- Include any necessary analysis or verification before dependent implementation steps. If its outcome could materially change the proposed solution, make that a stopping point and obtain approval for a revised plan before continuing.
- If essential information is missing or contradictory, present it to the user under `Open questions` and stop before drafting speculative steps. Do not modify any file while waiting for the answers.

## Workflow

1. Verify that Codex or Copilot is in Plan mode before starting or revising a plan. Apply the hard stop described above if it is not.
2. Read `context/project-overview.md`, `context/rules.md`, and `context/current-context.md`.
3. Inspect only the repository files needed to understand the affected behavior, architecture, conventions, and existing tests.
4. Check the preconditions. If information is missing or contradictory, present a concise `Open questions` list and wait for the user's answers.
5. Draft the complete solution. It must satisfy the objective, requirements, and acceptance criteria, and must distinguish confirmed decisions from assumptions.
6. Present the draft in the plan structure defined below. Do not write it to a file yet.
7. Ask the user either to approve the plan explicitly or request changes. Apply requested changes and present the revised plan for approval. Approval must be an unambiguous affirmative response; silence or a request for changes is not approval.
8. Check whether `context/steps/01-implementation-plan.md` already exists. If it does, show the collision and get explicit approval before replacing it.
9. Write only the approved plan to `context/steps/01-implementation-plan.md`. Do not revise its scope while storing it.
10. Report the plan path and the `/context implement` command.

## Plan structure

The plan, whether displayed in the conversation or written to the file, must contain:

1. **Objective:** the implementation outcome.
2. **Confirmed decisions:** requirements and choices established by the request or the user.
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

- Store the complete approved plan in `context/steps/01-implementation-plan.md`.
- Never silently overwrite that file. If it exists, get explicit approval before replacing it.
- Do not delete other files in `context/steps/` unless the user explicitly asks for their removal.

## Mode and write limitations

If the active Plan mode does not permit file edits, keep the approved plan in the conversation and tell the user that it will be written to `context/steps/01-implementation-plan.md`. Ask the user to exit Plan mode and run `/context plan persist` in the same conversation. This is the sole exception to the Plan-mode gate. During the persistence pass:

- Use only the explicitly approved plan already present in the conversation.
- Do not inspect additional repository files, regenerate the plan, or revise its scope.
- If the approved plan is not available in the conversation, stop and require the user to return to Plan mode.
- Check whether the target file exists. If replacement was not already approved in the conversation, get explicit approval before replacing it. Write the approved content and report `/context implement`.
