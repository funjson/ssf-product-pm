# Cursor 适配说明

Cursor 规则文件位于：

`.cursor/rules/ssf-product-pm.mdc`

该文件只负责触发和路由，具体规则从 skill 事实源读取。

Cursor 执行时先读取 `SKILL.md`，再按其中的运行时读取路径加载：

- 必要的 `core/`
- 必要的 `registries/`
- 当前 action/document 对应的 `flows/`
- 当前输出对应的 `templates/`
- 当前 gate 或修复任务需要的 `references/`

不要在 Cursor 规则里复制完整 workflow。关键不变量以 `SKILL.md` 为准。
