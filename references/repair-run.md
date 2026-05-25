# repair-run 修复运行规则

> repair-run 不是“顺手补一补”，而是对流程资产和文档结构做一致性修复。只要存在下列结构问题，即使正文内容看起来正确，也必须判定本次 repair-run 未完成。

## 1. repair-run 目标

repair-run 只修复结构、追踪、状态、证据和模板一致性，默认不改变产品事实。

允许修复：

- `index.md` 和 `manifest.md` 的状态、字段、Review Gate、证据记录。
- 正文文档中缺失的小节、表头、检查 ID、版本字段。
- 变更记录、架构 Delta、自动检查记录之间的不一致。
- 已有内容的结构迁移，例如把旧版短表迁移为新版完整表。

禁止修复：

- 未经用户确认改写产品定位、需求、模块边界、业务规则。
- 借 repair-run 新增无关需求、页面、功能或技术方案。
- 用“摘要说明已修复”替代实际改正文档结构。

## 2. 必读文件

执行 repair-run 前必须读取：

1. `references/workflow.md`
2. `references/action-commands.md`
3. `references/template-index.md`
4. `references/review-gates.md`
5. `references/id-conventions.md`
6. `references/quality-checklist.md`
7. `references/repair-run.md`
8. 目标工作区 `ssf-workspace/index.md`
9. 目标实例 `manifest.md`

如果 repair-run 涉及某个正文文档，还必须读取对应 `templates/` 模板。

## 3. 结构迁移优先级

repair-run 必须按以下顺序修复，不得只修复后面的正文细节而跳过前面的流程资产。

| 顺序 | 修复对象 | 必须满足 |
|---|---|---|
| 1 | `ssf-workspace/index.md` | 使用 `templates/state/workspace-index.md` 的完整实例列表表头 |
| 2 | `manifest.md` | active_gate、blocked、next_allowed_actions、Review Gate 状态、人工/自动证据一致 |
| 3 | 被影响正文文档 | 文档元信息、结构小节、Review Gate、检查 ID 与模板一致 |
| 4 | `10-product-baseline-change.md` | current_version、previous_version、版本历史、CHG 记录一致 |
| 5 | 交叉追踪 | ARCH-DELTA、CHECK、CHG、FEAT、SCR、AC 在各文档中能互相定位 |

## 4. Workspace Index 硬规则

`index.md` 是实例调度依据，不能自由发挥格式。

必须使用以下实例列表表头：

```markdown
| instance_id | 实例名称 | 产品 / 项目名称 | 任务类型 | 当前阶段 | 当前状态 | 阻塞 Review Gate | 最近运行模式 | 下一步建议动作 | 最近更新时间 | 摘要 | 路径 |
```

禁止使用旧版短表：

```markdown
| instance_id | 产品名称 | 产品形态 | 业务领域 | 当前状态 | 最近更新时间 | 摘要 | 实例路径 |
```

`index_version` 是模板结构版本，不是每次生成的流水号。除非模板文件本身升级，否则不得把 `v0.4` 自行改成 `v0.8`、`v0.9` 等任意版本。

如果 repair-run 后 `index.md` 仍使用旧版短表，本次 repair-run 必须判定为 fail。

## 5. Baseline 硬规则

`10-product-baseline-change.md` 必须使用当前模板结构。

文档元信息必须包含：

- `current_version`
- `previous_version`
- `related_documents`
- `review_gate`
- `review_status`

必须包含 `## 2. 版本历史`，并记录至少：

| version | change_id | change_type | 摘要 | 状态 |
|---|---|---|---|---|
| v0.1 | CHG-001 | 新增 | 初始产品基线 | ready_for_review / approved |

每次 `change-run` 后：

- `current_version` 必须等于最新 `target_version`。
- `previous_version` 必须等于本次变更前版本。
- `版本历史` 必须追加对应 `CHG-xxx`。
- CHG 小节编号必须与模板一致，不得出现 `## 9` 下继续写 `## 8.1` 的错位编号。

如果 `current_version = v0.2` 但缺少 `previous_version` 或版本历史，本次 repair-run 必须判定为 fail。

## 6. 检查 ID 硬规则

正文文档和 `manifest.md` 必须使用同一组检查 ID。

禁止正文文档出现：

```text
CHECK-001
CHECK-002
CHECK-003
```

必须使用：

```text
CHECK-PRD-001
CHECK-FEAT-001
CHECK-UIIA-001
CHECK-UISPEC-001
CHECK-PROT-001
CHECK-BASE-001
CHECK-ARCH-DELTA-001
CHECK-CHG-002-001
```

如果正文和 manifest ID 不一致，本次 repair-run 必须判定为 fail。

## 7. 完成判定

repair-run 结束前必须自查：

| check_id | 检查项 | 通过标准 |
|---|---|---|
| CHECK-REPAIR-001 | index 结构 | 实例列表使用完整表头，没有旧版短表 |
| CHECK-REPAIR-002 | manifest 证据 | Review Gate 状态和人工/自动证据一致 |
| CHECK-REPAIR-003 | baseline 版本 | 有 current_version、previous_version、版本历史 |
| CHECK-REPAIR-004 | 检查 ID | 正文和 manifest 使用同一组带前缀 CHECK ID |
| CHECK-REPAIR-005 | 不改产品事实 | 未借 repair-run 修改需求、模块边界或业务规则 |

以上任一项失败，不能把 repair-run 写成 complete。
