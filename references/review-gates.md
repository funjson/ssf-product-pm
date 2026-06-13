# Review Gate 规则

> 本文件集中管理 `ssf-product-pm` 的评审能力。工作流只引用评审标识，不在每个文档里散写评审规则，方便后续调整评审方案。

## 1. 评审类型

| review_type | 含义 | 是否中断流程 | continue_on_pass | 处理方式 |
|---|---|---|---|---|
| human_review | 人机交互评审 | 是 | 否 | 必须停止继续生成，等待用户确认、修改或驳回 |
| auto_review | 自动自检查 | 否 | 是 | 模型根据检查项自检；通过则自动继续，失败时进入 repair-run |

## 2. 状态枚举

| 字段 | 可选值 |
|---|---|
| review_status | draft / ready_for_review / auto_checked / ready_for_review_delta / approved / approved_with_delta / rejected / needs_rework |
| review_result | pass / fail / pending |
| blocking_level | none / warning / blocking |
| evidence_id | APR-xxx / CHECK-xxx / 无 |

默认规则：

- `ready_for_review` 只表示 human_review 等待用户确认，不得用于要求用户逐个确认 auto_review 文档。
- Analysis 的 `analysis-human-review` 是阶段级 gate，覆盖 `01-analysis-input.md`、`02-research-insight.md` 和 `03-requirement-analysis.md`，只在 01-03 全部生成后中断一次。
- 产品架构的 `product-architecture-human-review` 是文档级 gate，只在 `04-product-architecture.md` 完成后中断一次。
- auto_review 文档生成后，若自检查通过，文档 `review_status = auto_checked`，gate `status = pass`，`blocked = no`，并自动继续下一节点。
- auto_review 文档自检查失败时，文档 `review_status = needs_rework`，gate `status = fail`，`blocked = yes`，下一步进入 `repair-run`。
- 只有用户明确确认并写入 `manifest.md` 的人工确认记录 `APR-xxx` 后，人工评审节点才可写 `approved`。
- 自动评审通过只能说明结构和一致性检查通过，不代表用户已确认。
- 自动评审失败时，必须把失败检查写入 `manifest.md` 的 Review Gate 状态和自动检查记录。
- 不得因为 auto_review 文档状态为 `auto_checked` 或存在待确认问题，就向用户逐文档索要确认；待确认问题进入文档和 manifest，流程仍按 gate 规则继续。

## 3. Gate 清单

| gate_id | 节点 | 类型 | gate_scope | must_stop | continue_on_pass | 失败处理 |
|---|---|---|---|---|---|---|
| analysis-human-review | 分析阶段评审 | human_review | stage:analysis，覆盖 01-03 | yes | no | 停止流程，列出缺失信息和建议补充项 |
| product-architecture-human-review | 产品架构评审 | human_review | document:04-product-architecture | yes | no | 停止流程，要求用户确认模块划分、边界和对象 |
| product-architecture-delta-review | 产品架构局部变更自检查 | auto_review | change:architecture-delta | no | yes | 如果改变模块边界，升级为 product-architecture-human-review |
| prd-auto-review | PRD 自检查 | auto_review | document:05-prd | no | yes | repair-run 修复目标、范围、角色、约束缺失 |
| feature-spec-auto-review | 功能任务自检查 | auto_review | document:06-feature-task-spec | no | yes | repair-run 补齐缺失 FEAT 小节和模块边界 |
| ui-ia-auto-review | UI 信息架构自检查 | auto_review | document:07-ui-ia-screen-inventory | no | yes | repair-run 补齐页面、导航、页面到功能映射 |
| ui-spec-auto-review | UI 规格自检查 | auto_review | document:08-structured-ui-interaction-spec | no | yes | repair-run 补齐 SCR 小节、组件和状态 |
| prototype-auto-review | 原型 Prompt 与标注自检查 | auto_review | document:09-prototype-prompt-ui-annotation | no | yes | repair-run 补齐 Prompt、标注和追踪关系 |
| baseline-auto-review | 基线与变更自检查 | auto_review | document:10-product-baseline-change | no | yes | repair-run 补齐变更前后、影响范围和回归关注点 |
| change-run-local-review | 局部变更自检查 | auto_review | change:local | no | yes | repair-run 修复受影响文档；若发现模块边界变化则升级人工评审 |
| prototype-input-auto-review | 原型输入包自检查 | auto_review | package:prototype-input | no | yes | repair-run 或补充输入包；未生成真实原型前原型结果检查保持 pending |

## 4. 人工评审输出格式

人工评审节点必须在文档末尾输出：

| 字段 | 内容 |
|---|---|
| review_gate | gate_id |
| review_type | human_review |
| review_status | ready_for_review / approved / rejected / needs_rework |
| must_stop | yes |
| user_decision_required | yes |
| approval_evidence | APR-xxx / 无 |
| suggested_decisions | 接受 / 修改 / 补充信息 / 重新生成 / 其他 |

阶段级人工评审规则：

- `analysis-human-review` 只能在 01-03 全部生成后触发一次，不能在每个 Analysis 文档后分别询问用户。
- `approved_scope` 必须覆盖 `01-analysis-input.md / 02-research-insight.md / 03-requirement-analysis.md`。

人工评审未获得用户明确确认时：

- 文档 `review_status` 必须保持 `ready_for_review`。
- `manifest.md` 中对应 gate 的 `blocked` 必须为 `yes`。
- `active_gate` 必须指向当前人工评审 gate。

人工评审获得用户明确确认时，必须同步更新 `manifest.md`：

| 字段 | 写入规则 |
|---|---|
| approval_id | 新增 `APR-xxx` |
| gate_id | `analysis-human-review` 或 `product-architecture-human-review` |
| user_words | 用户原话，不要改写成模型总结 |
| approved_scope | 用户确认的文档或阶段范围 |
| approval_result | approved / rejected / needs_rework |
| approved_at | 当前日期或时间 |

## 5. 自动评审输出格式

自动评审节点必须在文档末尾输出：

| 字段 | 内容 |
|---|---|
| review_gate | gate_id |
| review_type | auto_review |
| review_status | auto_checked / needs_rework |
| must_stop | no |
| user_decision_required | no |
| continue_on_pass | yes |

| check_id | 检查项 | 结果 | 问题 | 修复动作 |
|---|---|---|---|---|
| CHECK-PRD-001 / CHECK-FEAT-001 / CHECK-UIIA-001 / CHECK-UISPEC-001 / CHECK-PROT-001 / CHECK-BASE-001 / CHECK-PINPUT-001 / CHECK-RUNTIME-001 |  | pass / fail / pending |  | 无 / repair-run |

如果所有核心检查为 `pass`，本次节点不得停下来要求用户确认，必须自动继续下一节点。

如果任一核心检查为 `fail`，本次节点不得标记为完成，必须进入 `repair-run` 或把失败项写入 `manifest.md`。

### 5.1 自动检查 ID 命名

自动检查 ID 必须带来源前缀，避免正文 `CHECK-001` 与 manifest `CHECK-PRD-001` 不一致。

禁止在正文文档中继续使用裸编号 `CHECK-001`、`CHECK-002`。如果模板中没有合适检查项，先按当前 Review Gate 的前缀新增编号，并同步写入 `manifest.md`。

| 场景 | 命名 |
|---|---|
| PRD 自检查 | CHECK-PRD-001 |
| 功能任务自检查 | CHECK-FEAT-001 |
| UI 信息架构自检查 | CHECK-UIIA-001 |
| 结构化 UI 自检查 | CHECK-UISPEC-001 |
| 原型标注自检查 | CHECK-PROT-001 |
| 基线自检查 | CHECK-BASE-001 |
| 产品架构局部变更自检查 | CHECK-ARCH-DELTA-001 |
| 某次变更自检查 | CHECK-CHG-xxx-001 |
| 原型输入包自检查 | CHECK-PINPUT-001 |
| 真实原型生成后检查 | CHECK-PROTOTYPE-001 |
| 运行时持久化检查 | CHECK-RUNTIME-001 |

正文文档和 `manifest.md` 必须使用同一组检查 ID。

## 6. 产品架构 Delta 规则

当变更修改了 `04-product-architecture.md`，但没有新增/删除/合并/拆分模块，也没有改变模块职责边界时：

- 执行 `product-architecture-delta-review`。
- 在产品架构文档写入 `ARCH-DELTA-xxx`。
- 文档状态可以写 `approved_with_delta` 或 `ready_for_review_delta`。
- `manifest.md` 必须说明本次 delta 未改变模块边界。
- 不需要中断到 `product-architecture-human-review`。

当变更改变模块边界时：

- 不得使用 `approved_with_delta`。
- 必须进入 `product-architecture-human-review`。
- `blocked = yes`，`next_allowed_actions = wait-user-review`。

## 7. prototype-input-auto-review 规则

`prototype-input-auto-review` 只检查输入包是否适合原型工具消费。

允许写 `pass` 的对象：

- `prototype-input/` 文件结构是否完整。
- 页面、组件、流程、样例数据、ID 约束是否完整。
- Prompt 是否禁止新增规格外内容。

必须保持 `pending` 的对象：

- 真实 Figma / Motiff / Uizard 原型是否已经生成。
- 真实原型 Frame 是否完整。
- 真实原型 layer 是否保留 `CMP`。
- 真实原型可点击流程是否可用。

没有真实原型证据时，不得把 `CHECK-PROTOTYPE-xxx` 写成 `pass`。

## 8. Manifest 写入要求

每次执行 Review Gate 后，必须同步更新目标实例 `manifest.md`：

- `current_phase`
- `active_gate`
- `blocked`
- `current_blocker`
- `next_allowed_actions`
- `Review Gate 状态`
- `人工确认记录` 或 `自动检查记录`

不得只在正文文档末尾写 Review Gate，而不更新 `manifest.md`。
