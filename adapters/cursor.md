# Cursor 适配说明

Cursor 规则文件位于：

`.cursor/rules/ssf-product-pm.mdc`

该文件只负责触发和路由，具体规则从 skill 事实源读取。

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
