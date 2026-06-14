# 模板索引兼容说明

本文件是历史兼容索引，不是运行时权威来源。

运行时必须使用 `registries/documents.md` 来确定：

- 目标输出路径
- 当前阶段
- 节点 flow
- 输出 template
- Review Gate
- gate_scope
- 是否需要中断

不要把本文件作为默认必读上下文；只有在维护旧适配器、排查模板路由兼容问题，或人工快速浏览模板目录时才读取。

## 运行时选择模板

```text
用户请求
  -> registries/actions.md 判断 execution_mode
  -> registries/documents.md 找到 doc_id / flow / template / gate
  -> 读取对应 flow
  -> 读取对应 template
  -> 执行 gate
```

## 兼容目录概览

| 目录 | 用途 |
|---|---|
| `templates/common/` | intake 和运行入口 |
| `templates/analysis/` | 01-03 分析阶段文档 |
| `templates/design/` | 04-10 设计阶段和基线文档 |
| `templates/prototype/` | prototype-input 派生产物 |
| `templates/state/` | workspace 和 instance 状态资产 |

repair-run 做结构迁移时，应读取目标文档在 `registries/documents.md` 中映射的模板，而不是凭本文件猜测。
