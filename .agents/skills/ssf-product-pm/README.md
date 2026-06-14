# ssf-product-pm

`ssf-product-pm` 是面向 AI 软件研发流程的产品经理 Skill。它把产品分析和产品设计沉淀成结构化、可追踪、可评审的文档，供后续架构师 AI、研发 AI、测试 AI、原型 AI 和前端 AI 消费。

## 核心设计

- `SKILL.md` 是运行时入口和路由器，不承载所有细节。
- `core/` 定义工作流、运行时、状态和评审协议。
- `registries/` 定义 action、document、gate 和 check 的映射。
- `flows/` 定义阶段、节点、change-run、prototype-run 和 repair-run 的执行规则。
- `templates/` 定义输出结构。
- `references/` 存放按需读取的详细规则、兼容说明和质量/修复指南。

运行时以 `registries/documents.md` 作为文档路径、flow、template、review gate 和中断行为的权威映射。`registries/templates.md` 与 `references/template-index.md` 只作为兼容索引。

## 流程模型

```text
User request
  -> action detection
  -> persistence policy
  -> instance resolution
  -> flow/template routing
  -> artifact write or read-only inspection
  -> review gate
  -> state sync
```

Analysis 包含 01-03 三份文档，并在全部完成后统一进入 `analysis-human-review`。Design 必须先完成产品架构，并在 `product-architecture-human-review` 后才继续 PRD、功能任务、UI 和基线。后续设计节点使用自动评审，通过后自动继续，失败时进入 `repair-run`。

`prototype-run` 是 Design 之后的派生流程，只生成目标实例内 `prototype-input/`，不修改 `product-spec/` 产品事实。

## 运行时读取策略

Agent 不应默认读取所有文件。推荐顺序：

1. 读取 `SKILL.md`。
2. 读取 `core/workflow.md`、`core/runtime-protocol.md`、`core/state-protocol.md`。
3. 读取 `registries/actions.md`、`registries/documents.md`、`registries/gates.md`。
4. 按当前 action、document、gate 读取对应 `flows/`、`templates/` 和必要的 `references/`。

按需引用：

- 用户意图不清：`references/action-commands.md`
- 执行或更新评审：`references/review-gates.md`
- 新增或修复 ID：`references/id-conventions.md`
- 自动检查或 repair：`registries/checks.md`
- repair-run：`references/repair-run.md`
- 质量审计：`references/quality-checklist.md`

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
      prototype-input/
        00-prototype-master-brief.md
        01-design-system-constraints.md
        02-screen-contracts.md
        03-flow-contracts.md
        04-sample-data.md
        05-figma-make-prompts.md
        06-ui-annotation-handoff.md
        07-prototype-review-checklist.md
```

## 不变量

- 生成、修改、修复、续跑、重跑、变更和 prototype-run 默认必须落盘。
- 只有用户明确要求读取、检查、复述或审阅现有文件时，才使用 `inspect-only`。
- 只有用户明确要求先讨论、先讲方案、不写文件或不要修改时，才使用 `discuss-only`。
- 只有 `analysis-human-review` 和 `product-architecture-human-review` 能中断等待用户确认。
- 自动评审通过后继续流程，失败时进入 repair-run。
- `index.md` 与目标 `manifest.md` 是流程判断依据，写入正文产物后必须同步。
- 功能任务和 UI 页面必须同构完整展开，不得用摘要或总表压缩。
- PM 文档不写数据库、接口、缓存、队列、部署等技术实现细节。
