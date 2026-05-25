# 安装与跨平台适配说明

## 1. 通用原则

本 Skill 的核心事实源只有一套：

- `SKILL.md`
- `core/`
- `flows/`
- `registries/`
- `templates/`
- `references/`

不同平台的规则文件只负责把 Agent 引导到这套事实源，不要在多个平台规则里复制大量模板正文，避免规则漂移。

## 2. Claude Code

复制到项目级 Skill：

```bash
mkdir -p .claude/skills/ssf-product-pm
cp -R SKILL.md README.md core flows registries references templates .claude/skills/ssf-product-pm/
```

使用方式：

```text
/ssf-product-pm 生成一个健康管理 App 的产品设计文档
```

## 3. Codex

Codex Skill 位置建议：

```bash
mkdir -p .agents/skills/ssf-product-pm
cp -R SKILL.md AGENTS.md README.md core flows registries references templates .agents/skills/ssf-product-pm/
```

同时保留仓库根目录的 `AGENTS.md`，用于稳定加载项目规则。

## 4. Cursor

Cursor 规则文件已提供：

```text
.cursor/rules/ssf-product-pm.mdc
```

规则只做路由和约束，实际模板读取 `templates/`。

## 5. Qoder

Qoder 规则文件已提供：

```text
.qoder/rules/ssf-product-pm.md
```

同时 Qoder 支持读取项目中的 `AGENTS.md`，因此建议保留根目录 `AGENTS.md`。

## 6. Trae

Trae 规则文件已提供：

```text
.trae/rules/project_rules.md
```

若 Trae 当前版本的规则入口不同，可把该文件内容复制到项目规则配置中。

## 7. 推荐调用提示词

### 完整产品设计包

```text
使用 ssf-product-pm，根据下面的产品想法生成完整产品设计包。要求按 Analysis 和 Design 两阶段执行，遵守 references 和 templates 中的配置，不要生成传统需求池、优先级矩阵、Roadmap。
生成文件前先读取或创建 ssf-workspace/index.md；如果这是新产品，创建新的实例目录，不要覆盖已有实例。
如果需要重新生成、覆盖、跳阶段或变更，先执行 intake gate。
Analysis 阶段结束后停止等待人工评审；产品架构设计结束后再次停止等待人工评审。

产品想法：...
```

### 分析阶段

```text
使用 ssf-product-pm，先执行 Analysis 阶段：信息收集、产品调研与洞察、需求分析。
如果我没有提供完整客户现场信息，可以先根据常识补充假设，但必须标记“模型假设 / 待确认”。
完成后执行 analysis-human-review 并停止，等待我确认后再进入设计。
```

### 产品架构设计

```text
使用 ssf-product-pm，基于已通过评审的 Analysis 文档生成产品架构设计。
要求包含模块划分策略、CAP/MOD/OBJ、模块边界、REQ -> MOD -> FEAT 映射、Mermaid 产品模块图、Mermaid 用户任务流/模块协作图。
完成后执行 product-architecture-human-review 并停止，等待我确认。
```

### 单个功能任务规格

```text
使用 ssf-product-pm，只生成 FEAT-xxx 的功能任务规格。要求包含目标、用户故事、输入输出、主流程、分支流程、异常流程、业务规则、权限、关联页面、验收标准和测试关注点。
如果某个小节暂无内容，也要保留小节并写“无 / 暂无 / 待确认”。
必须关联产品模块 MOD-xxx；如果产品架构缺失，标记“模块待补齐”并提出待确认问题。
如果产品架构未通过人工评审，不要把本功能任务标记为已确认。
```

### UI 原型输入

```text
使用 ssf-product-pm，基于已有产品架构和功能任务规格生成 UI 信息架构、结构化 UI/交互规格、原型生成 Prompt 与 UI 标注说明。要求所有页面和组件都有 ID，并能追溯到模块、功能、规则和验收标准。
每个 SCR 页面必须完整展开，不得用多个页面合并总表替代。
```

### 需求变更

```text
使用 ssf-product-pm，基于当前产品基线处理下面的需求变更。要求输出变更前、变更后、影响范围、需要修改的功能/页面/规则/验收，以及回归关注点。
修改前先读取 ssf-workspace/index.md 和目标实例 manifest.md，确认变更属于哪个实例。

变更：...
```
