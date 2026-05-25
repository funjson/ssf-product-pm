# Review Gate 协议

## 1. Review 类型

| 类型 | 含义 | 是否中断 |
|---|---|---|
| human_review | 人工评审 | 是 |
| auto_review | 自动自检查 | 否 |

## 2. 人工评审

人工评审必须给用户决策入口：

```text
接受 / 修改 / 补充信息 / 重新生成 / 其他
```

通过后必须写入：

- `APR-xxx`
- 用户原话
- 确认范围
- 确认时间

## 3. 自动评审

自动评审必须使用带来源前缀的 `CHECK` ID。

示例：

- `CHECK-PRD-001`
- `CHECK-FEAT-001`
- `CHECK-UISPEC-001`
- `CHECK-CHG-002-001`

禁止使用裸编号 `CHECK-001`。

## 4. 架构 Delta

产品架构局部变更但不改变模块边界时：

- 写入 `ARCH-DELTA-xxx`。
- 执行 `product-architecture-delta-review`。
- 同步 `manifest.md` 和 baseline。

改变模块边界时：

- 不得使用 `approved_with_delta`。
- 必须进入 `product-architecture-human-review`。
