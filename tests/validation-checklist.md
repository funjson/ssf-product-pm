# 验证清单

## 1. 目录检查

- 是否存在 `core/`。
- 是否存在 `flows/`。
- 是否存在 `registries/`。
- 是否存在 `templates/common`、`templates/analysis`、`templates/design`、`templates/state`。
- 是否存在 `adapters/`。
- 是否存在 `tests/`。

## 2. 运行检查

- `SKILL.md` 是否指向新架构。
- 每个动作是否能找到对应 flow。
- 每个文档是否能从 `registries/documents.md` 找到模板和 gate。
- 每个 repair-run 是否执行 `CHECK-REPAIR`。

## 3. 漂移检查

- 平台规则是否引用 `core/flows/registries/references/templates`。
- `.agents` 和 `.claude` 是否与主事实源同步。
- `.cursor/.qoder/.trae` 是否只做路由。
