---
name: init-project
description: 第一次把代码仓库初始化成 Agent 可读的项目结构，创建或补齐 AGENTS.md、DESIGN.md、PLANS.md、docs/ 及索引文档，并把后续工作规则写进仓库。当用户提到初始化项目、第一次建立 AGENTS.md、把老项目改造成 Agent-Readable、建立 docs 记录系统、落地统一项目模板时使用。初始化完成后，后续任务应直接读取仓库内 AGENTS.md 和索引文档，不再重复使用本 skill。
metadata:
  tags: [project, docs, bootstrap, agent]
---

# 初始化项目

## 这个 skill 负责什么

- 只做一次性的项目初始化。
- 把规则写进仓库，不把规则留在聊天里。
- 初始化完成后，后续智能体直接读仓库里的 `AGENTS.md`、`DESIGN.md`、`PLANS.md` 和 `docs/`。

## 什么时候用

只在下面场景使用：

- 新项目第一次搭建 Agent 可读环境
- 老项目第一次补 `AGENTS.md`、`DESIGN.md`、`PLANS.md`
- 第一次建立 `docs/` 记录系统和索引文档
- 第一次给项目落统一模板

不要在这些场景重复使用：

- 日常开发
- 日常修测试
- 局部补文档
- 某次单独补一条架构规则

这些工作都应该直接按仓库里的文档做。

## 用哪些模板

初始化时优先使用现成模板，不要现场自由发挥。

核心模板：

- `assets/AGENTS.template.md`
- `assets/DESIGN.template.md`
- `assets/PLANS.template.md`
- `assets/design-docs.index.template.md`
- `assets/references.index.template.md`
- `assets/tech-debt-tracker.template.md`

可选模板：

- `assets/layer-mapping.template.md`

只有项目确实有显式分层，而且后面会做架构边界校验时，才创建 `layer-mapping.md`。

## 怎么执行

1. 先确认项目根目录。
2. 扫描现有结构，识别语言、框架、构建工具、测试工具、启动方式。
3. 创建或补齐这些目录：
   - `docs/design-docs/`
   - `docs/exec-plans/active/`
   - `docs/exec-plans/completed/`
   - `docs/references/`
4. 创建或补齐这些根级文件：
   - `AGENTS.md`
   - `DESIGN.md`
   - `PLANS.md`
5. 创建或补齐这些索引文件：
   - `docs/design-docs/index.md`
   - `docs/references/index.md`
   - `docs/exec-plans/tech-debt-tracker.md`
6. 如果项目需要分层映射，再补：
   - `docs/design-docs/layer-mapping.md`

## 写入规则

- 已有文件优先补充和合并，不要无条件覆盖。
- `AGENTS.md` 只做入口和索引，不写成长篇说明。
- 长期规则写进仓库文档，不要只写在 skill 里。
- 模板里的占位内容要替换成项目真实信息，不要原样保留。

## 完成标准

初始化完成时，至少要满足下面几点：

1. 核心目录和文件已经落盘
2. `AGENTS.md` 能指向其他核心文档
3. `DESIGN.md`、`PLANS.md`、索引文件已经有最小可用内容
4. 后续智能体不需要回来看本 skill，也能继续工作

## 汇报时要说什么

- 新建或更新了哪些核心文件
- 当前目录结构
- 哪些模板已经落地
- 哪些地方还需要项目负责人补真实信息

## 初始化完成后怎么读仓库

后续任务默认按这个顺序读取：

1. `AGENTS.md`
2. `DESIGN.md`
3. `PLANS.md`
4. `docs/design-docs/index.md`
5. `docs/references/index.md`
6. 具体专题文档
