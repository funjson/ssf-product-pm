# change-run 节点规则

## 1. 目标

处理基于已有实例的新增需求、功能调整、UI 调整或规则变化。

## 2. 必读

- `ssf-workspace/index.md`
- 目标实例 `manifest.md`
- `product-spec/04-product-architecture.md`
- `product-spec/10-product-baseline-change.md`

## 3. 影响范围判断

| 变更类型 | 默认处理 |
|---|---|
| 分析事实变化 | 回到 Analysis 并重新人工评审 |
| 新增需求 | 判断产品架构影响，再更新后续文档 |
| 模块边界变化 | 产品架构人工评审 |
| 架构局部补充 | architecture-delta |
| 单功能变化 | 更新对应 FEAT、UI、baseline |
| 纯 UI 变化 | 更新 UI 规格、原型标注、baseline |

## 4. 输出

change-run 必须在 baseline 中写入 `CHG-xxx`，包含：

- 变更前。
- 变更后。
- 影响范围。
- 是否改变模块边界。
- 回归关注点。

## 5. Review Gate

执行 `change-run-local-review`。如果发现模块边界变化，升级到 `product-architecture-human-review`。
