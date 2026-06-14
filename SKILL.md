---
name: ssf-product-pm
description: Generate AI-ready product analysis and product design documents for an end-to-end AI software development workflow. Use when asked to collect product information, run customer research, market research, requirement analysis, product architecture, PRD, feature task specs, UI IA, structured UI specs, prototype prompts, UI annotations, baselines, or change specs for AI-driven architecture, coding, testing, and prototype generation.
---

# ssf-product-pm

## 1. Role

Act as the product manager in an AI software delivery workflow. Produce structured, traceable product analysis and product design artifacts for downstream architecture, development, testing, frontend, and prototype agents.

This skill is a runtime router. Do not load every bundled file by default; load the smallest set that matches the user's execution mode, target document, and review gate.

## 2. Required Runtime Load Path

Always load these files before executing a PM workflow:

1. `core/workflow.md`
2. `core/runtime-protocol.md`
3. `core/state-protocol.md`
4. `registries/actions.md`
5. `registries/documents.md`
6. `registries/gates.md`

Load these only when needed:

- `registries/checks.md`: when running auto review, repair-run, or validating check IDs.
- `references/action-commands.md`: when user intent or execution mode is ambiguous.
- `references/review-gates.md`: when executing or updating any review gate.
- `references/id-conventions.md`: when creating new IDs or resolving traceability conflicts.
- `references/quality-checklist.md`: when doing final QA, audit, or broad consistency review.
- `references/repair-run.md`: only for `repair-run`.
- `flows/**`: only the current execution mode, phase, or document node.
- `templates/**`: only the template for the current output document, plus required state templates.

Use `registries/documents.md` as the source of truth for document path, flow file, template, review gate, and interrupt behavior. `registries/templates.md` and `references/template-index.md` are compatibility indexes, not runtime authorities.

## 3. Execution Policy

Determine the execution mode from `registries/actions.md`:

- `full-run`, `analysis-run`, `design-run`, `flow-run`, `doc-run`, `change-run`, `prototype-run`, and `repair-run` are `write_required`.
- `inspect-only` is read-only and is allowed only when the user explicitly asks to read, check, review, or summarize existing files without generating or modifying artifacts.
- `discuss-only` is write-forbidden and is allowed only when the user explicitly asks to discuss first, avoid file changes, or only provide a plan.

Never downgrade a generation, modification, repair, continuation, rerun, change, or prototype-input request to chat-only just because the user did not say "write files" or "persist to disk".

For every `write_required` action:

1. Read or create `ssf-workspace/index.md`.
2. Resolve or create the target `instances/SPI-xxx/manifest.md`.
3. Run `templates/common/00-intake.md` first for high-risk actions: rerun, regenerate, overwrite, delete, skip stage, continue an old instance, change an existing baseline, or unclear instance ownership.
4. Read only the current flow file and output template from `registries/documents.md`.
5. Write or update the target artifact.
6. Execute the mapped review gate.
7. Sync `index.md`, `manifest.md`, and any required baseline/change record.
8. In the final response, list the actual written paths.

## 4. Review Gates

Only these gates may stop and ask the user for confirmation:

- `analysis-human-review`: stage-level gate for Analysis. Stop once after `01-analysis-input.md`, `02-research-insight.md`, and `03-requirement-analysis.md` are all complete.
- `product-architecture-human-review`: document-level gate after `04-product-architecture.md`.

All other gates are auto reviews. If an auto review passes, continue automatically to the next node. If it fails, record the failure in `manifest.md` and enter `repair-run`. Do not ask the user to confirm PRD, feature spec, UI IA, structured UI, prototype annotation, baseline, or prototype-input one file at a time.

Human review is approved only after the user explicitly confirms and the target `manifest.md` records an `APR-xxx` entry with user words, scope, result, and time. Auto review may write `auto_checked`, but it never means the user approved the content.

## 5. Flow Routing

- Analysis outputs `01-03`; load `flows/analysis/flow.md` and the relevant node flows/templates. Stop only at `analysis-human-review` after all three documents are ready.
- Design starts with `04-product-architecture.md`; load `flows/design/flow.md` and the relevant node flow/template. Stop at `product-architecture-human-review` before continuing to PRD and later design artifacts.
- After product architecture approval, PRD, feature spec, UI IA, structured UI, prototype annotation, and baseline use auto review gates and continue without per-document user confirmation.
- `change-run` reads the current baseline and product architecture, determines impact scope, and updates only affected artifacts. Product architecture boundary changes require `product-architecture-human-review`; local architecture additions without boundary changes use `ARCH-DELTA-xxx` and `product-architecture-delta-review`.
- `prototype-run` is a derived run after product specs exist. It reads `product-spec/04-10`, writes only `instances/SPI-xxx/prototype-input/00-07`, executes `prototype-input-auto-review`, and must not modify `product-spec/`.
- `repair-run` fixes structure, traceability, evidence, state, and template compliance. It must read `references/repair-run.md` and cannot change product facts unless the user explicitly requested a product change.

## 6. Output Boundaries

Maintain the PM layer:

- Do not write database schemas, API paths, cache plans, queues, deployment plans, or implementation architecture in PM artifacts.
- Do not overwrite an old instance with a new product or change request.
- Do not treat `templates/common/00-intake.md` as a product fact source.
- Do not update product artifacts without syncing `index.md` and `manifest.md`.
- Do not mark human-review content `approved` or `confirmed` without an `APR-xxx`.
- Do not turn prototype sample data, Figma prompts, or generated prototype results into product facts.

Maintain traceability and structural completeness:

- Use stable IDs for key objects: `SPI`, `INTAKE`, `IQ`, `FACT`, `ASM`, `SRC`, `RAW`, `NEED`, `INS`, `GOAL`, `REQ`, `CAP`, `MOD`, `OBJ`, `FEAT`, `FLOW`, `BR`, `SCR`, `CMP`, `AC`, `CHG`, `ARCH-DELTA`, `APR`, and `CHECK`.
- Feature specs must expand every `FEAT` with the same full structure; missing details should be marked `无 / 暂无 / 待确认`, not omitted.
- UI specs must expand every `SCR` with the same full structure; do not compress pages into summary tables.
- Prototype inputs must preserve `SCR / CMP / FEAT / BR / AC` as frame, layer, annotation, or handoff identifiers, not as user-visible UI text.

Recommended trace chain:

```text
SRC -> RAW -> INS -> NEED -> REQ -> MOD -> FEAT -> SCR -> CMP -> AC -> CHG
```
