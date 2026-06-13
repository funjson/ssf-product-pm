# Trae 适配说明

Trae 规则文件位于：

`.trae/rules/project_rules.md`

Trae 规则应只做路由，不复制完整 workflow，避免和主事实源漂移。

当用户要求原型输入包或原型工具 prompt 时，路由到 `flows/prototype/prototype-run.md` 和 `templates/prototype/`。
