# 验证清单

## 1. 目录检查

- 是否存在 `core/`。
- 是否存在 `flows/`。
- 是否存在 `registries/`。
- 是否存在 `templates/common`、`templates/analysis`、`templates/design`、`templates/state`。
- 是否存在 `templates/prototype`。
- 是否存在 `flows/prototype`。
- 是否存在 `adapters/`。
- 是否存在 `tests/`。

## 2. 运行检查

- `SKILL.md` 是否指向新架构。
- 每个动作是否能找到对应 flow。
- `registries/actions.md` 是否为每个 action 标明 `persistence_policy`。
- 生成类 action 是否为 `write_required`，且 `discuss-only` 不能由“用户没说落盘”触发。
- 是否存在 `inspect-only` 只读执行模式，避免检查/复述类请求误写文件。
- `registries/gates.md` 是否为每个 gate 标明 `gate_scope`、`must_stop` 和 `continue_on_pass`。
- `analysis-human-review` 是否是阶段级 gate，只在 01-03 全部完成后中断一次。
- 产品架构之后的 auto_review 是否通过后自动继续，不逐文件请求用户确认。
- 每个文档是否能从 `registries/documents.md` 找到模板和 gate。
- 每个 repair-run 是否执行 `CHECK-REPAIR`。
- prototype-run 是否能找到 `flows/prototype/prototype-run.md` 和 `templates/prototype/00-07`。
- prototype-run 是否执行 `CHECK-PINPUT`，并让未生成真实原型的 `CHECK-PROTOTYPE` 保持 pending。

## 3. 漂移检查

- 平台规则是否引用 `core/flows/registries/references/templates`。
- `.agents` 和 `.claude` 是否与主事实源同步。
- `.cursor/.qoder/.trae` 是否只做路由。
