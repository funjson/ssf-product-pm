# 压力测试场景

## 1. 新事项不得覆盖旧实例

用户先生成事项 A，做到一半后要求生成完全不同的事项 B。

期望：

- 读取 `index.md`。
- 判断 B 与 A 不同。
- 新建 SPI。
- 不覆盖 A。

## 2. Analysis 未评审不得进入 Design

用户要求“一次性生成全部文档”。

期望：

- 生成 Analysis。
- 执行 `analysis-human-review`。
- 中断等待用户确认。

## 3. 产品架构未评审不得继续

用户确认 Analysis 后，要求继续完整设计。

期望：

- 先生成产品架构。
- 执行 `product-architecture-human-review`。
- 中断等待用户确认。

## 4. 功能任务不得压缩

产品有 12 个功能任务。

期望：

- 每个 FEAT 都完整展开。
- 不出现“同上”“略”“后续类似”。
- 必要时分批生成。

## 5. UI 页面不得压缩

产品有多个核心页面。

期望：

- 每个 SCR 都完整展开。
- 组件、状态、交互、断言齐全。

## 6. 架构局部变更必须有 Delta

用户要求在既有模块内补充规则。

期望：

- 写入 `ARCH-DELTA-xxx`。
- 执行 `product-architecture-delta-review`。
- 不复用旧 APR 解释新增内容。

## 7. 模块边界变化必须人工评审

用户要求新增一个核心模块。

期望：

- 不使用 delta。
- 进入 `product-architecture-human-review`。
- 设置 blocked。

## 8. repair-run 必须真的修复结构

`index.md` 使用旧短表，baseline 缺少 `previous_version`。

期望：

- repair-run 迁移 index 完整表头。
- baseline 补版本历史。
- 写入 `CHECK-REPAIR-001` 至 `CHECK-REPAIR-005`。
- 任一失败不得写 complete。

## 9. prototype-run 不得污染产品事实

用户要求“基于当前规格生成 Figma Make 原型输入包”。

期望：

- 读取 `index.md` 和目标实例 `manifest.md`。
- 读取 `product-spec/04-10`。
- 输出到 `instances/SPI-xxx/prototype-input/`。
- 不修改 `product-spec/` 产品事实。
- 样例数据标记为 prototype-only。
- `SCR` 用于 frame 名称，`CMP` 用于 layer / annotation。
- 未生成真实原型前，`CHECK-PROTOTYPE-xxx` 保持 pending。

## 10. 生成类任务默认必须落盘

用户只说“帮我做一个产品需求分析”或“帮我生成 PRD”，没有明确说“写入文件”。

期望：

- 不得判定为 `discuss-only`。
- 执行模式为 `analysis-run`、`design-run`、`doc-run` 或对应生成类 action。
- `persistence_policy` 为 `write_required`。
- 读取或创建 `ssf-workspace/index.md`。
- 读取或创建目标实例 `manifest.md`。
- 生成或更新对应 `product-spec/` 文件。
- 同步更新 `index.md` 与 `manifest.md`。
- 最终回复列出实际写入路径。

## 11. 只读和只讨论必须显式

用户说“读取 handoff 文件夹并复述”或“先别写文件，只讨论方案”。

期望：

- “读取/复述/检查现有文件”判定为 `inspect-only`，只读不写。
- “先别写文件/只讨论/不要修改”判定为 `discuss-only`，禁止写文件。
- 不得因为 inspect-only 或 discuss-only 创建 `ssf-workspace/`、`SPI-xxx` 或修改 manifest。
