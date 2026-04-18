---
name: agent-harness-bootstrap
description: 第一次把代码仓库整理成 Agent 可读的项目结构，创建或补齐 AGENTS.md、DESIGN.md、PLANS.md、docs/ 和索引文档，把后续规则写进仓库。当用户提到初始化项目、第一次建立 AGENTS.md、把老项目改造成 Agent-Readable、建立 docs 记录系统、落地统一项目模板时使用。初始化完成后，后续任务直接读取仓库内 AGENTS.md 和索引文档，不再重复使用本 skill。
metadata:
  tags: [project, docs, bootstrap, agent]
---

# 初始化项目

这个 skill 只做第一次初始化。

- 创建 `AGENTS.md`、`DESIGN.md`、`PLANS.md`
- 建 `docs/` 和索引文件
- 把后续协作规则写进仓库

初始化完成后，后续智能体直接读仓库里的 `AGENTS.md`、`DESIGN.md`、`PLANS.md` 和 `docs/`。

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

初始化时优先用现成模板。

核心模板：

- `assets/AGENTS.template.md`
- `assets/DESIGN.template.md`
- `assets/PLANS.template.md`
- `assets/design-docs.index.template.md`
- `assets/core-flows.template.md`
- `assets/references.index.template.md`
- `assets/module-validation.template.md`
- `assets/tech-debt-tracker.template.md`

可选模板：

- `assets/layer-mapping.template.md`（分层映射）
- `assets/glossary.template.md`（项目术语表，多模块项目强烈建议）
- `assets/ci-validation.template.md`（CI/验证流水线说明）
- `assets/archive-template.md`（计划归档模板，用于 `docs/exec-plans/completed/`）

只有项目确实有显式分层，而且后面会做架构边界校验时，才创建 `layer-mapping.md`。

如果项目是老项目、多模块项目，初始化时优先补下面两份资料：

- `docs/design-docs/core-flows.md`
- `docs/references/module-validation.md`

这两份比继续补通用模板更值钱。它们直接影响后续编码和复杂问题排查的速度。

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
6. 如果项目是老项目、多模块项目，优先补：
   - `docs/design-docs/core-flows.md`
   - `docs/references/module-validation.md`
7. 如果项目需要分层映射，再补：
   - `docs/design-docs/layer-mapping.md`

## 写入规则

- 已有文件优先补充和合并，不要无条件覆盖。
- `AGENTS.md` 只做入口和索引。
- 长期规则写进仓库文档，不要只写在 skill 里。
- 模板里的占位内容要替换成项目真实信息，不要原样保留。

## 幂等执行策略

初始化应支持安全重复运行。检测与合并策略如下：

**检测现有文件：**
- 执行 `test -f <file>` 检查文件是否已存在
- 对于已存在的文件，先读取现有内容，再决定是补充还是跳过

**合并策略：**
- `AGENTS.md`：已存在时，检查是否包含 `Read This First` 章节，若缺失则补充
- `DESIGN.md`：已存在时，检查是否包含 `Goal` 章节，若缺失则补充
- `PLANS.md`：已存在时，检查是否包含 `Validation Rule` 章节，若缺失则补充
- 索引文件（`index.md`）：已存在时，合并新增条目，保留现有条目
- `tech-debt-tracker.md`：已存在时，追加新条目，不覆盖现有内容

**冲突处理：**
- 如果检测到文件内容已包含模板的关键章节（通过章节标题匹配），则跳过该文件的写入
- 在汇报时明确列出：新建的文件、更新的文件、跳过的文件（原因）

**示例检测命令：**
```bash
# 检查核心文件是否存在
test -f AGENTS.md && echo "AGENTS.md exists" || echo "AGENTS.md missing"
test -f DESIGN.md && echo "DESIGN.md exists" || echo "DESIGN.md missing"
test -f PLANS.md && echo "PLANS.md exists" || echo "PLANS.md missing"
```

## 完成标准

初始化完成时，至少要满足下面几点：

1. 核心目录和文件已经落盘
2. `AGENTS.md` 能指向其他核心文档
3. `DESIGN.md`、`PLANS.md`、索引文件已经有最小可用内容
4. 后续智能体不需要回来看本 skill，也能继续工作

**自验证命令（执行此命令验证完成度）：**
```bash
set -e
test -f AGENTS.md || { echo "FAIL: AGENTS.md missing"; exit 1; }
test -f DESIGN.md || { echo "FAIL: DESIGN.md missing"; exit 1; }
test -f PLANS.md || { echo "FAIL: PLANS.md missing"; exit 1; }
test -d docs/design-docs || { echo "FAIL: docs/design-docs/ missing"; exit 1; }
test -d docs/exec-plans/active || { echo "FAIL: docs/exec-plans/active/ missing"; exit 1; }
test -d docs/exec-plans/completed || { echo "FAIL: docs/exec-plans/completed/ missing"; exit 1; }
test -d docs/references || { echo "FAIL: docs/references/ missing"; exit 1; }
test -f docs/design-docs/index.md || { echo "FAIL: docs/design-docs/index.md missing"; exit 1; }
test -f docs/references/index.md || { echo "FAIL: docs/references/index.md missing"; exit 1; }
test -f docs/exec-plans/tech-debt-tracker.md || { echo "FAIL: tech-debt-tracker.md missing"; exit 1; }

# 检查占位符是否被替换（若包含尖括号占位符则警告）
if grep -qE '<[^>]+>' AGENTS.md DESIGN.md PLANS.md docs/design-docs/index.md docs/references/index.md; then
  echo "WARNING: Found placeholder content that should be replaced"
fi

echo "PASS: All required files and directories exist"
```

**最小可用内容检查：**
- `AGENTS.md` 包含 `Read This First` 章节
- `DESIGN.md` 包含 `Goal` 章节
- `PLANS.md` 包含 `Validation Rule` 章节，且 `<test_command>` 已被替换为实际命令

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

## AGENTS.md 与 CLAUDE.md 兼容性

- 本 skill 使用 `AGENTS.md` 作为智能体入口（源自 OpenAI Harness Engineering 约定）。
- Claude Code 原生会读取根目录的 `CLAUDE.md`。
- 兼容方式：初始化时在 `CLAUDE.md` 中添加一行指向 `AGENTS.md`，内容如下：

  ```markdown
  # CLAUDE

  项目智能体入口请阅读 `AGENTS.md`。
  ```

- 或直接将 `AGENTS.md` 作为 `CLAUDE.md` 使用，在文件头部添加 Claude 相关说明。

## DESIGN.md 与 docs/design-docs/ 职责划分

避免职责重叠，明确分工：

**DESIGN.md（单页总览）：**
- 职责：高层项目概述，作为索引入口
- 内容范围：
  - 项目 Goal、Scope
  - 核心模块或分层（概要）
  - 关键 Runtime Flow（简述）
  - 主要 Integrations（列表）
  - 指向 `docs/design-docs/index.md` 的链接
- 不展开：详细的架构设计、具体的链路说明、技术细节

**docs/design-docs/（深入专题）：**
- 职责：详细设计文档的存储和索引
- 内容范围：
  - `core-flows.md`：详细的调用链路分析
  - `layer-mapping.md`：完整的分层映射
  - 其他专题设计文档
- 更新方式：每次新增专题文档时更新 `index.md`

**协作规则：**
- `DESIGN.md` 保持简洁，通过链接指向详细文档
- 详细设计放在 `docs/design-docs/` 下，通过 `index.md` 组织
- Agent 先读 `DESIGN.md` 了解全局，再根据需要深入 `docs/design-docs/`
