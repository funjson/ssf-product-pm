# architecture-delta 节点规则

## 1. 适用场景

变更修改了产品架构文档，但没有新增、删除、合并、拆分模块，也没有改变模块职责边界。

## 2. 必须输出

- `ARCH-DELTA-xxx`
- 触发变更 `CHG-xxx`
- 影响范围 `CAP / MOD / OBJ / ARCH-DEC / FEAT / SCR`
- 是否改变模块边界：必须为 `no`
- Review Gate：`product-architecture-delta-review`

## 3. 禁止事项

- 不得把新架构内容解释为旧 `APR-xxx` 已确认。
- 不得在改变模块边界时使用 delta。
- 不得只更新产品架构，不更新 baseline 和 manifest。

## 4. 升级条件

发现以下任一情况，必须升级人工评审：

- 新增或删除模块。
- 合并或拆分模块。
- 改变模块职责。
- 改变关键上下游边界。
