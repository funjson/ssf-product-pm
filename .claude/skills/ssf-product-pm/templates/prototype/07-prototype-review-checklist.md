# 07 原型输入包与原型验收清单

> 本文档用于检查 prototype-input 是否可用，以及真实原型生成后是否与产品规格一致。

## 0. 文档元信息

| 字段 | 内容 |
|---|---|
| document_id | PROTO-REVIEW-CHECKLIST-001 |
| instance_id | SPI-xxx |
| version | v0.1 |
| generated_at |  |
| review_gate | prototype-input-auto-review |
| review_status | draft / auto_checked / needs_rework |

## 1. 输入包自检查

| check_id | 检查项 | 通过标准 | 结果 | 问题 | 修复动作 |
|---|---|---|---|---|---|
| CHECK-PINPUT-001 | 页面完整性 | 所有 UI IA 中的 SCR 都进入 screen contracts | pass / fail / pending |  | repair-run / 补齐 |
| CHECK-PINPUT-002 | 组件追踪 | 关键可交互组件都有 CMP 并进入 handoff | pass / fail / pending |  | repair-run / 补齐 |
| CHECK-PINPUT-003 | 流程完整性 | 主要导航和点击流进入 flow contracts | pass / fail / pending |  | repair-run / 补齐 |
| CHECK-PINPUT-004 | 样例数据 | 核心页面有样例数据，且标记为 prototype-only | pass / fail / pending |  | 补充样例 |
| CHECK-PINPUT-005 | ID 使用 | SCR/CMP 用于 frame/layer/annotation，不作为 UI 文案 | pass / fail / pending |  | 修正 prompt |
| CHECK-PINPUT-006 | 禁止扩展 | Prompt 明确禁止新增规格外页面、功能和流程 | pass / fail / pending |  | 修正 prompt |

## 2. 真实原型生成后检查

> 未生成真实原型前，本节必须保持 `pending`，不得提前写 pass。

| check_id | 检查项 | 通过标准 | 结果 | 问题 | 修复 Prompt |
|---|---|---|---|---|---|
| CHECK-PROTOTYPE-001 | Frame 完整 | 每个 SCR 有对应主 Frame | pending / pass / fail |  |  |
| CHECK-PROTOTYPE-002 | 图层命名 | 关键组件图层保留 CMP | pending / pass / fail |  |  |
| CHECK-PROTOTYPE-003 | 无规格外内容 | 未新增无关页面、按钮、业务流程 | pending / pass / fail |  |  |
| CHECK-PROTOTYPE-004 | 状态覆盖 | 默认、加载、空态、错误、禁用、无权限按规格呈现 | pending / pass / fail |  |  |
| CHECK-PROTOTYPE-005 | 业务规则表达 | BR / AC 相关组件表现正确 | pending / pass / fail |  |  |
| CHECK-PROTOTYPE-006 | 可点击流程 | 核心 PFLOW 可点击通过 | pending / pass / fail |  |  |

## 3. 待确认问题

| question_id | 问题 | 影响范围 | 建议处理 |
|---|---|---|---|
| Q-PINPUT-001 |  |  |  |
