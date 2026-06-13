# 06 UI 标注交付

> 本文档面向前端 AI、测试 AI 和设计交付。它把关键组件与功能、规则、验收、测试断言连接起来。

## 0. 文档元信息

| 字段 | 内容 |
|---|---|
| document_id | PROTO-ANNOTATION-HANDOFF-001 |
| instance_id | SPI-xxx |
| version | v0.1 |
| base_ui_spec | UI-SPEC-001 |
| base_prototype_annotation | PROTOTYPE-ANNOTATION-001 |
| generated_at |  |
| review_gate | prototype-input-auto-review |
| review_status | draft / ready_for_review / needs_rework |

## 1. 标注覆盖规则

| 组件类型 | 是否必须标注 | 说明 |
|---|---|---|
| 页面主入口 | yes | 影响导航或核心任务 |
| 可点击组件 | yes | 影响交互和测试 |
| 表单组件 | yes | 影响校验和错误状态 |
| 数据绑定组件 | yes | 影响实现理解 |
| 规则约束组件 | yes | 关联 BR / AC |
| 状态变化组件 | yes | 关联 loading / empty / error / permission |
| 纯展示组件 | optional | 只在影响理解时标注 |

## 2. 标注总表

| annotation_id | screen_id | component_id | layer_name | feature_id | rule_id | ac_id | implementation_note | test_assertion |
|---|---|---|---|---|---|---|---|---|
| PANN-001 | SCR-xxx | CMP-xxx | CMP-xxx 组件用途 | FEAT-xxx | BR-xxx | AC-xxx |  | UIA-xxx |

## 3. 缺失标注清单

| component_id | screen_id | 缺失原因 | 建议补充 |
|---|---|---|---|
| CMP-xxx | SCR-xxx |  |  |

## 4. 前端 AI 使用说明

- 以 `product-spec/08-structured-ui-interaction-spec.md` 为页面事实源。
- 以本文件理解 Figma layer 与业务规则的关系。
- 不从视觉稿反推出新业务规则。
- 发现原型与规格冲突时，以 `product-spec/` 为准，并提交待确认问题。
