# Codex 适配说明

Codex 使用：

- 根目录 `AGENTS.md` 作为项目规则。
- `SKILL.md` 作为 skill 入口。
- `core/`、`flows/`、`registries/`、`references/`、`templates/` 作为事实源。

安装或同步时必须复制完整 skill 目录，不得只复制 `SKILL.md`。

生成、修改、修复和 prototype-run 默认必须落盘；只有用户明确要求只读、只讨论或不修改文件时，才使用 `inspect-only` 或 `discuss-only`。

优先读取顺序：

1. `SKILL.md`
2. `core/workflow.md`
3. `core/runtime-protocol.md`
4. `registries/documents.md`
5. 对应 `flows/`
6. 对应模板

当用户要求输出原型输入包、Figma Make prompt 或 Figma MCP prompt 时，使用 `prototype-run`，读取 `flows/prototype/prototype-run.md` 和 `templates/prototype/`。
