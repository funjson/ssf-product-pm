# ssf-product-pm Qoder Rule

## Apply When

Use this rule when the user asks to generate, modify, or review product design documents for an AI-driven software development workflow, including PRD, feature task specs, UI specs, prototype prompts, UI annotations, baseline, or change specs.

## Instructions

Read and follow:

- `SKILL.md`
- `templates/`
- `references/id-conventions.md`
- `references/workflow.md`
- `references/quality-checklist.md`

## Core Rules

- Do not create traditional demand management artifacts such as backlog, priority matrix, MVP roadmap, or next release plan unless explicitly requested.
- Before writing files, read `ssf-workspace/index.md` when it exists and resolve the target instance; do not overwrite unrelated instances.
- Combine project description, field/user research, market research, and competitive analysis into one research insight document.
- Generate requirement analysis before PRD.
- Use the PRD as product-level context only.
- Use feature task specs as the main execution unit.
- Put flows, rules, permissions, acceptance criteria, and testing focus into feature task specs.
- Every feature task must keep the same full structure; write "none / TBD" instead of omitting sections.
- Keep UI IA, structured UI spec, and prototype prompt + UI annotation separate but linked by IDs.
- Use stable IDs: SPI, SRC, RAW, NEED, INS, GOAL, REQ, FEAT, FLOW, BR, SCR, CMP, AC, CHG.
- Treat structured UI spec and UI annotation as source of truth for frontend AI, not prototype images alone.
- Use product baseline and change spec for all requirement change scenarios.
