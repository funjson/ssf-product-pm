# Claude Code 适配说明

Claude Code 项目级 skill 应包含完整目录：

- `SKILL.md`
- `core/`
- `flows/`
- `registries/`
- `references/`
- `templates/`

不要只复制入口文件。

Claude Code 执行时应遵守人工评审中断点，不得在 Analysis 或产品架构未确认时继续完整设计。

生成原型输入包时使用 `prototype-run`。该流程只输出实例内 `prototype-input/`，不修改 `product-spec/` 产品事实。
