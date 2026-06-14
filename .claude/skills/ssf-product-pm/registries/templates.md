# 模板兼容索引

`registries/documents.md` 是运行时权威来源，已经同时声明：

- 输出文件路径
- 阶段
- 节点 flow
- 输出 template
- Review Gate
- 是否中断

本文件仅保留给旧适配器或人工快速查阅，不参与运行时决策。Agent 需要选择模板时，应读取 `registries/documents.md`，不要在本文件和 `references/template-index.md` 之间做二次推断。

## 模板目录

| 类型 | 目录 | 用途 |
|---|---|---|
| common | `templates/common/` | intake 和运行入口 |
| analysis | `templates/analysis/` | 01-03 分析阶段文档 |
| design | `templates/design/` | 04-10 设计阶段与基线文档 |
| prototype | `templates/prototype/` | prototype-input 派生产物 |
| state | `templates/state/` | workspace index、instance manifest 和 README |

## 使用规则

1. 先用 `registries/documents.md` 根据目标 doc_id 找到模板。
2. 只读取当前输出需要的模板。
3. 不要默认读取整个 `templates/` 目录。
4. repair-run 需要结构迁移时，再读取对应旧文档的新模板。
