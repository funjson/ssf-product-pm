# Gate 注册表

| gate_id | 类型 | gate_scope | must_stop | continue_on_pass | 主要证据 |
|---|---|---|---|---|---|
| analysis-human-review | human_review | stage:analysis，覆盖 01-03 | yes | no | APR-001 |
| product-architecture-human-review | human_review | document:04-product-architecture | yes | no | APR-002 |
| product-architecture-delta-review | auto_review | change:architecture-delta | no | yes | CHECK-ARCH-DELTA-xxx |
| prd-auto-review | auto_review | document:05-prd | no | yes | CHECK-PRD-xxx |
| feature-spec-auto-review | auto_review | document:06-feature-task-spec | no | yes | CHECK-FEAT-xxx |
| ui-ia-auto-review | auto_review | document:07-ui-ia-screen-inventory | no | yes | CHECK-UIIA-xxx |
| ui-spec-auto-review | auto_review | document:08-structured-ui-interaction-spec | no | yes | CHECK-UISPEC-xxx |
| prototype-auto-review | auto_review | document:09-prototype-prompt-ui-annotation | no | yes | CHECK-PROT-xxx |
| baseline-auto-review | auto_review | document:10-product-baseline-change | no | yes | CHECK-BASE-xxx |
| change-run-local-review | auto_review | change:local | no | yes | CHECK-CHG-xxx-xxx |
| prototype-input-auto-review | auto_review | package:prototype-input | no | yes | CHECK-PINPUT-xxx / CHECK-PROTOTYPE-xxx |
| repair-run-completion-check | auto_review | runtime:repair-run | no | yes | CHECK-REPAIR-xxx |

详细规则见 `references/review-gates.md`。
