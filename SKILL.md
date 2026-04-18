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

- `assets/layer-mapping.template.md`（分层映射，有显式分层且需要架构边界校验时创建）
- `assets/glossary.template.md`（项目术语表，**多模块项目或复杂项目强烈建议**）
- `assets/ci-validation.template.md`（CI/验证流水线说明，**有 CI/CD 流水的项目建议**）
- `assets/archive-template.md`（计划归档模板，用于 `docs/exec-plans/completed/`）

**可选文档的创建规则：**
- `glossary.md`：多模块项目、有业务术语的项目、需要频繁解释概念的项目应该创建
- `ci-validation.md`：有 CI/CD 流水线的项目应该创建，方便本地开发对照

这些文档不是必需的，但创建后能显著提升开发效率。

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

初始化应支持安全重复运行，且能随 skill 版本演进补进新章节。检测与合并策略如下：

**检测现有文件：**
- 执行 `test -f <file>` 检查文件是否已存在
- 对于已存在的文件，先读取现有内容，再按章节级决定是否补充

**合并策略（按章节级合并）：**

`AGENTS.md` - 检查并补充以下章节（按顺序）：
1. `## First Read` 或 `## Read This First`（关键词：First Read, Read This First, 首次阅读）
2. `## Project Stack`（关键词：Project Stack, 项目栈, 技术栈）
3. `## Build And Verify`（关键词：Build And Verify, 构建和验证）
4. `## Runtime Feedback`（关键词：Runtime Feedback, 运行时反馈）
5. `## Docs Index`（关键词：Docs Index, 文档索引）
6. `## Architecture`（关键词：Architecture, 架构）
7. `## Validation`（关键词：Validation, 验证）
8. `## Working Rule`（关键词：Working Rule, 工作规则）
9. `## Index Maintenance`（关键词：Index Maintenance, 索引维护）- **新增，若缺失则补充**
- 原则：**只补充缺失的章节，不覆盖已存在的章节**

`DESIGN.md` - 检查并补充以下章节：
1. `## Goal`（关键词：Goal, 目标, 项目目标）
2. `## Scope`（关键词：Scope, 边界, 范围）
3. `## Architecture`（关键词：Architecture, 架构）
4. `## Layering`（关键词：Layering, 分层）
5. `## Runtime Flow`（关键词：Runtime Flow, 运行链路）
6. `## Integrations`（关键词：Integrations, 集成）
7. `## Constraints`（关键词：Constraints, 约束）
8. `## Detailed Docs`（关键词：Detailed Docs, 详细文档）
- 原则：**只补充缺失的章节，不覆盖已存在的章节**

`PLANS.md` - 检查并补充以下章节：
1. `## Active Work`（关键词：Active Work, 当前工作）
2. `## Next`（关键词：Next, 下一步）
3. `## Blockers`（关键词：Blockers, 阻塞点）
4. `## Validation Rule`（关键词：Validation Rule, 验证规则）- **特殊处理：即使章节已存在，也必须检查 `<test_command>` 是否已被替换**
5. `## Blocker Handling`（关键词：Blocker Handling, 阻塞处理）
6. `## Active Plans`（关键词：Active Plans, 活跃计划）
- 原则：**只补充缺失的章节，不覆盖已存在的章节**
- **例外：** `Validation Rule` 章节即使已存在，也要检查占位符

**索引文件合并：**
- `docs/design-docs/index.md`：已存在时，合并新增条目，保留现有条目
- `docs/references/index.md`：已存在时，合并新增条目，保留现有条目
- `docs/exec-plans/tech-debt-tracker.md`：已存在时，追加新条目，不覆盖现有内容

**章节合并实现要点：**

**章节检测策略（语义匹配优先，精确匹配兜底）：**
- 不要只依赖精确的章节标题匹配（如 `grep -q '## Index Maintenance'`）
- 使用语义匹配：用正则表达式匹配章节的"核心关键词"，容忍格式变化
- 如果语义匹配失败，再回退到精确标题匹配作为兜底

**示例检测命令（语义匹配）：**
```bash
# 检查核心文件是否存在
test -f AGENTS.md && echo "AGENTS.md exists" || echo "AGENTS.md missing"
test -f DESIGN.md && echo "DESIGN.md exists" || echo "DESIGN.md missing"
test -f PLANS.md && echo "PLANS.md exists" || echo "PLANS.md missing"

# 语义匹配：检查 Index Maintenance 章节（容忍大小写、空格、符号变化）
grep -qiE '^#+\s*(index\s*maintenance|maintenance\s*of\s*index|索引维护)' AGENTS.md && echo "Index Maintenance exists" || echo "Index Maintenance missing"

# 语义匹配：检查 Validation 章节（容忍变化）
grep -qiE '^#+\s*(validation|验证|验证规则)' PLANS.md && echo "Validation exists" || echo "Validation missing"

# 语义匹配：检查 Goal 章节（容忍变化）
grep -qiE '^#+\s*(goal|目标|项目目标)' DESIGN.md && echo "Goal exists" || echo "Goal missing"
```

**风险说明：**
- 老项目可能修改过章节标题（如 `## Validation` → `## Validation & Checks`）
- 只用精确匹配会导致"误判为缺失"，重复添加章节
- 语义匹配能降低这种误判，但不能完全消除
- 对于高度定制的老项目，建议手动 review 合并结果

**合并流程：**
1. 对每个章节，先用语义匹配检测是否存在
2. **如果存在：**
   - 普通章节：跳过该章节的追加写入
   - **特殊章节（PLANS.md 的 Validation Rule）：检查是否包含占位符**
     - 使用 `grep -q '<[^>]+>'` 检测是否包含 `<test_command>` 等占位符
     - 如果有占位符，根据项目扫描结果替换为真实值（如 `npm test`、`pytest`、`gradlew test`）
     - 汇报时注明："Validation Rule 章节已存在，替换了占位符"
3. **如果不存在：**
   - 从模板中提取该章节内容
   - 替换模板中的占位符为真实值
   - 追加到文件末尾
4. 汇报时列出：新建的文件、新增的章节、跳过的章节（原因）、替换的占位符

**占位符检测和替换示例：**
```bash
# 检测 PLANS.md 是否包含未替换的占位符
grep -qE '<[^>]+>' PLANS.md && echo "Found placeholders" || echo "No placeholders"

# 检测特定占位符
grep -q '<test_command>' PLANS.md && echo "test_command not replaced"

# 替换占位符（示例）
sed -i 's/<test_command>/npm test/g' PLANS.md
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
- **重要：** 即使 PLANS.md 的 Validation Rule 章节已存在，也要检查并替换占位符

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
