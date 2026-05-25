# 04 产品架构设计

> 本文档定义产品能力结构、功能模块、模块边界、核心业务对象和需求到功能任务的组织关系。它不是技术架构文档，不写数据库、接口、缓存、消息队列、部署或模型供应商。

## 0. 文档元信息

**生成说明**：产品架构是设计阶段第一节点，位于需求分析之后、PRD 和功能任务规格之前，用于把平铺需求归纳为产品模块，避免直接从 REQ 跳到零散 FEAT。

| 字段 | 内容 |
|---|---|
| document_id | PRODUCT-ARCH-001 |
| instance_id | SPI-xxx |
| version | v0.1 |
| product_name |  |
| base_requirement_analysis | REQ-ANALYSIS-001 |
| base_analysis_review | analysis-human-review |
| generated_at |  |
| document_goal | 定义产品模块结构、模块边界、核心业务对象和 REQ 到 FEAT 的组织关系 |
| downstream_consumers | 产品经理 AI / 架构师 AI / 研发 AI / 测试 AI / 前端 AI |
| review_gate | product-architecture-human-review |
| review_status | draft / ready_for_review / ready_for_review_delta / approved / approved_with_delta / rejected / needs_rework |

## 1. 产品架构目标

**生成说明**：说明为什么需要这些模块，以及这些模块如何支撑产品目标。

| arch_goal_id | 架构目标 | 关联产品目标 | 说明 |
|---|---|---|---|
| PARCH-GOAL-001 |  | GOAL-xxx |  |

## 2. 模块划分策略

**生成说明**：产品架构是强交互节点，必须说明为什么采用这种模块划分方式，并给用户可选择的调整项。

| strategy_id | 划分方式 | 是否采用 | 采用 / 不采用原因 |
|---|---|---|---|
| ARCH-STRATEGY-001 | 按用户任务组织 | 是 / 否 / 部分采用 |  |
| ARCH-STRATEGY-002 | 按业务流程组织 | 是 / 否 / 部分采用 |  |
| ARCH-STRATEGY-003 | 按产品能力组织 | 是 / 否 / 部分采用 |  |
| ARCH-STRATEGY-004 | 按页面 / 端组织 | 是 / 否 / 部分采用 |  |
| ARCH-STRATEGY-005 | 按企业组织角色组织 | 是 / 否 / 部分采用 |  |

## 3. 产品能力地图

**生成说明**：用产品能力层级表达“用户看到的能力”和“支撑能力”之间的关系。能力不是技术服务，也不是研发任务。

| capability_id | 能力名称 | 能力类型 | 说明 | 关联需求 |
|---|---|---|---|---|
| CAP-001 |  | 核心用户能力 / 支撑能力 / 管理能力 / 体验能力 |  | REQ-xxx |

## 4. 功能模块清单

**生成说明**：模块是产品架构的基本组织单位。每个模块应有明确职责、边界和下游功能任务。

| module_id | 模块名称 | 模块职责 | 包含能力 | 不包含内容 | 关联需求 | 关联功能任务 |
|---|---|---|---|---|---|---|
| MOD-001 |  |  | CAP-xxx |  | REQ-xxx | FEAT-xxx |

## 5. 模块边界说明

**生成说明**：明确模块之间如何分工，防止后续 AI 把规则、页面或任务归错模块。

| module_id | 输入 | 输出 | 上游模块 | 下游模块 | 边界规则 |
|---|---|---|---|---|---|
| MOD-001 |  |  | MOD-xxx / 无 | MOD-xxx / 无 |  |

## 6. 核心业务对象

**生成说明**：只定义 PM 阶段需要稳定理解的业务对象，不设计数据库表。

| object_id | 业务对象 | 业务含义 | 关键属性概念 | 关联模块 | 关联规则 |
|---|---|---|---|---|---|
| OBJ-001 |  |  |  | MOD-xxx | BR-xxx |

## 7. 需求到模块映射

**生成说明**：每个核心 REQ 必须至少映射到一个模块；不能直接跳过模块进入功能任务。

| req_id | 需求描述 | 归属模块 | 映射理由 | 后续功能任务 |
|---|---|---|---|---|
| REQ-001 |  | MOD-xxx |  | FEAT-xxx |

## 8. 模块到功能任务映射

**生成说明**：用于指导功能任务规格文档如何组织 FEAT，避免任务平铺。

| module_id | 模块名称 | 功能任务 | 任务边界说明 | 任务生成状态 |
|---|---|---|---|---|
| MOD-001 |  | FEAT-xxx |  | 待生成 / 已生成 / 待确认 |

## 9. 产品架构图

**生成说明**：使用 Mermaid 画出模块关系。节点必须使用稳定 ID 和中文名称，便于后续还原为图。

```mermaid
flowchart TD
  MOD001["MOD-001 模块名称"]
  MOD002["MOD-002 模块名称"]
  MOD001 --> MOD002
```

## 10. 用户任务流与模块协作图

**生成说明**：用 Mermaid 表达用户完成核心任务时，各产品模块如何协作。不要写技术调用链。

```mermaid
sequenceDiagram
  participant User as 用户
  participant MOD001 as MOD-001 模块名称
  participant MOD002 as MOD-002 模块名称
  User->>MOD001: 执行用户动作
  MOD001->>MOD002: 产生产品层协作
  MOD002-->>User: 返回用户可见结果
```

## 11. 新项目与迭代处理规则

**生成说明**：说明当前产品架构是新建、继承、局部变更还是待补齐。

| 场景 | 处理方式 |
|---|---|
| 新项目 | 先建立完整模块地图，再生成 FEAT。 |
| 功能迭代 | 先读取既有 `PRODUCT-ARCH-001`，判断新增/修改/废弃哪些模块。 |
| 跳过产品架构 | 允许临时跳过，但必须在功能任务规格中标记模块归属为“待补齐”，并创建阻塞问题。 |
| 已有产品架构 | 不重复生成；基于旧架构追加变更说明。 |

## 12. 产品架构决策表

**生成说明**：本节用于支持后续按钮式交互。每个关键架构判断都必须给出当前建议、可选动作和影响范围。

| decision_id | 决策项 | 当前建议 | 可选动作 | 用户选择 | 影响范围 |
|---|---|---|---|---|---|
| ARCH-DEC-001 | 模块划分方式 | 按用户任务 + 产品能力组织 | 接受 / 合并模块 / 拆分模块 / 重命名模块 / 重新生成 / 其他 | 待确认 | MOD / FEAT / SCR |
| ARCH-DEC-002 | 核心业务对象是否合理 | 保留当前 OBJ 清单 | 接受 / 增加对象 / 删除对象 / 重命名对象 / 其他 | 待确认 | OBJ / BR / AC |
| ARCH-DEC-003 | 是否存在过度设计模块 | 当前无 / 指定模块 | 接受 / 合并 / 降级为功能 / 移出本期 / 其他 | 待确认 | MOD / FEAT / PRD |
| ARCH-DEC-004 | 是否存在缺失模块 | 当前无 / 指定缺口 | 接受 / 新增模块 / 放入已有模块 / 标记待确认 / 其他 | 待确认 | MOD / FEAT / UI |
| ARCH-DEC-005 | 模块边界是否清楚 | 当前边界可进入后续设计 | 接受 / 调整边界 / 补充规则 / 其他 | 待确认 | MOD / FEAT / BR |

## 13. 产品架构 Delta 记录

**生成说明**：当 change-run 修改产品架构但不改变模块边界时，必须记录本节。不得只沿用旧 `APR-xxx` 解释新增架构内容。

| architecture_delta_id | change_id | 变更内容 | 是否改变模块边界 | 评审方式 | 结果 | 说明 |
|---|---|---|---|---|---|---|
| ARCH-DELTA-001 | CHG-xxx | CAP-xxx / MOD-xxx / OBJ-xxx / ARCH-DEC-xxx | yes / no | product-architecture-delta-review / product-architecture-human-review | pass / escalated / pending |  |

## 14. Product Architecture Review Gate

> 产品架构评审是人机交互节点，必须中断流程等待用户确认。未通过前，不得进入 PRD、功能任务和 UI 设计。

| 字段 | 内容 |
|---|---|
| review_gate | product-architecture-human-review |
| review_type | human_review |
| review_status | ready_for_review / approved / rejected / needs_rework |
| must_stop | yes |
| user_decision_required | yes |
| approval_evidence | APR-xxx / 无 |
| suggested_decisions | 接受 / 修改 / 合并模块 / 拆分模块 / 重命名模块 / 补充对象 / 重新生成 / 其他 |

## 15. Product Architecture Delta Review

> 产品架构局部变更自检查用于处理不改变模块边界的小改动。若发现模块边界变化，必须升级为 `product-architecture-human-review`。

| check_id | 检查项 | 结果 | 问题 | 修复动作 |
|---|---|---|---|---|
| CHECK-ARCH-DELTA-001 | 是否新增/删除/合并/拆分 MOD | pass / fail / pending |  | fail 时升级人工评审 |
| CHECK-ARCH-DELTA-002 | 是否改变模块职责或上下游边界 | pass / fail / pending |  | fail 时升级人工评审 |
| CHECK-ARCH-DELTA-003 | 是否记录 ARCH-DELTA-xxx | pass / fail / pending |  | repair-run |
| CHECK-ARCH-DELTA-004 | 是否同步基线 CHG 影响范围 | pass / fail / pending |  | repair-run |

## 16. 待确认问题

| question_id | 问题 | 影响范围 | 建议处理 |
|---|---|---|---|
| Q-001 |  |  |  |
