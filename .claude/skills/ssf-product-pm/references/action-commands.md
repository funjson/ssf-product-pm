# 动作指令规则

> 本文件集中管理用户自然语言指令到执行模式的映射。`SKILL.md` 只负责要求模型读取本文件，不把所有动作判断写死在入口里。

## 1. 执行模式

| execution_mode | 触发语义 | 处理方式 |
|---|---|---|
| full-run | 完整生成、从头做一套、生成完整产品设计 | 先执行 intake，再执行 Analysis，人工评审通过后进入 Design |
| analysis-run | 先分析、做调研、收集信息、需求分析 | 只执行 Analysis；结束于 `analysis-human-review` |
| design-run | 做设计、生成 PRD/产品架构/功能/UI | 验证 Analysis 是否存在且通过；缺失则中断或基于假设标记风险 |
| flow-run | 只跑某个阶段 | 检查该阶段依赖，允许跳阶段但必须标记缺失输入 |
| doc-run | 只生成或修改某个文档 | 检查目标实例和上游依赖，只更新相关文档与 manifest |
| change-run | 基于已有版本修改、迭代、追加需求 | 读取基线与产品架构，判断影响范围后局部更新 |
| repair-run | 补齐、修复、重新检查、格式不完整 | 不改变产品事实，按 `references/repair-run.md` 修复结构、追踪、状态、证据和模板一致性 |
| discuss-only | 只讨论、不落盘 | 不写文件，可给流程建议 |

## 2. 高风险指令

遇到以下语义必须执行 intake gate，并记录写入策略：

- 重新生成 / 重做 / 再来一版 / 全部重跑
- 覆盖 / 删除旧的 / 重新开始
- 基于之前改 / 继续上次 / 补齐上次
- 直接生成某个后续阶段
- 用户输入明显像另一个产品或另一个事项

## 3. 跳阶段规则

跳阶段不是禁止项，但必须满足：

1. 读取 `ssf-workspace/index.md` 和目标实例 `manifest.md`。
2. 明确目标阶段所需上游输入。
3. 标记已有输入、缺失输入和模型假设。
4. 若跳过人工评审节点，不得把后续文档标记为 `approved`。
5. 若跳到设计阶段，必须先验证产品架构是否存在；不存在时先生成或更新产品架构。

## 4. 变更局部执行规则

功能迭代、小调整、局部 UI 修改不应全量重跑。默认流程：

```text
读取 index 与 manifest
  ↓
读取当前基线和产品架构
  ↓
判断影响范围：Analysis / Product Architecture / PRD / FEAT / UI / Baseline
  ↓
只更新受影响文档
  ↓
执行对应 review gate
  ↓
更新 manifest 与 baseline change
```

### 4.1 产品架构影响判断

变更影响产品架构时，不是一律重新人工评审，必须先判断影响层级：

| 影响类型 | 示例 | 处理方式 |
|---|---|---|
| 模块边界变化 | 新增/删除/合并/拆分 MOD，改变模块职责或上下游边界 | 必须进入 `product-architecture-human-review`，中断等待用户确认 |
| 架构局部补充 | 在既有 MOD 内补充 OBJ 属性、规则描述、决策记录，不改变模块边界 | 执行 `product-architecture-delta-review`，记录 `ARCH-DELTA-xxx`，不复用旧 APR 解释新增内容 |
| 功能内规则变化 | 只影响 FEAT/BR/AC，不影响 CAP/MOD/OBJ | 执行 `change-run-local-review`，不更新产品架构 |
| UI 表达变化 | 只影响 SCR/CMP/ANN | 执行对应 UI auto review，不更新产品架构 |

产品架构文档发生任何内容变更时，必须满足：

1. 在 `04-product-architecture.md` 写入 `ARCH-DELTA-xxx`。
2. 在 `manifest.md` 写入 `product-architecture-delta-review` 或 `product-architecture-human-review`。
3. 在 `10-product-baseline-change.md` 的变更影响范围中说明是否改变模块边界。
4. 不得只沿用旧 `APR-xxx`，让新架构内容看起来像旧人工确认的一部分。

## 5. repair-run 硬规则

repair-run 不是局部润色，而是结构一致性修复。执行 repair-run 时必须读取 `references/repair-run.md`。

必须优先修复：

1. `ssf-workspace/index.md` 是否使用新版完整实例列表表头。
2. `manifest.md` 是否记录 Review Gate、blocked、next_allowed_actions 和证据。
3. `10-product-baseline-change.md` 是否有 `previous_version` 和版本历史。
4. 正文文档检查 ID 是否与 manifest 一致，且没有裸 `CHECK-001`。
5. ARCH-DELTA、CHG、CHECK、FEAT、SCR、AC 是否能互相追踪。

如果这些硬规则没有通过，不得把 repair-run 写成 complete。
