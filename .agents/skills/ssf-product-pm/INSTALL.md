# 安装与跨平台适配说明

## 1. 通用原则

本 Skill 的核心事实源只有一套：

- `SKILL.md`
- `templates/`
- `references/`

不同平台的规则文件只负责把 Agent 引导到这套事实源，不要在多个平台规则里复制大量模板正文，避免规则漂移。

## 2. Claude Code

复制到项目级 Skill：

```bash
mkdir -p .claude/skills/ssf-product-pm
cp SKILL.md .claude/skills/ssf-product-pm/SKILL.md
```

使用方式：

```text
/ssf-product-pm 生成一个健康管理 App 的产品设计文档
```

## 3. Codex

Codex Skill 位置建议：

```bash
mkdir -p .agents/skills/ssf-product-pm
cp SKILL.md .agents/skills/ssf-product-pm/SKILL.md
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
使用 ssf-product-pm，根据下面的产品想法生成完整产品设计包。要求输出 9 个产品版本文档，遵守 templates 中的模板，不要生成传统需求池、优先级矩阵、Roadmap。
生成文件前先读取或创建 ssf-workspace/index.md；如果这是新产品，创建新的实例目录，不要覆盖已有实例。
如果需要重新生成、覆盖、跳阶段或变更，先执行 intake gate。

产品想法：...
```

### 单个功能任务规格

```text
使用 ssf-product-pm，只生成 FEAT-xxx 的功能任务规格。要求包含目标、用户故事、输入输出、主流程、分支流程、异常流程、业务规则、权限、关联页面、验收标准和测试关注点。
如果某个小节暂无内容，也要保留小节并写“无 / 暂无 / 待确认”。
必须关联产品模块 MOD-xxx；如果产品架构缺失，标记“模块待补齐”并提出待确认问题。
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
