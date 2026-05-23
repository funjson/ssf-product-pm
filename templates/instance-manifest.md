# 实例 Manifest

> 本文件记录单个产品设计实例的身份、状态、文档树和最近变更。Agent 进入实例后必须先读取本文件。

## 1. 实例身份

| 字段 | 内容 |
|---|---|
| instance_id | SPI-xxx |
| instance_name |  |
| product_name |  |
| task_type | 新系统 / 功能迭代 / 变更 / 单文档 / 其他 |
| workflow_type | full-run / flow-run / doc-run / change-run / repair-run |
| current_phase | intake / analysis / design / completed |
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
| 04 产品架构设计 | product-spec/04-product-architecture.md | missing / draft / ready_for_review / approved / needs_rework |  | product-architecture-human-review |
| 05 PRD 产品需求文档 | product-spec/05-prd.md | missing / draft / ready_for_review / needs_rework |  | prd-auto-review |
| 06 功能任务规格文档 | product-spec/06-feature-task-spec.md | missing / draft / ready_for_review / needs_rework |  | feature-spec-auto-review |
| 07 UI 信息架构与页面清单 | product-spec/07-ui-ia-screen-inventory.md | missing / draft / ready_for_review / needs_rework |  | ui-ia-auto-review |
| 08 结构化 UI/交互规格 | product-spec/08-structured-ui-interaction-spec.md | missing / draft / ready_for_review / needs_rework |  | ui-spec-auto-review |
| 09 原型生成 Prompt 与 UI 标注说明 | product-spec/09-prototype-prompt-ui-annotation.md | missing / draft / ready_for_review / needs_rework |  | prototype-auto-review |
| 10 产品基线与变更说明 | product-spec/10-product-baseline-change.md | missing / draft / ready_for_review / needs_rework |  | baseline-auto-review |

## 4. Review Gate 状态

| gate_id | gate_type | status | must_stop | result | blocking_issues |
|---|---|---|---|---|---|
| analysis-human-review | human_review | pending / approved / rejected / needs_rework | yes | pending |  |
| product-architecture-human-review | human_review | pending / approved / rejected / needs_rework | yes | pending |  |
| prd-auto-review | auto_review | pending / pass / fail | no | pending |  |
| feature-spec-auto-review | auto_review | pending / pass / fail | no | pending |  |
| ui-ia-auto-review | auto_review | pending / pass / fail | no | pending |  |
| ui-spec-auto-review | auto_review | pending / pass / fail | no | pending |  |
| prototype-auto-review | auto_review | pending / pass / fail | no | pending |  |
| baseline-auto-review | auto_review | pending / pass / fail | no | pending |  |

## 5. 运行记录

| time | execution_mode | user_intent | result | affected_documents |
|---|---|---|---|---|
|  |  |  |  |  |

## 6. 待确认问题

| question_id | 问题 | 影响范围 | 建议处理 |
|---|---|---|---|
| Q-001 |  |  |  |
