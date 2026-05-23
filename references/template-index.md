# 模板索引

> 本文件是模板入口索引。Agent 不应凭记忆猜模板路径；执行某个阶段前先读取本文件确认应使用哪个模板和对应 Review Gate。

## 1. 公共能力

| 能力 | 模板 | 说明 |
|---|---|---|
| Intake 运行入口 | `templates/00-intake.md` | 判断实例、执行模式、写入策略和覆盖风险 |

## 2. Analysis 分析阶段

| 阶段 | 模板 | Review Gate |
|---|---|---|
| 信息收集 | `templates/01-analysis-input.md` | analysis-human-review |
| 调研与洞察 | `templates/02-product-research-insight.md` | analysis-human-review |
| 需求分析 | `templates/03-requirement-analysis.md` | analysis-human-review |

分析阶段结束后必须中断流程，等待用户确认。未通过 `analysis-human-review` 不得进入设计阶段。

## 3. Design 设计阶段

| 阶段 | 模板 | Review Gate |
|---|---|---|
| 产品架构设计 | `templates/04-product-architecture.md` | product-architecture-human-review |
| PRD 产品需求文档 | `templates/05-prd.md` | prd-auto-review |
| 功能任务规格 | `templates/06-feature-task-spec.md` | feature-spec-auto-review |
| UI 信息架构 | `templates/07-ui-ia-screen-inventory.md` | ui-ia-auto-review |
| 结构化 UI/交互规格 | `templates/08-structured-ui-interaction-spec.md` | ui-spec-auto-review |
| 原型 Prompt 与 UI 标注 | `templates/09-prototype-prompt-ui-annotation.md` | prototype-auto-review |
| 产品基线与变更说明 | `templates/10-product-baseline-change.md` | baseline-auto-review |

产品架构评审是人工评审节点，必须中断流程。其他设计节点默认执行自动自检查，失败时进入 repair-run。
