# Trae 适配说明

Trae 规则文件位于：

`.trae/rules/project_rules.md`

Trae 规则应只做触发和路由，不复制完整 workflow，避免和主事实源漂移。

执行时先读取 `SKILL.md`，再按其中的运行时读取路径加载 core、registries、当前 flow、当前 template 和必要 reference。

关键不变量以 `SKILL.md` 为准：生成/修改/修复/prototype-run 默认落盘；只有两个人工中断点；auto review 通过后自动继续，失败进入 repair-run；prototype-run 不修改 `product-spec/`。
