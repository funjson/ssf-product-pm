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
- 运行协议、阶段规则、注册表和模板已分层：`core/`、`flows/`、`registries/`、`templates/`。
- `manifest.md` 是单实例流程控制中心，记录当前阶段、阻塞点、Review Gate、人工确认和自动检查。
- 人工评审通过必须有 `APR-xxx` 证据；自动评审通过只代表自检查通过。
- 产品架构小改不改模块边界时走 `ARCH-DELTA-xxx` 和 `product-architecture-delta-review`，改模块边界才重新进入人工评审。

## 配置文件

```text
core/
  workflow.md
  runtime-protocol.md
  state-protocol.md
  review-protocol.md
  id-conventions.md

flows/
  analysis/
  design/
  change/
  repair/

registries/
  actions.md
  documents.md
  gates.md
  checks.md
  templates.md

references/
  workflow.md
  action-commands.md
  template-index.md
  review-gates.md
  id-conventions.md
  quality-checklist.md
  repair-run.md
```

Agent 执行前应先读取这些配置，再按模板生成。

## 模板清单

```text
templates/
  common/
  analysis/
  design/
  state/
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
- `index.md` 和 `manifest.md` 必须同步更新，后续判断新旧流程、跳阶段和 repair-run 都依赖它们。
- 功能任务和 UI 页面必须同构完整展开，不得用摘要或总表压缩。
- 未经用户确认，文档状态不得写 `approved / confirmed`。
- 变更后的 baseline 版本、变更记录、自动检查 ID 必须保持一致。
- `repair-run` 必须按 `references/repair-run.md` 完成结构修复；`index.md` 旧版短表、baseline 缺版本历史、正文裸 `CHECK-001` 都不能判定为完成。
- 每个阶段和小阶段的规则放在 `flows/`；模板只定义输出结构，不承载流程判断。
