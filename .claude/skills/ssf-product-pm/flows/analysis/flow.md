# Analysis Flow

## 1. 目标

回答：

```text
为什么做？
真实用户是谁？
客户现场发生了什么？
哪些是事实，哪些是假设？
哪些需求可以进入设计？
```

## 2. 节点顺序

```text
01 信息收集
  ↓
02 产品调研与洞察
  ↓
03 需求分析
  ↓
analysis-human-review
```

## 3. 输入

- 用户原始想法。
- 客户现场访谈、用户原话、观察记录。
- 市场/竞品资料。
- 已有系统、旧流程、原型、文档。
- 模型假设，必须显式标记。

## 4. 输出

- `product-spec/01-analysis-input.md`
- `product-spec/02-research-insight.md`
- `product-spec/03-requirement-analysis.md`
- `manifest.md` 中的 `analysis-human-review` 状态。

## 5. 门禁

Analysis 结束必须中断，等待用户确认。

未通过前不得继续 Design；如果用户强制跳过，后续文档必须标记风险。
