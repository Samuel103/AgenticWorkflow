---
name: context
description: "Manage the active project context through loading, planning, implementation, and closeout."
---

# Skill instructions

## Command routing

Route exactly one command, then read only the matching file from `actions/`:

- `/context load <param>` → [load](actions/load.md)
- `/context plan [persist]` → [plan](actions/plan.md)
- `/context implement` → [implement](actions/implement.md)
- `/context end` → [end](actions/end.md)

## Recommended workflow

1. `/context load <param>`: Gather context for the current request using the base context.
2. `/context plan`: Examine the request and relevant repository files, then prepare an implementation plan for approval. Include any necessary analysis or verification in the plan.
3. `/context implement`: Implement and validate the approved plan in `context/steps/01-implementation-plan.md`.
4. `/context end`: Generate the configured closeout artifacts, reset the current context, and run the configured GitHub closeout process.

Use `/context plan persist` only when Plan mode cannot write an approved plan.

---

# Skill configuration

The sections below are project-specific configuration. Replace every placeholder before relying on the corresponding workflow.

## Where to find the base context
<Where to find the base context? In a Markdown file, an external request, or another source? How should the reference be resolved?>

## How to name the branch?
<With the request reference or a concise name?>

## Release notes and resolution summary

Before using `/context end`, replace the guidance below with the project's exact requirements. Specify:

- Whether both artifacts are required and who their audience is.
- Their format, required sections, naming convention, and destination.
- Which context, diff, test results, request data, or other sources to use.
- Whether existing files may be updated and how generated content must be validated.

<Describe exactly how the AI must generate and save the release notes and resolution summary.>

## GitHub closeout process

Before using `/context end`, replace the guidance below with the repository's exact finalization workflow. Specify:

- The ordered Git and GitHub operations to perform, such as committing, pushing, or updating a pull request.
- The applicable repository, branch, naming, commit-message, pull-request, label, reviewer, and linking conventions.
- Required checks, approvals, stopping conditions, and cases where the process must be skipped.
- Whether the correct action for this repository is explicitly to perform no GitHub operation.

<Describe exactly what the AI must do as the final step of `/context end`.>
