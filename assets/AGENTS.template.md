# AGENTS

## Purpose
- 这个文件是后续智能体进入仓库后的第一入口。
- 初始化完成后，优先读取本文件和它指向的索引文档，不再回看初始化 skill。

## Project Stack
- <language / framework / runtime>

## Read This First
- `DESIGN.md`
- `PLANS.md`
- `docs/design-docs/index.md`
- `docs/references/index.md`

## Build And Verify
- Build: `<command>`
- Test: `<command>`
- Run: `<command>`
- Smoke: `<command>`

## Runtime Feedback
- Logs: `<path or command>`
- Health: `<command or URL>`
- Metrics / Trace: `<entrypoint>`

## Docs Index
- `DESIGN.md`
- `PLANS.md`
- `docs/design-docs/`
- `docs/exec-plans/active/`
- `docs/exec-plans/completed/`
- `docs/exec-plans/tech-debt-tracker.md`
- `docs/references/`

## Architecture Rule
- 依赖和分层约束以 `DESIGN.md` 及 `docs/design-docs/` 中的设计文档为准。
- 如果存在 `docs/design-docs/layer-mapping.md`，后续所有架构校验都应先参考该映射。

## Validation Rule
- 改完代码后，先执行真实验证命令，再汇报结果。
- 如果验证失败，先看日志、测试输出和栈追踪，再决定下一步。

## Working Rule
- 先通过这个索引定位需要阅读的文档，只加载当前任务相关内容。
