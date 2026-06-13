# 文档注册表

| doc_id | 输出文件 | 阶段 | 节点协议 | 模板 | Review Gate | gate_scope | 是否中断 |
|---|---|---|---|---|---|---|---|
| INTAKE | `intake.md` | common | `templates/common/00-intake.md` | `templates/common/00-intake.md` | 无 | 无 | no |
| ANALYSIS-INPUT | `product-spec/01-analysis-input.md` | Analysis | `flows/analysis/01-information-collection.md` | `templates/analysis/01-analysis-input.md` | analysis-human-review | stage:analysis，01-03 完成后统一触发 | no |
| RESEARCH | `product-spec/02-research-insight.md` | Analysis | `flows/analysis/02-research-insight.md` | `templates/analysis/02-product-research-insight.md` | analysis-human-review | stage:analysis，01-03 完成后统一触发 | no |
| REQ-ANALYSIS | `product-spec/03-requirement-analysis.md` | Analysis | `flows/analysis/03-requirement-analysis.md` | `templates/analysis/03-requirement-analysis.md` | analysis-human-review | stage:analysis，01-03 完成后统一触发 | yes |
| PRODUCT-ARCH | `product-spec/04-product-architecture.md` | Design | `flows/design/04-product-architecture.md` | `templates/design/04-product-architecture.md` | product-architecture-human-review | document:04-product-architecture | yes |
| PRD | `product-spec/05-prd.md` | Design | `flows/design/05-prd.md` | `templates/design/05-prd.md` | prd-auto-review | document:05-prd | no |
| FEATURE-SPEC | `product-spec/06-feature-task-spec.md` | Design | `flows/design/06-feature-task-spec.md` | `templates/design/06-feature-task-spec.md` | feature-spec-auto-review | document:06-feature-task-spec | no |
| UI-IA | `product-spec/07-ui-ia-screen-inventory.md` | Design | `flows/design/07-ui-ia-screen-inventory.md` | `templates/design/07-ui-ia-screen-inventory.md` | ui-ia-auto-review | document:07-ui-ia-screen-inventory | no |
| UI-SPEC | `product-spec/08-structured-ui-interaction-spec.md` | Design | `flows/design/08-structured-ui-spec.md` | `templates/design/08-structured-ui-interaction-spec.md` | ui-spec-auto-review | document:08-structured-ui-interaction-spec | no |
| PROTOTYPE | `product-spec/09-prototype-prompt-ui-annotation.md` | Design | `flows/design/09-prototype-annotation.md` | `templates/design/09-prototype-prompt-ui-annotation.md` | prototype-auto-review | document:09-prototype-prompt-ui-annotation | no |
| BASELINE | `product-spec/10-product-baseline-change.md` | Design / Change | `flows/design/10-baseline-change.md` | `templates/design/10-product-baseline-change.md` | baseline-auto-review | document:10-product-baseline-change | no |
| PROTO-MASTER-BRIEF | `prototype-input/00-prototype-master-brief.md` | Prototype | `flows/prototype/prototype-run.md` | `templates/prototype/00-prototype-master-brief.md` | prototype-input-auto-review | package:prototype-input | no |
| PROTO-DESIGN-SYSTEM | `prototype-input/01-design-system-constraints.md` | Prototype | `flows/prototype/prototype-run.md` | `templates/prototype/01-design-system-constraints.md` | prototype-input-auto-review | package:prototype-input | no |
| PROTO-SCREEN-CONTRACTS | `prototype-input/02-screen-contracts.md` | Prototype | `flows/prototype/prototype-run.md` | `templates/prototype/02-screen-contracts.md` | prototype-input-auto-review | package:prototype-input | no |
| PROTO-FLOW-CONTRACTS | `prototype-input/03-flow-contracts.md` | Prototype | `flows/prototype/prototype-run.md` | `templates/prototype/03-flow-contracts.md` | prototype-input-auto-review | package:prototype-input | no |
| PROTO-SAMPLE-DATA | `prototype-input/04-sample-data.md` | Prototype | `flows/prototype/prototype-run.md` | `templates/prototype/04-sample-data.md` | prototype-input-auto-review | package:prototype-input | no |
| PROTO-FIGMA-PROMPTS | `prototype-input/05-figma-make-prompts.md` | Prototype | `flows/prototype/prototype-run.md` | `templates/prototype/05-figma-make-prompts.md` | prototype-input-auto-review | package:prototype-input | no |
| PROTO-ANNOTATION-HANDOFF | `prototype-input/06-ui-annotation-handoff.md` | Prototype | `flows/prototype/prototype-run.md` | `templates/prototype/06-ui-annotation-handoff.md` | prototype-input-auto-review | package:prototype-input | no |
| PROTO-REVIEW-CHECKLIST | `prototype-input/07-prototype-review-checklist.md` | Prototype | `flows/prototype/prototype-run.md` | `templates/prototype/07-prototype-review-checklist.md` | prototype-input-auto-review | package:prototype-input | no |
| WORKSPACE-INDEX | `ssf-workspace/index.md` | State | `core/state-protocol.md` | `templates/state/workspace-index.md` | repair-run-completion-check | runtime:repair-run | no |
| MANIFEST | `instances/SPI-xxx/manifest.md` | State | `core/state-protocol.md` | `templates/state/instance-manifest.md` | repair-run-completion-check | runtime:repair-run | no |
