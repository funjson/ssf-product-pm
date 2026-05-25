# ssf-product-pm Trae Project Rules

This project uses `ssf-product-pm` for product analysis and product design outputs in an AI-driven software development workflow.

Follow:

- `SKILL.md`
- `core/`
- `flows/`
- `registries/`
- `references/workflow.md`
- `references/action-commands.md`
- `references/template-index.md`
- `references/review-gates.md`
- `references/id-conventions.md`
- `references/quality-checklist.md`
- `references/repair-run.md`
- `templates/`

Rules:

1. Split work into Analysis and Design.
2. Analysis includes information collection, market/competitor/customer research, and requirement analysis.
3. Analysis review is a human review gate and must interrupt the flow.
4. Design starts with product architecture.
5. Product architecture review is a human review gate and must interrupt the flow.
6. Other design reviews are automatic self-check gates; failed checks require repair-run.
7. Before writing files, read `ssf-workspace/index.md` and resolve the target instance.
8. Run intake gate before regeneration, overwrite, skip-stage, or change requests.
9. Keep every FEAT and SCR structurally complete; do not compress later items into summary tables.
10. Do not write technical implementation details in PM documents.
11. Stage and sub-stage rules live in `flows/`; templates only define output structure.
12. repair-run must satisfy `references/repair-run.md`.
