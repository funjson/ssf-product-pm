# 运行时协议

## 1. 执行前必须判断

任何任务执行前必须判断：

1. 用户意图属于哪种执行模式。
2. 执行模式对应的 `persistence_policy` 是 `write_required`、`read_only` 还是 `write_forbidden`。
3. 是否已有 `ssf-workspace/index.md`。
4. 当前请求是新实例、旧实例续跑、旧实例变更、repair-run、inspect-only，还是 discuss-only。
5. 是否触发 intake gate。
6. 是否存在人工评审阻塞。

只有 `analysis-human-review` 和 `product-architecture-human-review` 能形成用户确认阻塞。auto_review 通过后不得阻塞等待用户确认；auto_review 失败时进入 repair-run。

## 2. 持久化策略

默认规则：

- `write_required`：必须写入或更新文件。适用于 `full-run`、`analysis-run`、`design-run`、`flow-run`、`doc-run`、`change-run`、`prototype-run` 和 `repair-run`。
- `read_only`：只允许读取、检查、复述和给出问题清单。适用于用户明确要求“读取”“检查”“复述”“审阅现有文件”，且没有要求生成或修改产物。
- `write_forbidden`：禁止写文件。仅适用于用户明确要求“只讨论”“先讲方案”“先别写文件”“不要修改文件”。

判定规则：

1. 用户要求生成、修改、补齐、修复、续跑、重跑、输出某类 PM 产物或输出 prototype 时，默认是 `write_required`。
2. 用户没有说“落盘”或“生成文件”时，不得自动降级为 `discuss-only`。
3. 只有用户明确要求不写文件时，才允许进入 `write_forbidden`。
4. 只有用户明确要求读取、检查、复述现有文件且没有生成产物诉求时，才允许进入 `read_only`。
5. `write_required` 完成前必须验证目标文件、`index.md` 和目标实例 `manifest.md` 已同步；否则不得声称任务完成。

## 3. 实例判断

每个独立产品、功能事项或变更任务都必须归属到一个 `SPI-xxx` 实例。

不得把新事项覆盖到旧实例。无法判断时必须让用户选择：

- 新建实例。
- 作为已有实例变更。
- 修复已有实例。
- 只读取检查不落盘。
- 只讨论不落盘。

## 4. 高风险动作

以下动作必须先执行 intake gate：

- 重新生成、重做、再来一版。
- 覆盖、删除旧内容。
- 跳阶段执行。
- 基于旧版本变更。
- 用户输入明显像另一个产品。

## 5. 跳阶段规则

跳阶段允许，但必须写明：

- 本阶段依赖哪些上游输入。
- 现有实例已经有哪些上游输入。
- 缺失哪些输入。
- 本次基于哪些模型假设。
- 哪些内容后续必须回填。

跳过人工评审节点时，不得把后续文档写成 `approved`。

## 6. 写入规则

每次生成或修改文件后，必须同步更新：

- `ssf-workspace/index.md`
- `instances/SPI-xxx/manifest.md`
- 必要时更新 `10-product-baseline-change.md`

只改正文不改状态资产，视为未完成。

`write_required` 动作的最终回复必须列出实际写入或更新的路径。若没有写入任何文件，必须说明阻塞原因，不能把聊天正文当成已完成产物。

## 7. prototype-run 规则

prototype-run 写入 `instances/SPI-xxx/prototype-input/`。

执行时必须：

- 读取目标实例 `manifest.md`。
- 读取 `product-spec/04-10`。
- 不修改 `product-spec/` 产品事实。
- 不把样例数据写回 baseline。
- 未生成真实原型时，真实原型检查保持 `pending`。
