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
8. Generation, modification, repair, and prototype-run tasks are `write_required` by default unless the user explicitly asks for read-only review or no file changes.
9. Use `inspect-only` only for explicit read/check/summarize requests, and `discuss-only` only for explicit no-write discussion requests.
10. Run intake gate before regeneration, overwrite, skip-stage, or change requests.
11. Keep every FEAT and SCR structurally complete; do not compress later items into summary tables.
12. Do not write technical implementation details in PM documents.
13. Stage and sub-stage rules live in `flows/`; templates only define output structure.
14. repair-run must satisfy `references/repair-run.md`.
15. For prototype input packages, use `prototype-run`, read `flows/prototype/prototype-run.md` and `templates/prototype/`, and write only to the target instance `prototype-input/`.
16. Prototype sample data and generated prototype results must not overwrite product facts in `product-spec/`.
