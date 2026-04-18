---
name: init-project
description: 将现有代码仓库初始化为适合 AI Agent 持续协作的项目环境，第一次创建或补齐 AGENTS.md、DESIGN.md、PLANS.md、docs/ 及索引文档，并把后续工作的规则写入仓库。当用户提到初始化项目、第一次建立 AGENTS.md、把仓库改造成 Agent-Readable、建立 docs 记录系统、给项目落地统一模板框架时使用。本 skill 只用于项目初始化，初始化完成后，后续任务应优先读取仓库内 AGENTS.md 和索引文档，不再依赖本 skill 作为持续工作规则来源。
metadata:
  tags: [project, docs, bootstrap, agent]
  author: "OpenAI Codex"
  version: "2.0.0"
---

# 初始化 Agent 可读项目环境

## 定位

- 这是一次性初始化 skill。
- 目标是把规则写进仓库，不是把规则长期留在 skill 里。
- 初始化完成后，后续智能体应从仓库根目录 `AGENTS.md`、`DESIGN.md`、`PLANS.md` 和 `docs/` 索引读取规则。

## 何时使用

只在下面场景使用：

- 新项目第一次搭建 Agent 可读环境
- 老项目第一次补 `AGENTS.md`、`DESIGN.md`、`PLANS.md`
- 第一次建立 `docs/` 记录系统和索引文档
- 第一次为项目落地统一模板框架

不要在下面场景重复使用：

- 日常编码
- 日常修测试
- 局部补文档
- 后续某次单独补一条架构规则

这些工作应直接根据仓库里的 `AGENTS.md` 和索引文档执行。

## 初始化目标

完成后，仓库至少具备下面这些能力：

1. 有清晰的根级入口：`AGENTS.md`、`DESIGN.md`、`PLANS.md`
2. 有 `docs/` 作为记录系统
3. 有索引文档，支持按需加载上下文
4. 有模板化的规则承载文件，而不是把规则留在聊天里

## 标准模板框架

优先使用本 skill 自带模板，不要现场随意发挥。

### 核心模板

- `assets/AGENTS.template.md`
- `assets/DESIGN.template.md`
- `assets/PLANS.template.md`
- `assets/design-docs.index.template.md`
- `assets/references.index.template.md`
- `assets/tech-debt-tracker.template.md`

### 可选模板

按项目复杂度或技术栈选择：

- `assets/layer-mapping.template.md`

只有在项目确实存在显式分层、需要后续做架构边界校验时，才创建 `layer-mapping.md`。

## 落盘规则

### 开工前

1. 确认项目根目录。
2. 扫描现有结构，识别语言、框架、构建工具、测试工具、启动方式。
3. 检查目标文件是否已存在。

### 写入原则

1. 已有文件优先补充和合并，不要无条件覆盖。
2. `AGENTS.md` 只做索引和工作入口，不写成长篇规则大全。
3. 长期有效的规则写进仓库文档模板，不要只写在 skill 里。
4. 模板里的示例字段要替换成当前项目真实信息，不要保留占位值。

## 目标目录结构

初始化后，至少应具备下面的结构：

```text
docs/
  design-docs/
    index.md
  exec-plans/
    active/
    completed/
    tech-debt-tracker.md
  references/
    index.md
DESIGN.md
PLANS.md
AGENTS.md
```

## 执行顺序

### 1. 建立记录系统

创建或补齐：

- `docs/design-docs/`
- `docs/exec-plans/active/`
- `docs/exec-plans/completed/`
- `docs/references/`

### 2. 写入根级入口文件

根据模板创建或补齐：

- `AGENTS.md`
- `DESIGN.md`
- `PLANS.md`

### 3. 写入索引文件

根据模板创建或补齐：

- `docs/design-docs/index.md`
- `docs/references/index.md`
- `docs/exec-plans/tech-debt-tracker.md`

### 4. 按需补充分层映射

如果项目存在明确分层，或者用户明确要求为后续架构约束做准备，再创建：

- `docs/design-docs/layer-mapping.md`

### 5. 汇报初始化结果

向用户汇报：

- 新建或更新了哪些核心文件
- 当前目录结构
- 哪些模板已落地
- 哪些内容还保留为待补充占位

## 完成条件

只有满足下面条件，才能认为初始化完成：

1. 核心目录和文件已经落盘
2. `AGENTS.md` 能指向其他核心文档
3. `DESIGN.md`、`PLANS.md`、`index.md` 已经具备最小可用内容
4. 后续智能体不需要回来看本 skill，也能根据仓库里的文档继续工作

## 交付要求

汇报时重点说产物，不要讲执行过程流水账。至少包括：

- 创建了哪些文件和目录
- 目录结构
- 哪些规则已经写进仓库
- 哪些内容还需要项目负责人补充真实信息

## 退出规则

初始化完成后，不要再把本 skill 当作后续工作的长期规则来源。

后续任务的读取顺序应当是：

1. `AGENTS.md`
2. `DESIGN.md`
3. `PLANS.md`
4. `docs/design-docs/index.md`
5. `docs/references/index.md`
6. 具体专题文档
