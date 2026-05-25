# 状态资产协议

## 1. 状态资产定位

状态资产不是说明文档，而是 Agent 判断流程的依据。

核心状态资产：

- `ssf-workspace/index.md`
- `instances/SPI-xxx/manifest.md`
- `product-spec/10-product-baseline-change.md`

## 2. Workspace Index

`index.md` 管理跨实例调度。

必须记录：

- 实例 ID。
- 实例名称。
- 产品 / 项目名称。
- 任务类型。
- 当前阶段。
- 当前状态。
- 阻塞 Review Gate。
- 最近运行模式。
- 下一步建议动作。
- 最近更新时间。
- 实例路径。

禁止降级为旧版短表。

## 3. Instance Manifest

`manifest.md` 管理单实例流程状态。

必须记录：

- 实例身份。
- 当前阶段。
- active gate。
- blocked。
- current blocker。
- next allowed actions。
- 文档状态。
- Review Gate 状态。
- 人工确认记录。
- 自动检查记录。
- 产品架构 Delta 记录。
- 运行记录。

## 4. Baseline

`10-product-baseline-change.md` 管理当前产品事实基线。

必须记录：

- `current_version`
- `previous_version`
- 版本历史。
- 当前模块、功能、页面、规则基线。
- 关键决策。
- 废弃设计。
- 每次 `CHG-xxx` 的变更前、变更后、影响范围、回归关注点。

## 5. 状态优先级

流程判断优先级：

```text
用户当前明确指令
  >
index.md
  >
manifest.md
  >
baseline
  >
正文文档
```

如果状态资产与正文冲突，必须进入 repair-run，而不是自行猜测。
