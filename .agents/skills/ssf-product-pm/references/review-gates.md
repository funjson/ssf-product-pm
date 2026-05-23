# Review Gate 规则

> 本文件集中管理 `ssf-product-pm` 的评审能力。工作流只引用评审标识，不在每个文档里散写评审规则，方便后续调整评审方案。

## 1. 评审类型

| review_type | 含义 | 是否中断流程 | 处理方式 |
|---|---|---|---|
| human_review | 人机交互评审 | 是 | 必须停止继续生成，等待用户确认、修改或驳回 |
| auto_review | 自动自检查 | 否 | 模型根据检查项自检；失败时进入 repair-run |

## 2. 状态枚举

| 字段 | 可选值 |
|---|---|
| review_status | draft / ready_for_review / approved / rejected / needs_rework |
| review_result | pass / fail / pending |
| blocking_level | none / warning / blocking |

默认规则：

- 新生成文档默认 `review_status = ready_for_review`，不得默认写 `approved` 或 `confirmed`。
- 只有用户明确确认后，人工评审节点才可写 `approved`。
- 自动评审通过只能说明结构和一致性检查通过，不代表用户已确认。

## 3. Gate 清单

| gate_id | 节点 | 类型 | 是否允许自动继续 | 失败处理 |
|---|---|---|---|---|
| analysis-human-review | 分析阶段评审 | human_review | 否 | 停止流程，列出缺失信息和建议补充项 |
| product-architecture-human-review | 产品架构评审 | human_review | 否 | 停止流程，要求用户确认模块划分、边界和对象 |
| prd-auto-review | PRD 自检查 | auto_review | 是 | repair-run 修复目标、范围、角色、约束缺失 |
| feature-spec-auto-review | 功能任务自检查 | auto_review | 是 | repair-run 补齐缺失 FEAT 小节和模块边界 |
| ui-ia-auto-review | UI 信息架构自检查 | auto_review | 是 | repair-run 补齐页面、导航、页面到功能映射 |
| ui-spec-auto-review | UI 规格自检查 | auto_review | 是 | repair-run 补齐 SCR 小节、组件和状态 |
| prototype-auto-review | 原型 Prompt 与标注自检查 | auto_review | 是 | repair-run 补齐 Prompt、标注和追踪关系 |
| baseline-auto-review | 基线与变更自检查 | auto_review | 是 | repair-run 补齐变更前后、影响范围和回归关注点 |

## 4. 人工评审输出格式

人工评审节点必须在文档末尾输出：

| 字段 | 内容 |
|---|---|
| review_gate | gate_id |
| review_type | human_review |
| review_status | ready_for_review / approved / rejected / needs_rework |
| must_stop | yes |
| user_decision_required | yes |
| suggested_decisions | 接受 / 修改 / 补充信息 / 重新生成 / 其他 |

## 5. 自动评审输出格式

自动评审节点必须在文档末尾输出：

| check_id | 检查项 | 结果 | 问题 | 修复动作 |
|---|---|---|---|---|
| CHECK-001 |  | pass / fail / pending |  | 无 / repair-run |

如果任一核心检查为 `fail`，本次节点不得标记为完成，必须进入 `repair-run` 或把失败项写入 `manifest.md`。
