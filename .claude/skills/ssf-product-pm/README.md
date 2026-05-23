# ssf-product-pm

`ssf-product-pm` 是面向 AI 软件研发流程的产品经理 Skill。它负责把产品分析和产品设计沉淀成结构化、可追踪、可评审的文档，服务后续架构师 AI、研发 AI、测试 AI、原型 AI 和前端 AI。

## 核心设计

- 工作流分为 `Analysis 分析阶段` 和 `Design 设计阶段`。
- Analysis 包含信息收集、市场/竞品调研、客户现场/用户需求调研、需求分析。
- Design 必须先做产品架构，再做 PRD、功能任务、UI 和基线。
- 分析阶段评审和产品架构评审是人工评审，必须中断流程等待用户确认。
- 其他设计节点使用自动自检查，失败时进入 `repair-run`。
- 使用 `ssf-workspace/index.md` 管理多个隔离实例，避免新事项覆盖旧事项。
- 流程、动作指令、模板索引、Review Gate 和质量规则都独立管理，便于后续调整。

## 配置文件

```text
references/
  workflow.md
  action-commands.md
  template-index.md
  review-gates.md
  id-conventions.md
  quality-checklist.md
```

Agent 执行前应先读取这些配置，再按模板生成。

## 模板清单

```text
templates/
  00-intake.md
  01-analysis-input.md
  02-product-research-insight.md
  03-requirement-analysis.md
  04-product-architecture.md
  05-prd.md
  06-feature-task-spec.md
  07-ui-ia-screen-inventory.md
  08-structured-ui-interaction-spec.md
  09-prototype-prompt-ui-annotation.md
  10-product-baseline-change.md
  workspace-readme.md
  workspace-index.md
  instances-readme.md
  instance-manifest.md
  product-spec-readme.md
```

## 默认输出目录

```text
ssf-workspace/
  README.md
  index.md
  instances/
    README.md
    SPI-xxx/
      manifest.md
      intake.md
      product-spec/
        README.md
        01-analysis-input.md
        02-research-insight.md
        03-requirement-analysis.md
        04-product-architecture.md
        05-prd.md
        06-feature-task-spec.md
        07-ui-ia-screen-inventory.md
        08-structured-ui-interaction-spec.md
        09-prototype-prompt-ui-annotation.md
        10-product-baseline-change.md
```

## 关键规则

- 写文件前必须读取 `ssf-workspace/index.md` 和目标实例 `manifest.md`。
- 重新生成、覆盖、跳阶段、变更和实例不清时必须执行 `00-intake.md`。
- Analysis 未通过人工评审，不得默认进入 Design。
- 产品架构未通过人工评审，不得默认进入 PRD、功能任务和 UI。
- 功能任务和 UI 页面必须同构完整展开，不得用摘要或总表压缩。
- 未经用户确认，文档状态不得写 `approved / confirmed`。
