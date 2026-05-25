# 动作注册表

| action | 适用语义 | flow | 是否落盘 | 是否需要 intake |
|---|---|---|---|---|
| full-run | 完整生成、从头做一套 | `flows/analysis/flow.md` + `flows/design/flow.md` | yes | yes |
| analysis-run | 先分析、调研、需求分析 | `flows/analysis/flow.md` | yes | 视情况 |
| design-run | 生成产品设计 | `flows/design/flow.md` | yes | 视情况 |
| doc-run | 单文档生成或修改 | 对应节点 flow | yes | 高风险时 yes |
| change-run | 基于现有版本变更 | `flows/change/change-run.md` | yes | yes |
| repair-run | 修复结构、证据、状态 | `flows/repair/repair-run.md` | yes | no |
| discuss-only | 只讨论 | 无 | no | no |

详细规则见 `references/action-commands.md`。
