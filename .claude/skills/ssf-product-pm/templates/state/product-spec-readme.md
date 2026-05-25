# product-spec 目录说明

> 本目录保存当前实例的产品设计文档。它只属于当前实例，不代表整个工作区的唯一产品规格。

## 1. 文档顺序

```text
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

## 2. 使用规则

- 先完成 Analysis：信息收集、调研与洞察、需求分析。
- Analysis 结束后必须人工评审，未确认不得默认进入 Design。
- Design 阶段先产品架构，再 PRD、功能任务和 UI。
- 产品架构结束后必须人工评审，未确认不得默认进入后续设计。
- `intake.md` 位于实例根目录，不属于 product-spec 版本文档。
- 单独生成某个文档时，必须在文档中标记缺失的上游输入。
- 修改已有规格时，必须同步更新 `10-product-baseline-change.md`。
- 每个关键对象必须使用稳定 ID，并能跨文档追踪。
