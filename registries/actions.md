# 动作注册表

| action | 适用语义 | flow | persistence_policy | 是否需要 intake |
|---|---|---|---|---|
| full-run | 完整生成、从头做一套 | `flows/analysis/flow.md` + `flows/design/flow.md` | write_required | yes |
| analysis-run | 先分析、调研、需求分析 | `flows/analysis/flow.md` | write_required | 视情况 |
| design-run | 生成产品设计 | `flows/design/flow.md` | write_required | 视情况 |
| flow-run | 只跑某个阶段 | 对应阶段 flow | write_required | 视情况 |
| doc-run | 单文档生成或修改 | 对应节点 flow | write_required | 高风险时 yes |
| change-run | 基于现有版本变更 | `flows/change/change-run.md` | write_required | yes |
| prototype-run | 基于当前产品规格生成原型输入包 | `flows/prototype/prototype-run.md` | write_required | 视情况 |
| repair-run | 修复结构、证据、状态 | `flows/repair/repair-run.md` | write_required | no |
| inspect-only | 只读取、检查、复述、审阅现有文件 | 无 | read_only | no |
| discuss-only | 只讨论、先讲方案、不落盘 | 无 | write_forbidden | no |

详细规则见 `references/action-commands.md`。
