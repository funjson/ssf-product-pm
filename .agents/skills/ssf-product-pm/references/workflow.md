# ssf-product-pm 工作流说明

## 1. 设计目标

本工作流把产品经理的分析与设计活动转化为 AI 可消费的产品规格产物。它不是简单按编号生成文档，而是先建立事实与需求证据，再进入产品设计。

核心分层：

```text
Intake 运行入口
  ↓
Analysis 分析阶段
  ↓ 人工评审，中断等待用户确认
Design 设计阶段
  ↓ 产品架构人工评审，中断等待用户确认
后续设计文档自动自检查
```

## 2. Workflow 配置化原则

- `SKILL.md` 只保留入口规则和读取顺序。
- 本文件定义主工作流。
- `references/action-commands.md` 定义动作指令。
- `references/template-index.md` 定义阶段到模板的映射。
- `references/review-gates.md` 定义人工评审和自动评审规则。
- `references/quality-checklist.md` 定义质量检查项。

Agent 执行前必须先读取以上配置，不得只凭文件名猜流程。

## 3. Analysis 分析阶段

分析阶段目标是回答：

```text
这个产品为什么要做？
真实用户是谁？
客户现场发生了什么？
已有材料和约束是什么？
哪些是事实，哪些是模型假设？
哪些需求可以进入设计？
```

默认顺序：

```text
01 分析输入与信息收集
  ↓
02 产品调研与洞察
  ↓
03 需求分析
  ↓
analysis-human-review
```

### 3.1 信息收集

使用 `templates/analysis/01-analysis-input.md`。它收集产品基本信息、用户现场信息、已有系统材料、市场/竞品材料和待确认问题。

如果用户没有提供足够信息，允许模型补充，但必须标记为“模型假设 / 待确认”，不能伪装成事实。

### 3.2 产品调研与洞察

使用 `templates/analysis/02-product-research-insight.md`。它合并市场调研、竞品分析、客户现场调研和用户访谈材料，输出洞察与设计影响。

### 3.3 需求分析

使用 `templates/analysis/03-requirement-analysis.md`。它把 `RAW / INS / NEED / PROB` 转成 `REQ`，明确需求边界、排除项、假设和后续设计输入。

### 3.4 分析阶段人工评审

分析阶段必须执行 `analysis-human-review`。这是人机交互节点，必须中断流程，等待用户确认、补充或驳回。

未通过前，不得继续生成设计阶段文档。若用户强行要求继续，必须在后续文档显式标记“分析阶段未人工确认”。

## 4. Design 设计阶段

设计阶段目标是回答：

```text
产品能力如何组织？
需求归入哪些产品模块？
模块边界是什么？
每个功能任务如何执行？
UI 页面如何承载功能？
原型和 UI 标注如何服务前端 AI？
当前基线如何支持后续变更？
```

默认顺序：

```text
04 产品架构设计
  ↓
product-architecture-human-review
  ↓
05 PRD 产品需求文档
  ↓
06 功能任务规格
  ↓
07 UI 信息架构
  ↓
08 结构化 UI/交互规格
  ↓
09 原型 Prompt 与 UI 标注
  ↓
10 产品基线与变更说明
```

### 4.1 产品架构设计

产品架构是设计阶段第一节点。新项目和功能迭代都必须先检查产品架构。

- 新项目：建立 `CAP / MOD / OBJ`，明确模块边界，再进入后续设计。
- 功能迭代：读取已有产品架构，判断新增、修改、废弃哪些模块。
- 小调整：先判断是否影响模块边界；不影响则只局部更新后续文档。
- 跳过产品架构：允许临时跳过，但后续文档必须标记 `related_module = 待补齐`，并创建阻塞问题。

产品架构评审使用 `product-architecture-human-review`，必须中断流程等待用户确认。

### 4.2 PRD

PRD 在产品架构之后生成，用于表达产品总上下文、目标、范围、角色、约束和产品级成功标准。PRD 不承载全部功能细节。

### 4.3 功能任务规格

功能任务规格是后续架构、研发、测试的主输入。每个 `FEAT` 必须完整展开，不能摘要化。

### 4.4 UI 信息架构与结构化 UI

UI 文档必须基于产品架构和功能任务生成。每个 `SCR` 必须关联 `MOD / FEAT / REQ / AC`。

### 4.5 产品基线与变更

基线用于后续变更、续跑和上下文恢复。任何局部更新都必须同步影响范围和回归关注点。

## 5. Review 规则

- 分析阶段评审：人工评审，必须中断。
- 产品架构评审：人工评审，必须中断。
- 其他节点评审：自动自检查，失败时进入 repair-run。
- 任何自动评审通过都不等于用户确认，不得把文档写成 `approved / confirmed`。
- 人工评审通过必须在实例 `manifest.md` 中写入 `APR-xxx` 人工确认记录，并由 Review Gate 状态引用该证据。
- 自动评审必须在实例 `manifest.md` 中写入自动检查记录；失败时必须设置 `blocked = yes` 和 `next_allowed_actions = repair-run`。
- 产品架构局部变更但不改变模块边界时，必须记录 `ARCH-DELTA-xxx`，并执行 `product-architecture-delta-review`。

具体规则见 `references/review-gates.md`。

## 6. 流程状态资产

`index.md` 和 `manifest.md` 是流程判断依据，不是附属说明。

### 6.1 Workspace Index

`ssf-workspace/index.md` 用于跨实例调度，必须记录：

- 当前阶段。
- 当前状态。
- 阻塞 Review Gate。
- 最近运行模式。
- 下一步建议动作。
- 实例摘要和路径。

Agent 判断新流程、旧流程、续跑、变更或 repair-run 时，必须先读取它。

### 6.2 Instance Manifest

`instances/<instance-id>/manifest.md` 是单实例控制中心，必须记录：

- `current_phase`
- `active_gate`
- `blocked`
- `current_blocker`
- `next_allowed_actions`
- 文档状态
- Review Gate 状态
- 人工确认记录
- 自动检查记录
- 运行记录
- 待确认问题

如果 `manifest.md` 显示阻塞在人工 Review Gate，Agent 不得继续生成后续阶段文档，除非用户明确确认并生成 `APR-xxx`。

如果 change-run 修改了产品架构但 `manifest.md` 未记录 `ARCH-DELTA-xxx` 或 `product-architecture-human-review`，本次变更不合格，必须 repair-run。

## 7. 局部执行与成本控制

为了避免每次小调整都全量重跑，执行任何变更前必须判断影响范围：

| 变更类型 | 默认处理 |
|---|---|
| 分析事实变化 | 更新 Analysis，重新执行分析人工评审 |
| 新增需求 | 检查产品架构，更新受影响的 MOD / FEAT / UI |
| 模块边界变化 | 更新产品架构并执行产品架构人工评审 |
| 产品架构局部补充但不改边界 | 记录 `ARCH-DELTA-xxx`，执行 `product-architecture-delta-review` |
| 单个功能变化 | 更新对应 FEAT、相关 UI、基线和变更说明 |
| 纯 UI 文案或展示变化 | 更新 UI 相关文档和基线，不全量重跑 Analysis |
| 原型标注缺失 | repair-run 修复 UI 标注，不改变需求事实 |

## 8. 实例与跳阶段规则

### 8.1 实例判断

每个独立产品、功能事项或变更任务都是一个实例。实例由 `ssf-workspace/index.md` 统一登记，由 `instances/<instance-id>/manifest.md` 记录状态。

新事项不得覆盖旧实例。无法判断时必须让用户选择：新建实例、作为已有实例变更、修复已有实例、只讨论不落盘。

### 8.2 跳阶段执行

允许用户直接执行某个阶段，但必须显式说明：

- 本阶段需要哪些上游输入。
- 当前实例已有哪些上游输入。
- 缺失哪些上游输入。
- 本次基于哪些假设生成。
- 哪些内容需要后续回填到上游文档。

### 8.3 同构输出处理

- 功能任务规格和结构化 UI 规格必须逐个对象完整展开。
- 不允许用“后续同上”“若干页面总表”“FEAT-006 至 FEAT-014 摘要”代替完整结构。
- 输出过长时，分批生成或进入 repair-run 补齐，不得压缩结构。
