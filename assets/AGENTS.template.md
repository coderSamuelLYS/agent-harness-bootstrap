# AGENTS

## First Read
- 先看这个文件，再按这里的链接继续读。

## Project Stack
- <language / framework / runtime>

## Read This First
- `DESIGN.md`
- `PLANS.md`
- `docs/design-docs/index.md`
- `docs/references/index.md`
- `docs/design-docs/core-flows.md`  # 如果项目已补主链路说明，优先读
- `docs/references/module-validation.md`  # 如果项目已补模块验证说明，优先读

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
- `docs/design-docs/core-flows.md`
- `docs/design-docs/glossary.md`  # 如果项目已创建术语表，理解业务概念时优先读
- `docs/exec-plans/active/`
- `docs/exec-plans/completed/`
- `docs/exec-plans/tech-debt-tracker.md`
- `docs/references/`
- `docs/references/module-validation.md`
- `docs/references/ci-validation.md`  # 如果项目已创建 CI 验证说明，查看验证命令时优先读

## Architecture
- 分层和依赖约束以 `DESIGN.md` 和 `docs/design-docs/` 里的文档为准。
- 如果有 `docs/design-docs/layer-mapping.md`，先看它。

## Validation
- 改完代码后，先执行真实验证命令，再汇报结果。
- 如果验证失败，先看日志、测试输出和栈追踪，再决定下一步。

## Working Rule
- 先通过这个索引定位需要阅读的文档，只加载当前任务相关内容。

## Index Maintenance
- 新增 `docs/design-docs/*.md` 时，必须同步更新 `docs/design-docs/index.md`
- 新增 `docs/references/*.md` 时，必须同步更新 `docs/references/index.md`
- 新增计划文档时，放入 `docs/exec-plans/active/`，完成后移至 `docs/exec-plans/completed/`

**可选：pre-commit hook（防止忘记更新索引）**

在项目根目录创建 `.git/hooks/pre-commit`（或使用 pre-commit 配置工具）：

```bash
#!/bin/bash
# 检查新增的 docs 文件是否已在 index.md 中注册

NEW_DOCS=$(git diff --cached --name-only --diff-filter=A | grep '^docs/.*\.md$' | grep -v index.md || true)

if [ -n "$NEW_DOCS" ]; then
    echo "WARNING: 新增了以下文档文件，请确保已更新对应的 index.md："
    echo "$NEW_DOCS"
    echo ""
    echo "提交前请检查并更新索引文件，或者使用 --no-verify 跳过此检查。"
    # 取消注释以下行以强制阻止提交
    # exit 1
fi
```
