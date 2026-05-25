# repair-run 节点规则

## 1. 使用协议

详细硬规则见：

`references/repair-run.md`

## 2. 目标

修复：

- index 结构。
- manifest 状态和证据。
- baseline 版本链。
- CHECK ID 一致性。
- 文档结构同构性。
- 跨文档追踪关系。

## 3. 完成标准

必须通过：

- `CHECK-REPAIR-001`
- `CHECK-REPAIR-002`
- `CHECK-REPAIR-003`
- `CHECK-REPAIR-004`
- `CHECK-REPAIR-005`

任一失败，不得写 repair complete。
