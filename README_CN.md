# Agent-Harness-Bootstrap

[English](./README.md)

> **别再靠重复提示词带 Agent 干活。先把仓库改造成 Agent 能真正接手的工作环境。**
>
> `agent-harness-bootstrap` 会把一个普通代码仓库整理成真正的 **Agent-Readable（智能体可读）工作空间**：有入口文件、有仓库内规则、有长期记忆层。

![Paradigm](https://img.shields.io/badge/Paradigm-Agent--First-blueviolet.svg)
![Architecture](https://img.shields.io/badge/Architecture-Harness_Engineering-success.svg)
![Output](https://img.shields.io/badge/Output-Agent--Readable_Repo-black.svg)

它背后的核心思路和 OpenAI 提出的 **Harness Engineering** 一致：如果你想让 Agent 稳定工作，就不要把规则塞在 prompt 里，而是把规则写进仓库里。

---

## 为什么会有这个项目

很多团队用不好编码 Agent，不是因为模型不够强，而是因为仓库本身没有准备好。

典型症状就是：

- 每开一个新会话，都要重贴一遍项目背景
- 架构规则只存在聊天记录里，不在版本库里
- Agent 不知道先进哪个文件
- 计划、blocker、技术债没有固定位置
- 代码开始写了，但仓库还没说明这个项目该怎么工作

所以问题不只是“生成质量”，而是仓库没有被工程化成一个能承接 Agent 的工作环境。

`agent-harness-bootstrap` 做的就是第一步：先把这个环境搭起来。

---

## 你最终会得到什么

初始化完成后，仓库就不再只是“代码堆”，而会变成一个 Agent 可以进入、理解、继续工作的工程环境。

你会得到：

- 一个明确的第一入口：`AGENTS.md`
- 一个设计与边界入口：`DESIGN.md`
- 一个任务与验证入口：`PLANS.md`
- 一个放长期记忆的 `docs/` 体系
- 一套索引文件，让 Agent 按层读取上下文，而不是一次吞掉所有历史

结果很直接：

**初始化之后，项目上下文的来源从“聊天记录”切换成“仓库本身”。**

---

## 改造前后

### 改造前

项目只能靠反复提示词驱动：

> “记住这个架构，记住那个规则，先看这个文件，别忘了那个约束，顺便我再把背景给你讲一遍……”

### 改造后

仓库会自己告诉 Agent 该怎么进入项目：

> “先读 `AGENTS.md`，按索引继续读，然后基于仓库里的规则工作。”

这才是真正的变化。

你不再把每个会话都当成一次重新 onboarding，而是把仓库本身变成 Agent 的工程化运行环境。

---

## 会生成什么

最小结构如下：

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

这些文件各自有明确职责：

- `AGENTS.md`
  Agent 进入仓库后的第一入口，只负责路由、索引和阅读顺序。
- `DESIGN.md`
  项目的高层结构、边界和长期约束。
- `PLANS.md`
  当前任务、下一步、验证规则和 blocker 记录方式。
- `docs/design-docs/index.md`
  设计文档索引。
- `docs/references/index.md`
  外部依赖、平台资料、接口说明索引。
- `docs/exec-plans/tech-debt-tracker.md`
  技术债和后续处理入口。

如果项目存在明确分层，还可以额外补：

- `docs/design-docs/layer-mapping.md`

---

## 它和普通模板有什么不一样

普通模板解决的是“目录怎么摆”。

`agent-harness-bootstrap` 解决的是“Agent 进来以后怎么真正开始工作”。

它回答的是普通脚手架很少处理的问题：

- Agent 应该先读哪个文件
- 设计规则该写在哪
- 计划和 blocker 放在哪
- 怎么避免每个会话都重新解释一遍项目
- 怎么把上下文从聊天迁回仓库

这不是为了让仓库“看起来整齐”。

这是为了让 Agent 不只是这次能干活，而是下次还能继续接上。

---

## 自带模板

这个 skill 自带模板，初始化时优先用模板，不靠现场临时组织：

- `assets/AGENTS.template.md`
- `assets/DESIGN.template.md`
- `assets/PLANS.template.md`
- `assets/design-docs.index.template.md`
- `assets/references.index.template.md`
- `assets/tech-debt-tracker.template.md`

可选模板：

- `assets/layer-mapping.template.md`

---

## 适合什么场景

适合这些场景：

- 新项目从第一天开始就按 Agent-first 的方式组织仓库
- 老项目第一次补真正可用的 `AGENTS.md`
- 团队想把 AI 协作规则沉淀进 Git 仓库
- 希望后续 Agent 直接继承文件里的上下文，而不是继续靠聊天记录

不适合这些场景：

- 日常功能开发
- 一次性的 bug 修复
- 单独补一个测试
- 改一页普通文档
- 初始化很久以后，单独加一条局部规则

这些事应该在 harness 之上执行，而不是重新跑一遍初始化。

---

## 边界

这个项目的边界刻意收得很窄。

它只做一件事：

**把 harness 初始化好，一次就够。**

它不负责：

- 替代日常开发
- 替代项目文档本身
- 充当仓库永久的大脑
- 每次 Agent 动代码时都重新执行一次

初始化完成后，仓库本身就应该接管后续规则。

---

## 后续 Agent 该怎么进入项目

初始化之后，默认读取顺序是：

1. `AGENTS.md`
2. `DESIGN.md`
3. `PLANS.md`
4. `docs/design-docs/index.md`
5. `docs/references/index.md`
6. 当前任务真正相关的专题文档

这就是这个项目的核心价值：

它第一次把“Agent 到底该从哪里拿上下文”这件事，变成了一个明确的、可版本化的、属于仓库本身的答案。
