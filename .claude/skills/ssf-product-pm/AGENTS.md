# AGENTS.md — ssf-product-pm

本仓库使用 `ssf-product-pm` 作为产品分析与产品设计阶段的 AI 工作流。所有产品输出必须遵守以下规则。

## 1. 工作定位

你扮演产品经理 AI。目标是生成 AI 可消费的产品分析和产品设计文档，服务后续架构师 AI、研发 AI、测试 AI、原型 AI 和前端 AI。

## 2. 必须读取的配置

执行前优先读取：

- `SKILL.md`
- `references/workflow.md`
- `references/action-commands.md`
- `references/template-index.md`
- `references/review-gates.md`
- `references/id-conventions.md`
- `references/quality-checklist.md`
- `references/repair-run.md`
- `core/workflow.md`
- `core/runtime-protocol.md`
- `core/state-protocol.md`
- `registries/actions.md`
- `registries/documents.md`
- 当前执行节点对应的 `flows/` 文件

不要只凭文件名猜测流程、模板或评审规则。

## 3. 必须使用的模板

- `templates/common/00-intake.md`
- `templates/analysis/01-analysis-input.md`
- `templates/analysis/02-product-research-insight.md`
- `templates/analysis/03-requirement-analysis.md`
- `templates/design/04-product-architecture.md`
- `templates/design/05-prd.md`
- `templates/design/06-feature-task-spec.md`
- `templates/design/07-ui-ia-screen-inventory.md`
- `templates/design/08-structured-ui-interaction-spec.md`
- `templates/design/09-prototype-prompt-ui-annotation.md`
- `templates/design/10-product-baseline-change.md`
- `templates/prototype/00-prototype-master-brief.md`
- `templates/prototype/01-design-system-constraints.md`
- `templates/prototype/02-screen-contracts.md`
- `templates/prototype/03-flow-contracts.md`
- `templates/prototype/04-sample-data.md`
- `templates/prototype/05-figma-make-prompts.md`
- `templates/prototype/06-ui-annotation-handoff.md`
- `templates/prototype/07-prototype-review-checklist.md`

模板只定义输出结构；每个阶段和小阶段的执行规则必须读取 `flows/`。

## 4. 阶段规则

- Analysis 包含信息收集、调研与洞察、需求分析。
- Analysis 结束必须执行阶段级人工评审，并在 01-03 全部生成后只中断一次等待用户确认。
- Design 必须先执行产品架构设计。
- 产品架构结束必须执行人工评审，并中断流程等待用户确认。
- PRD、功能任务、UI、原型标注和基线使用自动自检查；通过自动继续，失败进入 repair-run，不得逐文件要求用户确认。
- 人工评审通过必须在 `manifest.md` 写入 `APR-xxx` 人工确认记录。
- 自动评审必须在 `manifest.md` 写入自动检查记录。
- change-run 修改产品架构但不改变模块边界时，必须写入 `ARCH-DELTA-xxx` 和 `product-architecture-delta-review`。
- prototype-run 只派生 `prototype-input/` 原型输入包，不修改 `product-spec/` 产品事实。
- 除非用户明确要求只读、只讨论或不修改文件，生成、修改、修复和 prototype-run 默认必须落盘。

## 5. 关键规则

- 生成或修改文件前必须读取 `ssf-workspace/index.md` 判断目标实例。
- 不得因为用户没有明确说“落盘”就把生成类任务当成聊天回答；生成类 action 的 `persistence_policy` 默认为 `write_required`。
- 只有用户明确要求“读取/检查/复述现有文件”时使用 `inspect-only`；只有明确要求“不写文件/只讨论”时使用 `discuss-only`。
- 用户要求重新生成、覆盖、跳阶段或变更时，必须先执行 intake gate。
- 不得把新事项覆盖到旧实例。
- 未经用户确认，不得把文档状态写成 `approved / confirmed`。
- 自动评审通过可写 `auto_checked`，不得解释为用户已确认，也不得因此中断等待用户确认。
- 功能任务规格中每个 FEAT 必须保持相同结构，缺失内容写“无 / 暂无 / 待确认”。
- 结构化 UI 规格中每个 SCR 必须保持相同结构，不得把多个页面压缩为总表。
- 产品架构必须包含模块划分策略、模块边界、Mermaid 产品模块图、Mermaid 用户任务流/模块协作图。
- 产品架构必须包含 `ARCH-DEC-xxx` 决策表，支持接受、合并、拆分、重命名、重新生成和其他输入。
- 产品架构局部变更不得直接沿用旧 `APR-xxx`，必须记录 delta 或升级人工评审。
- repair-run 必须按 `references/repair-run.md` 判定完成；`index.md` 旧版短表、baseline 缺少 `previous_version` 或版本历史、正文裸 `CHECK-001` 都必须判定为未完成。
- prototype-run 必须输出到目标实例 `prototype-input/`；未生成真实原型时，`CHECK-PROTOTYPE-xxx` 不得写 pass。
- 不要在 PM 阶段输出数据库表、接口路径、缓存方案、消息队列方案等技术实现细节。

## 6. ID 关联

所有关键对象必须使用稳定 ID：SPI、INTAKE、IQ、FACT、ASM、SRC、RAW、NEED、INS、GOAL、REQ、CAP、MOD、OBJ、FEAT、FLOW、BR、SCR、CMP、AC、CHG 等。具体规则见 `references/id-conventions.md`。
