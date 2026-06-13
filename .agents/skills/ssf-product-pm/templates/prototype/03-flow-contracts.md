# 03 流程合同

> 本文档定义可点击原型必须保留的页面流转和关键交互。流程只能来自 UI IA、功能任务规格或原型标注文档。

## 0. 文档元信息

| 字段 | 内容 |
|---|---|
| document_id | PROTO-FLOW-CONTRACTS-001 |
| instance_id | SPI-xxx |
| version | v0.1 |
| base_ui_ia | UI-IA-001 |
| base_feature_spec | FEATURE-SPEC-001 |
| base_prototype_annotation | PROTOTYPE-ANNOTATION-001 |
| generated_at |  |
| review_gate | prototype-input-auto-review |
| review_status | draft / ready_for_review / needs_rework |

## 1. 流程总表

| flow_id | 流程名称 | 起点 | 终点 | 关联功能 | 优先级 |
|---|---|---|---|---|---|
| PFLOW-001 |  | SCR-xxx | SCR-xxx | FEAT-xxx | high / medium / low |

## 2. 流程合同模板

# PFLOW-xxx 流程名称

## 2.1 页面顺序

```text
SCR-001 -> SCR-002 -> SCR-003
```

## 2.2 关键交互

| step | source_screen | component_id | 用户动作 | target_screen / state | 关联功能 |
|---|---|---|---|---|---|
| 1 | SCR-xxx | CMP-xxx |  | SCR-xxx / STATE-xxx | FEAT-xxx |

## 2.3 异常路径

| condition | 表现 | 恢复路径 | 关联验收 |
|---|---|---|---|
|  |  |  | AC-xxx |

## 2.4 原型工具提示

```text
请连接以下页面流转：
<页面顺序>

关键点击：
- <source_screen> 的 <component_id> 点击后进入 <target_screen>
```
