# prototype-run 节点规则

## 1. 目标

基于当前实例的产品规格，生成面向原型工具的 `prototype-input/` 输入包。

prototype-run 不调用 Figma，不保证一次生成最终原型；它负责把 PM 规格重组为原型工具可稳定消费的执行材料。

## 2. 必读

执行前必须读取：

- `ssf-workspace/index.md`
- 目标实例 `manifest.md`
- `product-spec/04-product-architecture.md`
- `product-spec/05-prd.md`
- `product-spec/06-feature-task-spec.md`
- `product-spec/07-ui-ia-screen-inventory.md`
- `product-spec/08-structured-ui-interaction-spec.md`
- `product-spec/09-prototype-prompt-ui-annotation.md`
- `product-spec/10-product-baseline-change.md`

如果产品架构未通过 `product-architecture-human-review`，可以生成草案，但必须在 `prototype-input/07-prototype-review-checklist.md` 标记风险，且不得写成 ready for final prototype。

## 3. 输出目录

输出到目标实例内：

```text
instances/SPI-xxx/
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

## 4. 派生规则

| 输出文件 | 主要来源 | 作用 |
|---|---|---|
| `00-prototype-master-brief.md` | PRD / UI IA / UI Spec / Baseline | 原型总控 Prompt 和产品上下文压缩 |
| `01-design-system-constraints.md` | UI Spec 全局约束 / 人工补充 | 原型级设计边界 |
| `02-screen-contracts.md` | UI IA / UI Spec / Prototype Annotation | 每个 SCR 的页面合同 |
| `03-flow-contracts.md` | UI IA 导航 / Feature flows / Prototype flows | 可点击流程合同 |
| `04-sample-data.md` | PRD / Feature Spec / PM 补充 | 原型样例数据，不作为事实源 |
| `05-figma-make-prompts.md` | 09 原型 Prompt / 00-04 输入包 | Figma Make / prompt-to-prototype 提示词 |
| `06-ui-annotation-handoff.md` | UI Spec 组件表 / 09 标注表 | 给前端 AI 和测试 AI 的标注交付 |
| `07-prototype-review-checklist.md` | 09 一致性检查 / prototype-run 自检 | 原型输入包和生成后原型验收 |

## 5. 硬规则

- 不得把 `prototype-input/` 当成产品事实源。
- 不得修改 `product-spec/` 中的产品事实；发现缺口时写入 review checklist。
- 不得新增规格外页面、功能、按钮、业务流程。
- 样例数据只用于原型，不得回写为真实业务数据。
- `SCR` 应进入 Frame 名称或页面标注。
- `CMP` 应进入关键图层名、组件名或 annotation。
- `FEAT / BR / AC` 应进入 annotation、handoff table 或 test note。
- 不得把 ID 作为用户可见 UI 文案展示，除非用户明确要求。
- 未生成真实原型前，原型生成结果检查只能写 `pending`，不得提前写 `pass`。

## 6. Review Gate

执行 `prototype-input-auto-review`。

如果出现以下情况，必须标记 fail 并建议 repair-run 或补充输入：

- 必需页面缺失。
- 关键可交互组件缺少 `CMP`。
- `FEAT / BR / AC` 无法追踪到页面或组件。
- Figma / Motiff / Uizard prompt 允许新增规格外内容。
- 样例数据缺失，导致原型工具会自行编造核心业务内容。
- 原型检查在未生成原型前被写成 pass。
