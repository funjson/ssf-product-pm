# ssf-product-pm

`ssf-product-pm` 是一个面向 AI 软件研发全流程的产品经理 Skill。它用于生成产品设计阶段的结构化文档，服务后续架构师 AI、研发 AI、测试 AI、原型 AI 和前端 AI。

## 文档清单

公共入口能力：

- Intake 信息收集模板：`templates/00-intake.md`

产品版本文档：

1. 产品调研与洞察报告
2. 需求分析说明
3. PRD 产品需求文档
4. 产品架构设计
5. 功能任务规格文档
6. UI 信息架构与页面清单
7. 结构化 UI/交互规格
8. 原型生成 Prompt 与 UI 标注说明
9. 产品基线与变更说明

## 核心设计

- 不做传统需求管理、排期、Roadmap、下一期规划。
- 使用 `ssf-workspace/index.md` 管理多个彼此隔离的产品设计实例，避免新事项覆盖旧事项。
- 支持完整生成、续跑、跳阶段、单文档生成和变更修改。
- 用户要求重新生成、覆盖、跳阶段或变更时，先执行 intake gate。
- 产品设计顺序是“调研与洞察 → 需求分析 → PRD → 产品架构 → 功能任务规格”。
- 调研文档必须包含项目基本描述和用户现场/访谈需求证据。
- 产品架构把需求归纳到产品模块，再进入功能任务。
- 以功能任务为 AI Coding 的主输入单元。
- 每个功能任务必须保持相同结构；无内容时显式写“无 / 暂无 / 待确认”。
- 每个 UI 页面必须保持相同结构；不得把多个页面合并成压缩总表。
- 流程、规则、验收标准合并到功能任务规格中。
- UI 相关文档独立，但通过 `screen_id`、`component_id`、`feature_id`、`rule_id`、`ac_id` 关联。
- 原型不是事实源；结构化 UI 规格和 UI 标注是事实源。
- 产品基线与变更说明用于支持需求变更和上下文恢复。

## 目录结构

```text
ssf-product-pm/
  SKILL.md
  AGENTS.md
  README.md
  templates/
    00-intake.md
    01-product-research-insight.md
    02-requirement-analysis.md
    03-prd.md
    04-product-architecture.md
    05-feature-task-spec.md
    06-ui-ia-screen-inventory.md
    07-structured-ui-interaction-spec.md
    08-prototype-prompt-ui-annotation.md
    09-product-baseline-change.md
    workspace-readme.md
    workspace-index.md
    instances-readme.md
    instance-manifest.md
    product-spec-readme.md
  references/
    id-conventions.md
    workflow.md
    quality-checklist.md
  .claude/skills/ssf-product-pm/SKILL.md
  .agents/skills/ssf-product-pm/SKILL.md
  .cursor/rules/ssf-product-pm.mdc
  .qoder/rules/ssf-product-pm.md
  .trae/rules/project_rules.md
```

## 使用建议

- Claude Code / Codex：优先使用 `SKILL.md`。
- Cursor / Qoder / Trae：使用规则文件把 Agent 指向同一套模板和工作流。
- 跨平台使用时，不要维护多份不同版本模板；模板目录应作为唯一事实源。

## 默认输出目录

生成文件时，默认创建或复用：

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
        01-research-insight.md
        02-requirement-analysis.md
        03-prd.md
        04-product-architecture.md
        05-feature-task-spec.md
        06-ui-ia-screen-inventory.md
        07-structured-ui-interaction-spec.md
        08-prototype-prompt-ui-annotation.md
        09-product-baseline-change.md
```

Agent 每次写入前必须读取 `ssf-workspace/index.md`，判断目标实例；如果当前请求与已有实例不是同一件事，默认不覆盖。
