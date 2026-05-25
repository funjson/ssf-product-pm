# Gate 注册表

| gate_id | 类型 | 是否中断 | 主要证据 |
|---|---|---|---|
| analysis-human-review | human_review | yes | APR-001 |
| product-architecture-human-review | human_review | yes | APR-002 |
| product-architecture-delta-review | auto_review | no | CHECK-ARCH-DELTA-xxx |
| prd-auto-review | auto_review | no | CHECK-PRD-xxx |
| feature-spec-auto-review | auto_review | no | CHECK-FEAT-xxx |
| ui-ia-auto-review | auto_review | no | CHECK-UIIA-xxx |
| ui-spec-auto-review | auto_review | no | CHECK-UISPEC-xxx |
| prototype-auto-review | auto_review | no | CHECK-PROT-xxx |
| baseline-auto-review | auto_review | no | CHECK-BASE-xxx |
| change-run-local-review | auto_review | no | CHECK-CHG-xxx-xxx |
| repair-run-completion-check | auto_review | no | CHECK-REPAIR-xxx |

详细规则见 `references/review-gates.md`。
