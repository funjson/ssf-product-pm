# ssf-product-pm Trae Project Rules

This project uses `ssf-product-pm` for product design outputs in an AI-driven software development workflow.

## Use When

Use these rules when generating product research, PRD, requirement analysis, feature task specs, UI IA, structured UI interaction specs, prototype prompts, UI annotations, product baselines, or change specs.

## Source of Truth

Follow these files:

- `SKILL.md`
- `templates/`
- `references/id-conventions.md`
- `references/workflow.md`
- `references/quality-checklist.md`

## Rules

1. Do not output backlog management, priority matrix, MVP roadmap, or next-phase planning unless explicitly requested.
2. Before writing files, read `ssf-workspace/index.md` when it exists and resolve the target instance; do not overwrite unrelated instances.
3. Combine project description, field/user research, market research, and competitive analysis into one research insight document.
4. Generate requirement analysis before PRD.
5. PRD should provide product-level context, not all feature-level details.
6. Feature task spec is the main execution document. Flow, rules, permissions, acceptance criteria, and testing focus belong inside each feature task.
7. Every feature task must keep the same full structure; write "none / TBD" instead of omitting sections.
8. UI IA, structured UI/interaction spec, and prototype prompt + UI annotation are separate documents but must be linked by stable IDs.
9. Use structured UI spec and UI annotation as the source of truth for frontend implementation, not prototype images alone.
10. Use product baseline and change spec to preserve context across requirement changes.
11. Do not write architecture implementation details in PM documents.
