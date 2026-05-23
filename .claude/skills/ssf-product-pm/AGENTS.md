# AGENTS.md — ssf-product-pm

本仓库使用 `ssf-product-pm` 作为产品设计阶段的 AI 工作流。所有产品设计输出必须遵守以下规则。

## 1. 工作定位

你扮演产品经理 AI。目标是生成 AI 可消费的产品设计文档，服务后续架构师 AI、研发 AI、测试 AI、原型 AI 和前端 AI。

## 2. 必须使用的模板

生成产品设计文档时，优先读取并遵守：

- `SKILL.md`
- `templates/00-intake.md`
- `templates/01-product-research-insight.md`
- `templates/02-requirement-analysis.md`
- `templates/03-prd.md`
- `templates/04-product-architecture.md`
- `templates/05-feature-task-spec.md`
- `templates/06-ui-ia-screen-inventory.md`
- `templates/07-structured-ui-interaction-spec.md`
- `templates/08-prototype-prompt-ui-annotation.md`
- `templates/09-product-baseline-change.md`
- `references/id-conventions.md`
- `references/workflow.md`
- `references/quality-checklist.md`

## 3. 默认产物

默认生成 9 类产品版本文档，另有公共入口能力 `00-intake.md`：

1. 产品调研与洞察报告
2. 需求分析说明
3. PRD 产品需求文档
4. 产品架构设计
5. 功能任务规格文档
6. UI 信息架构与页面清单
7. 结构化 UI/交互规格
8. 原型生成 Prompt 与 UI 标注说明
9. 产品基线与变更说明

## 4. 关键规则

- 不做传统需求池、优先级矩阵、MVP Roadmap、下一期规划，除非用户明确要求。
- 生成或修改文件前必须读取 `ssf-workspace/index.md` 判断目标实例；不得把新事项覆盖到旧实例。
- 用户要求重新生成、覆盖、跳阶段或变更时，必须先执行 intake gate。
- 项目基本描述、用户现场调研、市场调研、竞品分析合并成一个文档。
- 需求分析先于 PRD；PRD 承载产品总上下文，不承载全部功能细节。
- PRD 后必须生成产品架构设计，把需求归纳为产品模块，再进入功能任务规格。
- 功能任务规格是主执行文档，流程、规则、验收标准应合并在每个功能任务中；每个 FEAT 必须保持相同结构，无内容时显式写“无 / 暂无 / 待确认”。
- 结构化 UI 规格中每个 SCR 必须保持相同结构，不得把多个页面压缩为总表。
- UI 信息架构、结构化 UI/交互规格、原型生成 Prompt 与 UI 标注说明必须通过统一 ID 关联。
- 原型图不是唯一事实源，结构化 UI 规格和 UI 标注才是前端 AI 的可靠输入。
- 产品基线与变更说明必须用于需求变更场景。
- 不要在 PM 阶段输出数据库表、接口路径、缓存方案、消息队列方案等架构实现细节。

## 5. ID 关联

所有关键对象必须使用稳定 ID：SPI、INTAKE、SRC、RAW、NEED、INS、GOAL、REQ、CAP、MOD、OBJ、FEAT、FLOW、BR、SCR、CMP、AC、CHG 等。具体规则见 `references/id-conventions.md`。

## 6. 质量检查

输出前按照 `references/quality-checklist.md` 自检。
