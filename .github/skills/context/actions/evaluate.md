# Estimate engineering effort

Use this action for `/context evaluate`.

## Purpose

Estimate the engineering time required for the new feature or bug loaded in `context/current-context.md`. The estimate is for software-engineering allocation only. It is not an implementation plan, delivery commitment, calendar schedule, or authorization to change the project.

## Preconditions

- `context/current-context.md` must describe one specific active work item whose type is `feature` or `bug`.
- The objective and request must provide enough information to identify the intended outcome.
- If essential requirements, acceptance criteria, or access constraints are missing, identify them and either give a clearly conditional estimate or stop when no responsible range can be produced.

Do not use this action for maintenance, refactoring, research, or other work-item types. Do not relabel an unsupported work item merely to estimate it.

## Evaluation workflow

1. Read `context/project-overview.md`, `context/rules.md`, and `context/current-context.md`.
2. Read the repository instructions that apply to the likely affected areas. Inspect only enough relevant code, tests, configuration, and documentation to ground the estimate in the current system.
3. Define the estimation boundary: state what outcome is included, what is excluded, and which assumptions materially affect the effort.
4. Break the work into coarse engineering activities suitable for estimation, such as investigation, design, implementation, tests, integration, review corrections, and required validation. Do not turn these activities into an implementation plan.
5. Estimate each activity as a range in engineer-hours or engineer-days. Use the project's established unit when one exists; otherwise use engineer-hours and treat one engineer-day as eight engineer-hours.
6. Add the activity ranges to produce the total engineering-effort range. Do not convert effort into elapsed calendar time unless the user separately supplies team capacity, availability, and scheduling constraints.
7. Assign confidence as `High`, `Medium`, or `Low`, and explain the main reasons for that confidence. Prefer a wider range over false precision.
8. List the unknowns and risks most likely to move the estimate. When useful, state what investigation or decision would narrow the range.

For a bug without a completed `## Bug investigation`, include diagnosis and reproduction effort, keep the repair estimate conditional on the possible causes, and use `Low` confidence unless repository evidence justifies otherwise. Do not claim or infer a root cause. When a completed investigation exists, use its recorded evidence and root cause or hypothesis to narrow the estimate.

## Required output

Report:

- **Work item:** Its reference, title, and whether it is a feature or bug.
- **Estimation boundary:** Included work, excluded work, and material assumptions.
- **Effort breakdown:** A short table with each engineering activity, its effort range, and the evidence or assumption supporting it.
- **Total engineering effort:** The summed low-to-high range and the estimation unit.
- **Confidence:** `High`, `Medium`, or `Low`, with a concise rationale.
- **Estimate drivers:** Unknowns, dependencies, or risks that could materially increase or decrease the range.
- **Next step to narrow the estimate:** The smallest useful investigation, clarification, or decision, or `None` when confidence is already high.

Do not provide a single-point estimate when meaningful uncertainty remains. Keep contingency visible in the ranges rather than adding an unexplained buffer.

## Hard boundary

This action is read-only. Do not modify source code, tests, configuration, dependencies, context files, plans, branches, or external work items. Do not implement, fix, create an implementation plan, or perform project closeout. Diagnostic commands must not intentionally alter tracked files, install dependencies, run migrations, or update external systems.
