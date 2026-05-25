# Design Flow

## 1. 前置条件

进入 Design 前应满足：

- Analysis 文档存在。
- `analysis-human-review` 已通过，或明确标记未确认风险。

## 2. 节点顺序

```text
04 产品架构设计
  ↓ product-architecture-human-review
05 PRD
06 功能任务规格
07 UI 信息架构
08 结构化 UI/交互规格
09 原型 Prompt 与 UI 标注
10 产品基线与变更
```

## 3. 核心规则

- 产品架构必须先于 PRD 和功能任务。
- 功能任务必须归属产品模块。
- UI 页面必须关联功能任务和模块。
- Baseline 必须记录版本和变更。

## 4. 自动检查

产品架构之后的设计节点默认使用自动自检查。失败进入 repair-run。
