# Claude Code 适配说明

Claude Code 项目级 skill 应包含完整目录：

- `SKILL.md`
- `AGENTS.md`
- `core/`
- `flows/`
- `registries/`
- `references/`
- `templates/`

不要只复制入口文件。

Claude Code 执行时只做路由，不复制完整 workflow。先读取 `SKILL.md`，再按其中的运行时读取路径加载 core、registries、当前 flow、当前 template 和必要 reference。

关键不变量以 `SKILL.md` 为准：生成/修改/修复/prototype-run 默认落盘；只有 `analysis-human-review` 和 `product-architecture-human-review` 能中断；prototype-run 只写入目标实例 `prototype-input/`，不修改 `product-spec/`。
