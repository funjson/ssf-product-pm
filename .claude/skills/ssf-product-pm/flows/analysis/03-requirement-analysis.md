# 03 需求分析节点规则

## 使用模板

`templates/analysis/03-requirement-analysis.md`

## 目标

将 `RAW / INS / NEED / PROB` 转化为结构化 `REQ`。

## 必须包含

- 问题域分析。
- 用户需求归纳。
- 场景需求分析。
- 能力需求推导。
- 需求边界。
- 约束与风险。
- 进入产品架构的需求清单。

## 输出到下游

需求分析必须为产品架构提供：

- `REQ-xxx`
- 建议能力 `CAP`
- 建议模块方向 `MOD`
- 建议功能任务 `FEAT`

Analysis 阶段结束后必须触发 `analysis-human-review`。
