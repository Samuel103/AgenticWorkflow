---
name: context
description: "Manage the active project context for feature and bug workflows, including loading, effort evaluation, investigation, fixing, planning, implementation, and closeout."
---

# Skill instructions

## Command routing

Route exactly one command, then read only the matching file from `actions/`:

- `/context load <param>` → [load](actions/load.md)
- `/context evaluate` → [evaluate](actions/evaluate.md)
- `/context investigate` → [investigate](actions/investigate.md)
- `/context fix` → [fix](actions/fix.md)
- `/context plan [persist]` → [plan](actions/plan.md)
- `/context implement <spec>` → [implement](actions/implement.md)
- `/context end` → [end](actions/end.md)

## Recommended workflow

1. `/context load <param>`: Gather context for the current feature or bug using the base context.
2. Optionally run `/context evaluate` to estimate the engineering time for a newly loaded feature or bug. For bugs, an estimate made before investigation must include diagnosis time and reflect the additional uncertainty; rerun it after investigation when a narrower estimate is needed.
3. For a bug or defect, run `/context investigate` to diagnose the issue and record the findings in `context/current-context.md`. This action never makes a fix.
4. Choose the implementation path:
   - For a well-scoped bug with a completed investigation, run `/context fix` to apply and validate the smallest correction supported by the findings.
   - For a bug requiring a material design decision, broader scope, or explicit planning, run `/context plan` and then `/context implement <spec>`.
   - For non-bug work, run `/context plan` and then `/context implement <spec>`. Skip investigation and `/context fix`.
5. `/context end`: Generate the configured closeout artifacts, reset the current context, and run the configured GitHub closeout process.

Use `/context plan persist` only when Plan mode cannot write an approved plan. A bug or defect must have a completed investigation before either fixing or planning.

---

# Skill configuration

The sections below are project-specific configuration. Replace every placeholder before relying on the corresponding workflow.

## Where to find the base context
<Where to find the base context? in a markdown file? by fetching a Work-Item number on Azure if yes how?>

## How to name the branch?
<With the Work-Item number ? With the feature name?>

## Release notes and resolution summary

Before using `/context end`, replace the guidance below with the project's exact requirements. Specify:

- Whether both artifacts are required and who their audience is.
- Their format, required sections, naming convention, and destination.
- Which context, diff, test results, work-item data, or other sources to use.
- Whether existing files may be updated and how generated content must be validated.

<Describe exactly how the AI must generate and save the release notes and resolution summary.>

## GitHub closeout process

Before using `/context end`, replace the guidance below with the repository's exact finalization workflow. Specify:

- The ordered Git and GitHub operations to perform, such as committing, pushing, or updating a pull request.
- The applicable repository, branch, naming, commit-message, pull-request, label, reviewer, and linking conventions.
- Required checks, approvals, stopping conditions, and cases where the process must be skipped.
- Whether the correct action for this repository is explicitly to perform no GitHub operation.

<Describe exactly what the AI must do as the final step of `/context end`.>
