# Qoder 适配说明

Qoder 规则文件位于：

`.qoder/rules/ssf-product-pm.md`

Qoder 可同时读取项目 `AGENTS.md`。建议让平台规则保持轻量，只要求 Agent 读取 skill 事实源。

生成、修改、修复和 prototype-run 默认必须落盘；只有用户明确要求只读、只讨论或不修改文件时，才使用 `inspect-only` 或 `discuss-only`。

prototype-run 只派生 `prototype-input/`，不得把样例数据或原型结果回写为产品事实。
