# AGENTS.md — ssf-product-pm

本仓库使用 `ssf-product-pm` 作为产品分析与产品设计阶段的 AI 工作流。项目级规则只负责路由，详细执行规则以 `SKILL.md`、`core/`、`flows/`、`registries/`、`references/` 和 `templates/` 为准。

## 1. 读取策略

执行 PM 工作流时先读：

- `SKILL.md`
- `core/workflow.md`
- `core/runtime-protocol.md`
- `core/state-protocol.md`
- `registries/actions.md`
- `registries/documents.md`
- `registries/gates.md`

按需读取：

- 当前执行模式或文档对应的 `flows/` 文件。
- 当前输出对应的 `templates/` 文件。
- `registries/checks.md`：执行自动评审、repair-run 或检查 ID 时。
- `references/action-commands.md`：用户意图或执行模式不清时。
- `references/review-gates.md`：执行或更新 Review Gate 时。
- `references/id-conventions.md`：新增 ID 或修复追踪链路时。
- `references/quality-checklist.md`：最终 QA、审计或大范围一致性检查时。
- `references/repair-run.md`：仅 repair-run 使用。

不要默认一次性读取全部 references 或全部 templates。`registries/documents.md` 是文档路径、模板、flow 和 gate 映射的运行时权威来源。

## 2. 硬规则

- 生成、修改、修复、续跑、重跑、变更和 prototype-run 默认都是 `write_required`，除非用户明确要求只读、只讨论或不修改文件。
- `inspect-only` 只用于用户明确要求读取、检查、复述、审阅现有文件且没有生成/修改诉求。
- `discuss-only` 只用于用户明确要求先讨论、先讲方案、不要写文件或不要修改。
- 写文件前必须读取或创建 `ssf-workspace/index.md`，并解析目标 `instances/SPI-xxx/manifest.md`。
- 重新生成、覆盖、删除旧内容、跳阶段、继续旧实例、基于旧版本变更或实例归属不清时，先执行 `templates/common/00-intake.md`。
- 结束 `write_required` 任务前必须同步 `index.md`、`manifest.md` 和必要的 baseline/change 记录，并在最终回复列出实际写入路径。

## 3. 评审中断

只允许两个 gate 中断并等待用户确认：

- `analysis-human-review`：Analysis 01-03 全部完成后统一中断一次。
- `product-architecture-human-review`：`04-product-architecture.md` 完成后中断一次。

PRD、功能任务、UI IA、结构化 UI、原型标注、baseline、prototype-input 使用自动评审。自动评审通过后继续下一节点，失败时进入 repair-run，不得逐文件要求用户确认。

人工评审通过必须在 `manifest.md` 写入 `APR-xxx` 和用户原话。自动评审通过只能写 `auto_checked`，不得解释为用户已确认。

## 4. 输出边界

- PM 阶段不写数据库表、接口路径、缓存、消息队列、部署方案等技术实现细节。
- 功能任务规格中每个 `FEAT` 必须保持完整同构结构。
- UI 规格中每个 `SCR` 必须保持完整同构结构。
- 产品架构局部变更不改变模块边界时，记录 `ARCH-DELTA-xxx` 并执行 `product-architecture-delta-review`；改变模块边界时进入 `product-architecture-human-review`。
- `prototype-run` 只派生目标实例内 `prototype-input/`，不得修改 `product-spec/` 产品事实。
- 原型输入包中的 `SCR / CMP / FEAT / BR / AC` 用于 frame、layer、annotation 或 handoff，不作为用户可见 UI 文案。
