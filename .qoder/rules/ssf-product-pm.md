# ssf-product-pm Qoder Rule

Use this rule when generating, modifying, or reviewing product analysis and product design documents for an AI-driven software development workflow.

Read `SKILL.md` first and follow its runtime load path. Do not load all references or templates by default.

Load only:

- Required core and registry files named in `SKILL.md`.
- The current action/document flow.
- The current output template.
- Reference files needed by the current gate, repair, ID, or QA task.

Core invariants:

- Generation, modification, repair, continuation, rerun, change, and prototype-run tasks are `write_required` unless the user explicitly asks for read-only review or no file changes.
- Only `analysis-human-review` and `product-architecture-human-review` may stop for user confirmation.
- Other gates are auto reviews: pass continues automatically; fail enters repair-run.
- `registries/documents.md` is the runtime authority for document path, flow, template, gate, and interrupt behavior.
- `prototype-run` writes only to target instance `prototype-input/` and does not modify `product-spec/`.
- PM documents must not include database, API path, cache, queue, deployment, or other technical implementation details.
