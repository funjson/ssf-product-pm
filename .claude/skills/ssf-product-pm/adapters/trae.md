# Trae 适配说明

Trae 规则文件位于：

`.trae/rules/project_rules.md`

Trae 规则应只做路由，不复制完整 workflow，避免和主事实源漂移。

生成、修改、修复和 prototype-run 默认必须落盘；只有用户明确要求只读、只讨论或不修改文件时，才使用 `inspect-only` 或 `discuss-only`。

只在 `analysis-human-review` 和 `product-architecture-human-review` 中断；Analysis 01-03 完成后统一中断一次，产品架构中断一次，其他 auto_review 通过后自动继续。

当用户要求原型输入包或原型工具 prompt 时，路由到 `flows/prototype/prototype-run.md` 和 `templates/prototype/`。
