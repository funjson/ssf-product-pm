# 工作流总协议

## 1. 总体模型

`ssf-product-pm` 的运行模型是：

```text
用户请求
  ↓
动作识别
  ↓
实例判断
  ↓
工作流推进
  ↓
节点执行
  ↓
Review Gate
  ↓
状态回写
```

核心分层：

```text
workflow 编排 flow
flow 定义节点规则
template 定义输出结构
gate 定义评审方式
check 定义自检项
state 记录运行事实
```

## 2. 主流程

默认主流程：

```text
Intake
  ↓
Analysis
  ↓ analysis-human-review，必须中断
Design
  ↓ product-architecture-human-review，必须中断
Auto Review 文档
  ↓
Baseline
```

Analysis 包含：

1. 信息收集
2. 产品调研与洞察
3. 需求分析

Design 包含：

1. 产品架构设计
2. PRD
3. 功能任务规格
4. UI 信息架构
5. 结构化 UI/交互规格
6. 原型 Prompt 与 UI 标注
7. 产品基线与变更

## 3. 局部流程

支持局部流程，但必须先判断实例和影响范围：

- `analysis-run`：只执行 Analysis，并停在人工评审。
- `design-run`：从产品架构开始，验证 Analysis 是否存在和是否通过。
- `doc-run`：只生成或修复单个文档。
- `change-run`：基于当前 baseline 做局部变更。
- `repair-run`：修复结构、追踪、证据和状态，不改产品事实。
- `discuss-only`：只讨论，不落盘。

## 4. 人工中断点

必须中断等待用户确认：

- `analysis-human-review`
- `product-architecture-human-review`

未获得用户明确确认时，不得把对应阶段状态写为 `approved`。

## 5. 自动检查点

自动检查不等于用户确认。自动检查失败时：

- 写入 `manifest.md`。
- 设置阻塞状态。
- 进入 `repair-run`。

## 6. 回退规则

发现问题时按影响范围回退：

| 问题类型 | 回退位置 |
|---|---|
| 用户调研事实错误 | Analysis |
| 需求边界错误 | 需求分析 |
| 模块边界错误 | 产品架构人工评审 |
| 功能任务结构缺失 | 功能任务 repair-run |
| UI 页面结构压缩 | UI repair-run |
| 变更证据缺失 | baseline / manifest repair-run |
