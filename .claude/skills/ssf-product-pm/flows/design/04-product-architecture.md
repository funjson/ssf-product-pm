# 04 产品架构节点规则

## 使用模板

`templates/design/04-product-architecture.md`

## 目标

将需求组织为产品能力、功能模块、业务对象和模块边界。

## 必须包含

- 模块划分策略。
- `CAP / MOD / OBJ`。
- 模块边界：包含什么、不包含什么。
- `REQ -> MOD -> FEAT` 映射。
- Mermaid 产品模块图。
- Mermaid 用户任务流或模块协作图。
- `ARCH-DEC-xxx` 决策表。

## 门禁

初次产品架构必须执行 `product-architecture-human-review` 并中断。

## 迭代处理

功能迭代或 change-run 修改产品架构时：

- 改变模块边界：进入人工评审。
- 不改变模块边界：写 `ARCH-DELTA-xxx`，执行 `product-architecture-delta-review`。
