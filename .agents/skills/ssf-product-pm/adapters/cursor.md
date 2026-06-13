# Cursor 适配说明

Cursor 规则文件位于：

`.cursor/rules/ssf-product-pm.mdc`

该文件只负责触发和路由，具体规则从 skill 事实源读取。

生成、修改、修复和 prototype-run 默认必须落盘；只有用户明确要求只读、只讨论或不修改文件时，才使用 `inspect-only` 或 `discuss-only`。

只在 `analysis-human-review` 和 `product-architecture-human-review` 中断；Analysis 01-03 完成后统一中断一次，产品架构中断一次，其他 auto_review 通过后自动继续。

Cursor 规则应引用：

- `SKILL.md`
- `core/`
- `flows/`
- `registries/`
- `references/`
- `templates/`

用户要求 prototype / Figma Make / 原型输入包时，应额外读取：

- `flows/prototype/prototype-run.md`
- `templates/prototype/`
