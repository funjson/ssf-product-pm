# ssf-product-pm Qoder Rule

Use this rule when generating, modifying, or reviewing product analysis and product design documents for an AI-driven software development workflow.

Read and follow:

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

Core rules:

- Analysis includes information collection, research insight, and requirement analysis.
- Analysis review is human-interactive and must stop once after documents 01-03 are complete.
- Design starts with product architecture.
- Product architecture review is human-interactive and must stop for user confirmation.
- PRD, feature specs, UI specs, prototype annotations, and baseline use auto review gates; pass continues automatically, fail enters repair-run.
- Before writing files, read `ssf-workspace/index.md`; do not overwrite unrelated instances.
- Generation, modification, repair, and prototype-run tasks are `write_required` by default unless the user explicitly asks for read-only review or no file changes.
- Use `inspect-only` only for explicit read/check/summarize requests, and `discuss-only` only for explicit no-write discussion requests.
- Run intake gate for regeneration, overwrite, skip-stage, change, or unclear instance requests.
- Every FEAT and SCR must keep the same full structure.
- Stage and sub-stage rules live in `flows/`; templates only define output structure.
- repair-run must satisfy `references/repair-run.md`.
- prototype-run must read `flows/prototype/prototype-run.md` and `templates/prototype/`, then write only to `instances/SPI-xxx/prototype-input/`.
- Do not turn prototype sample data, Figma prompts, or generated prototype results into product facts.
- Use stable IDs: SPI, INTAKE, IQ, FACT, ASM, SRC, RAW, NEED, INS, GOAL, REQ, CAP, MOD, OBJ, FEAT, FLOW, BR, SCR, CMP, AC, CHG.
- Do not write database, API path, cache, queue, deployment, or other technical implementation details in PM documents.
