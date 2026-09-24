## Purpose

Gather the information needed to understand one feature or bug and record it in `context/current-context.md`. Stop after loading context; do not plan or implement the work.

## Input

Resolve and interpret `<param>` according to the rules defined in `SKILL.md` under "Where to find the base context."

## Workflow

1. Read `context/project-overview.md`, `context/rules.md`, and the existing `context/current-context.md`.
2. Resolve `<param>` using the sources available in the project. Inspect only the repository files needed to understand the relevant behavior, conventions, and constraints.
3. Separate confirmed facts from assumptions. Record missing information as open questions; do not invent requirements.
4. Replace `context/current-context.md` using [`../assets/current-context-template.md`](../assets/current-context-template.md), completing every applicable section. Use `None identified` when a section has no known entries.
5. Report which work item was loaded, the most relevant files or components found, and any open questions. Do not create implementation steps; `/context plan` owns that work.
6. Create and check out a new branch according to the rules defined in `SKILL.md` under "How to name the branch."
