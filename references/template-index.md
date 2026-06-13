# 模板索引

> 本文件是模板入口索引。Agent 不应凭记忆猜模板路径；执行某个阶段前先读取本文件确认应使用哪个模板和对应 Review Gate。

## 1. 公共能力

| 能力 | 模板 | 说明 |
|---|---|---|
| Intake 运行入口 | `templates/common/00-intake.md` | 判断实例、执行模式、写入策略和覆盖风险 |
| Workspace Index | `templates/state/workspace-index.md` | 工作区实例索引，所有落盘动作前必须读取；repair-run 必须按此模板迁移旧表 |
| Instance Manifest | `templates/state/instance-manifest.md` | 单实例控制中心，记录阶段、门禁、证据和运行记录 |

## 2. Analysis 分析阶段

| 阶段 | 模板 | Review Gate |
|---|---|---|
| 信息收集 | `templates/analysis/01-analysis-input.md` | analysis-human-review |
| 调研与洞察 | `templates/analysis/02-product-research-insight.md` | analysis-human-review |
| 需求分析 | `templates/analysis/03-requirement-analysis.md` | analysis-human-review |

分析阶段结束后必须中断流程，等待用户确认。未通过 `analysis-human-review` 不得进入设计阶段。

## 3. Design 设计阶段

| 阶段 | 模板 | Review Gate |
|---|---|---|
| 产品架构设计 | `templates/design/04-product-architecture.md` | product-architecture-human-review |
| PRD 产品需求文档 | `templates/design/05-prd.md` | prd-auto-review |
| 功能任务规格 | `templates/design/06-feature-task-spec.md` | feature-spec-auto-review |
| UI 信息架构 | `templates/design/07-ui-ia-screen-inventory.md` | ui-ia-auto-review |
| 结构化 UI/交互规格 | `templates/design/08-structured-ui-interaction-spec.md` | ui-spec-auto-review |
| 原型 Prompt 与 UI 标注 | `templates/design/09-prototype-prompt-ui-annotation.md` | prototype-auto-review |
| 产品基线与变更说明 | `templates/design/10-product-baseline-change.md` | baseline-auto-review |

产品架构评审是人工评审节点，必须中断流程。其他设计节点默认执行自动自检查，失败时进入 repair-run。

## 4. Prototype 原型输入包

| 阶段 | 模板 | Review Gate |
|---|---|---|
| 原型生成总控说明 | `templates/prototype/00-prototype-master-brief.md` | prototype-input-auto-review |
| 原型级设计系统约束 | `templates/prototype/01-design-system-constraints.md` | prototype-input-auto-review |
| 页面合同 | `templates/prototype/02-screen-contracts.md` | prototype-input-auto-review |
| 流程合同 | `templates/prototype/03-flow-contracts.md` | prototype-input-auto-review |
| 原型样例数据 | `templates/prototype/04-sample-data.md` | prototype-input-auto-review |
| Figma Make / 原型工具 Prompt | `templates/prototype/05-figma-make-prompts.md` | prototype-input-auto-review |
| UI 标注交付 | `templates/prototype/06-ui-annotation-handoff.md` | prototype-input-auto-review |
| 原型输入包与原型验收清单 | `templates/prototype/07-prototype-review-checklist.md` | prototype-input-auto-review |

prototype-run 只派生 `prototype-input/`，不修改 `product-spec/` 产品事实。未生成真实原型前，原型生成后检查必须保持 `pending`。

## 5. Repair 模板要求

repair-run 修复结构时，不得只修复用户指出的某一行，而必须对照对应模板进行结构迁移：

| 修复对象 | 模板 | 必须检查 |
|---|---|---|
| 工作区索引 | `templates/state/workspace-index.md` | 实例列表完整表头、index_version、当前流程状态 |
| 实例控制中心 | `templates/state/instance-manifest.md` | active_gate、blocked、Review Gate 状态、证据记录 |
| 产品基线与变更 | `templates/design/10-product-baseline-change.md` | previous_version、版本历史、CHG、CHECK-CHG |
| 自动评审正文 | 对应正文模板 | CHECK ID 是否带来源前缀 |
