# Codex 适配说明

Codex 使用根目录 `AGENTS.md` 作为项目规则，使用 `SKILL.md` 作为 Skill 入口。

安装或同步时必须复制完整 skill 目录，不得只复制入口文件：

- `SKILL.md`
- `AGENTS.md`
- `core/`
- `flows/`
- `registries/`
- `references/`
- `templates/`

执行时按 `SKILL.md` 的运行时读取路径加载配置：

1. 先读 core runtime、state 和 actions/documents/gates registry。
2. 再按当前 action、document、gate 读取对应 flow、template 和必要 reference。
3. 不要默认读取全部 references 或全部 templates。

关键不变量以 `SKILL.md` 为准：生成/修改/修复/prototype-run 默认落盘；只有 `analysis-human-review` 和 `product-architecture-human-review` 能中断；prototype-run 只写入目标实例 `prototype-input/`。
