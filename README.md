# init-project

`init-project` 是一个一次性初始化 skill。

它的用途不是帮智能体长期干活，而是把一个普通代码仓库，改造成一个后续智能体能直接读、直接接手的项目环境。

换句话说，这个 skill 做的是第一步：

- 创建根级入口文件
- 建立 `docs/` 记录系统
- 给文档补索引
- 把后续协作规则写进仓库

初始化完成后，后续智能体不应该继续依赖这个 skill，而应该直接读取仓库里的 `AGENTS.md`、`DESIGN.md`、`PLANS.md` 和 `docs/` 文档。

## 这个 skill 解决什么问题

很多项目的问题不是“AI 不会写代码”，而是：

- 仓库里没有给智能体看的入口
- 规则散落在聊天记录里
- 项目背景只存在于人脑子里
- 后来的智能体不知道先看什么
- 同一个项目每次初始化结果都不一样

这个 skill 的目的，就是把这些信息第一次写进仓库，让仓库本身成为后续工作的依据。

## 它会生成什么

初始化后，项目至少会有这套结构：

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

其中各文件的职责是：

- `AGENTS.md`
  后续智能体进入仓库后的第一入口，只负责索引和阅读顺序。
- `DESIGN.md`
  项目高层设计、边界、核心结构。
- `PLANS.md`
  当前活跃任务、下一步、验证规则、blocker 记录方式。
- `docs/design-docs/index.md`
  设计文档目录。
- `docs/references/index.md`
  外部依赖、接口、平台资料入口。
- `docs/exec-plans/tech-debt-tracker.md`
  技术债记录入口。

如果项目确实有明确分层，还可以额外生成：

- `docs/design-docs/layer-mapping.md`

## 模板文件

这个 skill 自带一组模板，初始化时优先用模板，不要让模型现场编一套新格式。

核心模板：

- `assets/AGENTS.template.md`
- `assets/DESIGN.template.md`
- `assets/PLANS.template.md`
- `assets/design-docs.index.template.md`
- `assets/references.index.template.md`
- `assets/tech-debt-tracker.template.md`

可选模板：

- `assets/layer-mapping.template.md`

## 什么时候该用

适合下面这些场景：

- 新项目第一次初始化
- 老项目第一次补 `AGENTS.md`
- 老项目第一次建立 `docs/` 记录系统
- 希望以后智能体不再依赖聊天记录，而是直接依赖仓库文档

## 什么时候不该用

不适合下面这些场景：

- 日常开发任务
- 修一个具体 bug
- 补一个单独测试
- 改一页普通文档
- 后续某次单独加一条架构规则

这些工作应该直接按项目仓库里已经写好的规则做，而不是重新跑一遍初始化。

## 这个 skill 的边界

它只负责第一次把规则载体建起来。

它不负责：

- 长期替代 `AGENTS.md`
- 长期替代项目设计文档
- 反复参与日常编码
- 成为每次任务都要回看的总入口

初始化完成后，仓库本身才是规则来源。

## 初始化完成后的工作方式

后续智能体默认按这个顺序读取项目：

1. `AGENTS.md`
2. `DESIGN.md`
3. `PLANS.md`
4. `docs/design-docs/index.md`
5. `docs/references/index.md`
6. 当前任务真正相关的专题文档

这也是这个 skill 的最终目标：让后续工作不再依赖这个 skill，而是依赖仓库。
