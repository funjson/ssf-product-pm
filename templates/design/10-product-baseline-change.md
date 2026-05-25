# 10 产品基线与变更说明

> 本文档解决需求变更时 AI 不知道旧系统是什么的问题。它记录当前产品基线、关键决策、已确认规格和每次变更的影响范围。

## 0. 文档元信息

**生成说明**：明确当前基线版本和关联文档，保证 AI 变更时知道基于哪一版修改。

| 字段 | 内容 |
|---|---|
| document_id | BASELINE-CHANGE-001 |
| instance_id | SPI-xxx |
| current_version | v0.1 |
| previous_version | 无 / v0.1 |
| related_documents | REQ-ANALYSIS-001 / PRD-001 / PRODUCT-ARCH-001 / FEATURE-SPEC-001 / UI-IA-001 / UI-SPEC-001 / PROTOTYPE-ANNOTATION-001 |
| generated_at |  |
| review_gate | baseline-auto-review |
| review_status | draft / ready_for_review / needs_rework |

## 1. 当前产品基线摘要

**生成说明**：用压缩方式描述当前系统是什么，不重复粘贴完整 PRD。

| 项目 | 当前基线 |
|---|---|
| 产品定位 |  |
| 目标用户 |  |
| 核心目标 |  |
| 核心能力 |  |
| 产品模块 |  |
| 核心页面 |  |
| 核心流程 |  |
| 关键业务规则 |  |

## 2. 版本历史

**生成说明**：每次 `change-run` 后必须追加版本历史，并确保 `current_version` 等于最新 target_version。

| version | change_id | change_type | 摘要 | 状态 |
|---|---|---|---|---|
| v0.1 | CHG-001 | 新增 | 初始产品基线 | ready_for_review / approved |

## 3. 产品架构基线

**生成说明**：列出当前产品模块状态，避免后续变更时模块边界漂移。未经用户确认不得写 `approved`。

| module_id | 模块名称 | 当前状态 | 关联需求 | 关联功能任务 |
|---|---|---|---|---|
| MOD-001 |  | draft / ready_for_review / approved / deprecated / changing | REQ-xxx | FEAT-xxx |

## 4. 功能基线

**生成说明**：列出当前功能任务状态，避免 AI 在后续变更中误删或重复生成。未经用户确认不得写 `approved`。

| feature_id | 功能名称 | 当前状态 | 关联页面 | 关键规则 | 关键验收 |
|---|---|---|---|---|---|
| FEAT-001 |  | draft / ready_for_review / approved / deprecated / changing | SCR-xxx | BR-xxx | AC-xxx |

## 5. 页面基线

**生成说明**：记录当前页面和页面职责，防止变更时 AI 新增重复页面。未经用户确认不得写 `approved`。

| screen_id | 页面名称 | 页面职责 | 关联功能 | 当前状态 |
|---|---|---|---|---|
| SCR-001 |  |  | FEAT-xxx | draft / ready_for_review / approved / deprecated / changing |

## 6. 业务规则基线

**生成说明**：记录当前规则，避免 AI 修改功能时破坏既有业务约束。未经用户确认不得写 `approved`。

| rule_id | 规则名称 | 规则内容 | 关联功能 | 当前状态 |
|---|---|---|---|---|
| BR-001 |  |  | FEAT-xxx | draft / ready_for_review / approved / deprecated / changing |

## 7. 关键决策日志

**生成说明**：记录为什么这么设计，防止后续 AI 推翻历史决策或重复讨论。

| decision_id | 决策问题 | 最终决策 | 选择原因 | 影响范围 | 关联文档 |
|---|---|---|---|---|---|
| DEC-001 |  |  |  | FEAT-xxx / SCR-xxx |  |

## 8. 废弃设计清单

**生成说明**：明确哪些内容已经废弃，防止 AI 在后续任务中重新启用。

| deprecated_id | 废弃内容 | 原 ID | 废弃原因 | 替代方案 |
|---|---|---|---|---|
| DEP-001 |  |  |  |  |

---

## 9. 变更说明模板

> 每次变更重复使用本模板。

# CHG-xxx 变更名称

## 9.1 变更元信息

| 字段 | 内容 |
|---|---|
| change_id | CHG-xxx |
| base_version | v0.1 |
| target_version | v0.2 |
| change_type | 新增 / 修改 / 删除 / 替换 / 废弃 |
| change_reason |  |
| requester |  |

## 9.2 变更前

**生成说明**：必须明确旧系统是什么，不能只写“修改为”。

- 原功能：FEAT-xxx
- 原模块：MOD-xxx
- 原页面：SCR-xxx
- 原规则：BR-xxx
- 原验收：AC-xxx
- 原行为描述：

## 9.3 变更后

**生成说明**：明确新的产品行为、页面表现、规则和验收变化。

- 新功能行为：
- 新产品模块：
- 新页面表现：
- 新业务规则：
- 新验收标准：

## 9.4 影响范围分析

**生成说明**：这是变更文档核心，告诉后续 AI 哪些文档和功能要同步修改。

| affected_type | affected_id | 影响说明 | 是否改变边界 | 需要修改的内容 |
|---|---|---|---|---|
| PRD / PRODUCT_ARCH / ARCH_DELTA / MODULE / FEATURE / FLOW / RULE / SCREEN / COMPONENT / AC / TEST |  |  | yes / no / 不适用 |  |

## 9.5 回归关注点

**生成说明**：给测试 AI 使用，说明变更后哪些旧能力必须重新验证。

| regression_id | 回归对象 | 回归原因 | 关联验收 |
|---|---|---|---|
| REG-001 | FEAT-xxx / SCR-xxx |  | AC-xxx |

## 9.6 待确认问题

| question_id | 问题 | 影响范围 | 建议处理 |
|---|---|---|---|
| Q-001 |  |  |  |

## 10. 变更自检查模板

| check_id | 检查项 | 结果 | 问题 | 修复动作 |
|---|---|---|---|---|
| CHECK-CHG-xxx-001 | 是否限定局部影响范围 | pass / fail / pending |  | repair-run |
| CHECK-CHG-xxx-002 | 是否写明变更前后 | pass / fail / pending |  | repair-run |
| CHECK-CHG-xxx-003 | 若更新产品架构，是否记录 ARCH-DELTA 或触发人工评审 | pass / fail / pending |  | repair-run / human-review |
| CHECK-CHG-xxx-004 | 是否同步 manifest 与 index | pass / fail / pending |  | repair-run |
