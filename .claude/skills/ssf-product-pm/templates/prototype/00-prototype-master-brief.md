# 00 原型生成总控说明

> 本文档是原型工具的总控输入，压缩产品背景、页面范围、ID 保留策略、禁止事项和输出要求。它不替代 PRD，也不新增产品事实。

## 0. 文档元信息

| 字段 | 内容 |
|---|---|
| document_id | PROTO-MASTER-BRIEF-001 |
| instance_id | SPI-xxx |
| version | v0.1 |
| base_prd | PRD-001 |
| base_ui_ia | UI-IA-001 |
| base_ui_spec | UI-SPEC-001 |
| base_prototype_annotation | PROTOTYPE-ANNOTATION-001 |
| generated_at |  |
| review_gate | prototype-input-auto-review |
| review_status | draft / ready_for_review / needs_rework |

## 1. 产品压缩背景

| 项目 | 内容 |
|---|---|
| 产品名称 |  |
| 产品一句话定位 |  |
| 目标用户 |  |
| 核心价值 |  |
| 本次原型目标 |  |
| 不覆盖内容 |  |

## 2. 原型范围

| scope_id | 范围项 | 来源 | 说明 |
|---|---|---|---|
| PSCOPE-001 |  | PRD-001 / UI-IA-001 |  |

## 3. 必须生成的页面

| screen_id | frame_name | 页面名称 | 页面目标 | 关联功能 |
|---|---|---|---|---|
| SCR-001 | SCR-001 页面名称 |  |  | FEAT-xxx |

## 4. 必须保留的流程

| flow_id | 流程名称 | 页面顺序 | 关键交互 | 关联功能 |
|---|---|---|---|---|
| PFLOW-001 |  | SCR-xxx -> SCR-xxx | CMP-xxx | FEAT-xxx |

## 5. ID 保留策略

| ID 类型 | 保留位置 | 用户可见性 |
|---|---|---|
| SCR | Frame 名称 / 页面标注 | 不作为 UI 文案显示 |
| CMP | 关键 layer 名称 / 组件名 / annotation | 不作为 UI 文案显示 |
| FEAT | annotation / handoff table | 不作为 UI 文案显示 |
| BR | annotation / test note | 不作为 UI 文案显示 |
| AC | annotation / test note | 不作为 UI 文案显示 |

## 6. 原型工具禁止事项

| 禁止项 | 原因 | 来源 |
|---|---|---|
| 不新增规格外页面 | 防止原型漂移 | UI-IA-001 |
| 不新增规格外按钮或业务流程 | 防止实现和测试误解 | UI-SPEC-001 |
| 不把 ID 展示给终端用户 | ID 是交付标注，不是产品文案 | prototype-run |

## 7. 总控 Prompt

```text
请基于本输入包生成原型。

产品：<产品名称>
原型类型：<低保真 / 高保真 / 可点击原型>
端类型：<移动端 / Web / 小程序 / 桌面端>

必须生成页面：
- <SCR-xxx 页面名称>

必须保留流程：
- <PFLOW-xxx>

Frame 和 layer 命名：
- 主 Frame 必须使用 screen_id + screen_name 命名。
- 关键组件 layer 必须使用 component_id + component_purpose 命名。
- 不得把 SCR / CMP / FEAT / BR / AC 显示为用户可见文案。

不得新增：
- 未在 screen contracts 中定义的页面。
- 未在 component contracts 中定义的核心按钮。
- 未在 flow contracts 中定义的业务流程。
```
