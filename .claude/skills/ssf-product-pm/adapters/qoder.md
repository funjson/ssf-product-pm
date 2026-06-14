# Qoder 适配说明

Qoder 规则文件位于：

`.qoder/rules/ssf-product-pm.md`

Qoder 可同时读取项目 `AGENTS.md`。平台规则应保持轻量，只要求 Agent 读取 skill 事实源。

执行时先读取 `SKILL.md`，再按其中的运行时读取路径加载 core、registries、当前 flow、当前 template 和必要 reference。

不要在 Qoder 规则里复制完整 workflow。关键不变量以 `SKILL.md` 为准：默认落盘、两个人工中断点、auto review 自动继续或 repair、prototype-run 只写 `prototype-input/`。
