# ssf-product-pm Qoder Rule

Use this rule when generating, modifying, or reviewing product analysis and product design documents for an AI-driven software development workflow.

Read and follow:

- `SKILL.md`
- `references/workflow.md`
- `references/action-commands.md`
- `references/template-index.md`
- `references/review-gates.md`
- `references/id-conventions.md`
- `references/quality-checklist.md`
- `templates/`

Core rules:

- Analysis includes information collection, research insight, and requirement analysis.
- Analysis review is human-interactive and must stop for user confirmation.
- Design starts with product architecture.
- Product architecture review is human-interactive and must stop for user confirmation.
- PRD, feature specs, UI specs, prototype annotations, and baseline use auto review gates.
- Before writing files, read `ssf-workspace/index.md`; do not overwrite unrelated instances.
- Run intake gate for regeneration, overwrite, skip-stage, change, or unclear instance requests.
- Every FEAT and SCR must keep the same full structure.
- Use stable IDs: SPI, INTAKE, IQ, FACT, ASM, SRC, RAW, NEED, INS, GOAL, REQ, CAP, MOD, OBJ, FEAT, FLOW, BR, SCR, CMP, AC, CHG.
- Do not write database, API path, cache, queue, deployment, or other technical implementation details in PM documents.
