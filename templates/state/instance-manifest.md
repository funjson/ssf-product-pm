# 实例 Manifest

> 本文件记录单个产品设计实例的身份、状态、文档树和最近变更。Agent 进入实例后必须先读取本文件。

## 1. 实例身份

| 字段 | 内容 |
|---|---|
| instance_id | SPI-xxx |
| instance_name |  |
| product_name |  |
| task_type | 新系统 / 功能迭代 / 变更 / 单文档 / 其他 |
| workflow_type | full-run / analysis-run / design-run / flow-run / doc-run / change-run / repair-run |
| current_phase | intake / analysis / design / completed |
| active_gate | analysis-human-review / product-architecture-human-review / product-architecture-delta-review / change-run-local-review / auto-review / none |
| blocked | yes / no |
| current_blocker | 无 / 等待分析阶段人工评审 / 等待产品架构人工评审 / 等待 repair-run / 等待用户选择实例 |
| next_allowed_actions | wait-user-review / continue-analysis / continue-design / repair-run / change-run / doc-run / prototype-run / discuss-only |
| status | in_progress / paused / completed / archived |
| created_at |  |
| updated_at |  |
| root_path | ssf-workspace/instances/SPI-xxx |

## 2. 实例摘要

| 项目 | 内容 |
|---|---|
| 产品形态 | App / Web / SaaS / 后台 / 小程序 / 插件 / IoT / 其他 |
| 业务领域 |  |
| 目标用户 |  |
| 核心目标 |  |
| 当前焦点 |  |
| 已有材料 |  |
| 关键约束 |  |

## 3. 文档状态

| 文档 | 路径 | 状态 | 最近更新时间 | review_gate / 说明 |
|---|---|---|---|---|
| Intake 信息收集 | intake.md | missing / completed / skipped_with_reason |  | 公共入口能力，不计入产品版本 |
| 01 分析输入与信息收集 | product-spec/01-analysis-input.md | missing / draft / ready_for_review / approved / needs_rework |  | analysis-human-review |
| 02 产品调研与洞察报告 | product-spec/02-research-insight.md | missing / draft / ready_for_review / approved / needs_rework |  | analysis-human-review |
| 03 需求分析说明 | product-spec/03-requirement-analysis.md | missing / draft / ready_for_review / approved / needs_rework |  | analysis-human-review |
| 04 产品架构设计 | product-spec/04-product-architecture.md | missing / draft / ready_for_review / ready_for_review_delta / approved / approved_with_delta / needs_rework |  | product-architecture-human-review / product-architecture-delta-review |
| 05 PRD 产品需求文档 | product-spec/05-prd.md | missing / draft / ready_for_review / needs_rework |  | prd-auto-review |
| 06 功能任务规格文档 | product-spec/06-feature-task-spec.md | missing / draft / ready_for_review / needs_rework |  | feature-spec-auto-review |
| 07 UI 信息架构与页面清单 | product-spec/07-ui-ia-screen-inventory.md | missing / draft / ready_for_review / needs_rework |  | ui-ia-auto-review |
| 08 结构化 UI/交互规格 | product-spec/08-structured-ui-interaction-spec.md | missing / draft / ready_for_review / needs_rework |  | ui-spec-auto-review |
| 09 原型生成 Prompt 与 UI 标注说明 | product-spec/09-prototype-prompt-ui-annotation.md | missing / draft / ready_for_review / needs_rework |  | prototype-auto-review |
| 10 产品基线与变更说明 | product-spec/10-product-baseline-change.md | missing / draft / ready_for_review / needs_rework |  | baseline-auto-review |

## 4. Review Gate 状态

> 人工评审和自动评审必须分开记录。人工评审通过必须引用 `approval_id`；自动评审通过只能引用 `CHECK-xxx`，不能代表用户确认。

| gate_id | gate_type | status | must_stop | blocked | evidence_id | updated_at | blocking_issues |
|---|---|---|---|---|---|---|---|
| analysis-human-review | human_review | pending / approved / rejected / needs_rework | yes | yes / no | APR-xxx / 无 |  |  |
| product-architecture-human-review | human_review | pending / approved / rejected / needs_rework | yes | yes / no | APR-xxx / 无 |  |  |
| product-architecture-delta-review | auto_review | pending / pass / fail / escalated | no | yes / no | ARCH-DELTA-xxx / CHECK-ARCH-DELTA-xxx / 无 |  |  |
| prd-auto-review | auto_review | pending / pass / fail | no | yes / no | CHECK-xxx / 无 |  |  |
| feature-spec-auto-review | auto_review | pending / pass / fail | no | yes / no | CHECK-xxx / 无 |  |  |
| ui-ia-auto-review | auto_review | pending / pass / fail | no | yes / no | CHECK-xxx / 无 |  |  |
| ui-spec-auto-review | auto_review | pending / pass / fail | no | yes / no | CHECK-xxx / 无 |  |  |
| prototype-auto-review | auto_review | pending / pass / fail | no | yes / no | CHECK-xxx / 无 |  |  |
| baseline-auto-review | auto_review | pending / pass / fail | no | yes / no | CHECK-xxx / 无 |  |  |
| change-run-local-review | auto_review | pending / pass / fail / escalated | no | yes / no | CHECK-CHG-xxx-xxx / 无 |  |  |

## 5. 人工确认记录

> 只有本节存在对应 `APR-xxx` 时，人工 Review Gate 才能写 `approved`。不得由模型自行推断人工确认。

| approval_id | gate_id | user_words | approved_scope | approval_result | approved_at | notes |
|---|---|---|---|---|---|---|
| APR-001 | analysis-human-review |  | 01-analysis-input.md / 02-research-insight.md / 03-requirement-analysis.md | approved / rejected / needs_rework |  |  |
| APR-002 | product-architecture-human-review |  | 04-product-architecture.md | approved / rejected / needs_rework |  |  |

## 6. 自动检查记录

| check_run_id | gate_id | checked_documents | result | failed_checks | repair_action |
|---|---|---|---|---|---|
| ACR-001 | prd-auto-review | product-spec/05-prd.md | pass / fail | CHECK-xxx / 无 | 无 / repair-run |

## 7. 产品架构 Delta 记录

| architecture_delta_id | change_id | changed_items | boundary_changed | review_gate | result | notes |
|---|---|---|---|---|---|---|
| ARCH-DELTA-001 | CHG-xxx | CAP-xxx / MOD-xxx / OBJ-xxx / ARCH-DEC-xxx | yes / no | product-architecture-delta-review / product-architecture-human-review | pass / escalated / pending |  |

## 8. 运行记录

| time | execution_mode | user_intent | result | affected_documents |
|---|---|---|---|---|
|  |  |  |  |  |

## 9. 下一步建议动作

| action_id | 建议动作 | 触发条件 | 是否允许自动执行 |
|---|---|---|---|
| NEXT-001 | 等待用户完成 Analysis 人工评审 | analysis-human-review pending / needs_rework | 否 |
| NEXT-002 | 等待用户完成产品架构人工评审 | product-architecture-human-review pending / needs_rework | 否 |
| NEXT-003 | 继续 Design 后续文档 | analysis-human-review approved 且 product-architecture-human-review approved | 是 |
| NEXT-004 | 执行 repair-run | 任一 auto_review fail | 是 |
| NEXT-005 | 执行 change-run | 用户提出基于当前基线变更 | 需先判断影响范围 |
| NEXT-006 | 执行 product-architecture-delta-review | 局部变更修改产品架构但不改变模块边界 | 是 |

## 10. 待确认问题

| question_id | 问题 | 影响范围 | 建议处理 |
|---|---|---|---|
| Q-001 |  |  |  |
