# 05 Figma Make / 原型工具 Prompt

> 本文档把原型输入包重组为可直接投喂 prompt-to-prototype 工具的提示词。它优先服务 Figma Make，也可适配 Motiff / Uizard / UX Pilot。

## 0. 文档元信息

| 字段 | 内容 |
|---|---|
| document_id | PROTO-FIGMA-MAKE-PROMPTS-001 |
| instance_id | SPI-xxx |
| version | v0.1 |
| base_master_brief | PROTO-MASTER-BRIEF-001 |
| base_screen_contracts | PROTO-SCREEN-CONTRACTS-001 |
| base_flow_contracts | PROTO-FLOW-CONTRACTS-001 |
| base_sample_data | PROTO-SAMPLE-DATA-001 |
| generated_at |  |
| review_gate | prototype-input-auto-review |
| review_status | draft / ready_for_review / needs_rework |

## 1. 第一段：总控 Prompt

```text
你是资深产品设计师。请基于以下约束生成可点击原型。

产品名称：<product_name>
原型类型：<prototype_type>
端类型：<device_type>

必须生成以下主 Frame：
- <SCR-xxx screen_name>

命名规则：
- 主 Frame 使用 "SCR-xxx screen_name"。
- 关键图层使用 "CMP-xxx component purpose"。
- 不要把 SCR / CMP / FEAT / BR / AC 显示成用户可见文案。

禁止：
- 不新增未定义页面。
- 不新增未定义功能。
- 不新增未定义业务流程。
- 不加入广告、营销页、社交评论或无关模块。
```

## 2. 第二段：页面与流程合同 Prompt

```text
请按以下页面合同生成：

<粘贴 02-screen-contracts 的页面总表和目标页面合同>

请按以下流程连接可点击原型：

<粘贴 03-flow-contracts 的核心流程>
```

## 3. 第三段：逐页修正 Prompt 模板

```text
请修正页面 <SCR-xxx screen_name>。

保留：
- 当前 screen_id。
- 当前 component_id。
- 当前主流程。

需要修正：
- <问题>

不得改变：
- 不新增规格外页面。
- 不新增规格外按钮。
- 不改变 FEAT / BR / AC 含义。
```

## 4. Figma MCP 执行 Prompt

```text
使用 Figma MCP 创建原生 Figma 原型。

读取本 prototype-input 包。

创建主 Frame：
- <SCR-xxx screen_name>

规则：
1. 使用 screen_id 命名 Frame。
2. 使用 component_id 命名关键 layer。
3. 不把 ID 显示为用户文案。
4. 使用一致的 spacing、typography、cards、tags、buttons。
5. 为核心流程创建 prototype connections。
6. 为关键组件添加 annotation，包含 feature_id、rule_id、ac_id、implementation note、test assertion。

完成后执行一致性检查，不要提前写 pass。
```
