# ssf-product-pm Trae Project Rules

This project uses `ssf-product-pm` for product analysis and product design outputs in an AI-driven software development workflow.

Read `SKILL.md` first and follow its runtime load path. Do not load all references or templates by default.

Load only:

1. Required core and registry files named in `SKILL.md`.
2. The current action/document flow.
3. The current output template.
4. Reference files needed by the current gate, repair, ID, or QA task.

Rules:

- Generation, modification, repair, continuation, rerun, change, and prototype-run tasks are write-required unless the user explicitly asks for read-only review or no file changes.
- Only `analysis-human-review` and `product-architecture-human-review` may stop for user confirmation.
- Other gates are auto reviews: pass continues automatically; fail enters repair-run.
- `registries/documents.md` is the source of truth for document path, flow, template, gate, and interrupt behavior.
- `prototype-run` writes only to target instance `prototype-input/` and must not modify `product-spec/`.
- PM documents must not include database, API path, cache, queue, deployment, or other technical implementation details.
