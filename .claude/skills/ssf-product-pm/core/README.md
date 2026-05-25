# core 目录说明

`core/` 存放 skill 的稳定运行协议。这里不写具体文档模板，也不写某个阶段的详细产出格式。

本目录回答：

- 工作流整体如何推进。
- 运行时如何判断实例、动作、跳阶段和续跑。
- `index.md`、`manifest.md`、baseline 等状态资产如何治理。
- Review Gate、ID、repair-run 这些跨阶段规则如何生效。

Agent 执行时应先读 `SKILL.md`，再按需读取本目录中的协议文件。

不放入本目录：

- 具体文档模板，放到 `templates/`。
- 每个阶段的小阶段规则，放到 `flows/`。
- 平台适配说明，放到 `adapters/`。
