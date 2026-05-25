# 文档注册表

| doc_id | 输出文件 | 阶段 | 节点协议 | 模板 | Review Gate |
|---|---|---|---|---|---|
| INTAKE | `intake.md` | common | `templates/common/00-intake.md` | `templates/common/00-intake.md` | 无 |
| ANALYSIS-INPUT | `product-spec/01-analysis-input.md` | Analysis | `flows/analysis/01-information-collection.md` | `templates/analysis/01-analysis-input.md` | analysis-human-review |
| RESEARCH | `product-spec/02-research-insight.md` | Analysis | `flows/analysis/02-research-insight.md` | `templates/analysis/02-product-research-insight.md` | analysis-human-review |
| REQ-ANALYSIS | `product-spec/03-requirement-analysis.md` | Analysis | `flows/analysis/03-requirement-analysis.md` | `templates/analysis/03-requirement-analysis.md` | analysis-human-review |
| PRODUCT-ARCH | `product-spec/04-product-architecture.md` | Design | `flows/design/04-product-architecture.md` | `templates/design/04-product-architecture.md` | product-architecture-human-review |
| PRD | `product-spec/05-prd.md` | Design | `flows/design/05-prd.md` | `templates/design/05-prd.md` | prd-auto-review |
| FEATURE-SPEC | `product-spec/06-feature-task-spec.md` | Design | `flows/design/06-feature-task-spec.md` | `templates/design/06-feature-task-spec.md` | feature-spec-auto-review |
| UI-IA | `product-spec/07-ui-ia-screen-inventory.md` | Design | `flows/design/07-ui-ia-screen-inventory.md` | `templates/design/07-ui-ia-screen-inventory.md` | ui-ia-auto-review |
| UI-SPEC | `product-spec/08-structured-ui-interaction-spec.md` | Design | `flows/design/08-structured-ui-spec.md` | `templates/design/08-structured-ui-interaction-spec.md` | ui-spec-auto-review |
| PROTOTYPE | `product-spec/09-prototype-prompt-ui-annotation.md` | Design | `flows/design/09-prototype-annotation.md` | `templates/design/09-prototype-prompt-ui-annotation.md` | prototype-auto-review |
| BASELINE | `product-spec/10-product-baseline-change.md` | Design / Change | `flows/design/10-baseline-change.md` | `templates/design/10-product-baseline-change.md` | baseline-auto-review |
| WORKSPACE-INDEX | `ssf-workspace/index.md` | State | `core/state-protocol.md` | `templates/state/workspace-index.md` | repair-run-completion-check |
| MANIFEST | `instances/SPI-xxx/manifest.md` | State | `core/state-protocol.md` | `templates/state/instance-manifest.md` | repair-run-completion-check |
