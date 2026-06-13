# 02 页面合同

> 本文档把 UI IA 和结构化 UI 规格重组为原型工具可执行的页面合同。每个 `SCR` 必须保留完整结构。

## 0. 文档元信息

| 字段 | 内容 |
|---|---|
| document_id | PROTO-SCREEN-CONTRACTS-001 |
| instance_id | SPI-xxx |
| version | v0.1 |
| base_ui_ia | UI-IA-001 |
| base_ui_spec | UI-SPEC-001 |
| generated_at |  |
| review_gate | prototype-input-auto-review |
| review_status | draft / auto_checked / needs_rework |

## 1. 页面总表

| screen_id | frame_name | 页面名称 | 页面目标 | 关联模块 | 关联功能 | 状态覆盖 |
|---|---|---|---|---|---|---|
| SCR-001 | SCR-001 页面名称 |  |  | MOD-xxx | FEAT-xxx | 默认 / 加载 / 空态 / 错误 / 无权限 |

---

## 2. 页面合同模板

# SCR-xxx 页面名称

## 2.1 页面元信息

| 字段 | 内容 |
|---|---|
| screen_id | SCR-xxx |
| frame_name | SCR-xxx 页面名称 |
| screen_goal |  |
| target_roles | ROLE-xxx |
| related_features | FEAT-xxx |
| related_modules | MOD-xxx |

## 2.2 必须出现的区域

| region_id | 区域名称 | 目标 | 包含组件 |
|---|---|---|---|
| REG-001 |  |  | CMP-xxx |

## 2.3 关键组件合同

| component_id | layer_name | 组件类型 | 用户可见文案 | 业务目标 | 关联规则 | 关联验收 | 是否必须标注 |
|---|---|---|---|---|---|---|---|
| CMP-001 | CMP-001 组件用途 |  |  |  | BR-xxx | AC-xxx | yes / no |

## 2.4 状态合同

| state_id | 状态类型 | 触发条件 | 原型表现 | 必须可见 |
|---|---|---|---|---|
| STATE-001 | 默认 / 加载 / 空态 / 错误 / 禁用 / 无权限 |  |  | yes / no |

## 2.5 负向约束

| 禁止项 | 原因 |
|---|---|
|  |  |
