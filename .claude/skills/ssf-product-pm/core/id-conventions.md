# ID 协议

完整 ID 规则见 `references/id-conventions.md`。

本文件只保留运行时必须遵守的核心规则：

1. 所有关键对象必须有稳定 ID。
2. 不同文档不得为同一对象重复创建多个 ID。
3. 用户调研链路建议保持：

```text
SRC -> RAW -> INS -> NEED -> REQ
```

4. 产品设计链路建议保持：

```text
REQ -> CAP -> MOD -> OBJ -> FEAT -> SCR -> CMP -> AC
```

5. 变更链路建议保持：

```text
CHG -> ARCH-DELTA / FEAT / SCR / CMP / AC / REG
```

6. 自动检查必须带来源前缀，不使用裸 `CHECK-001`。
