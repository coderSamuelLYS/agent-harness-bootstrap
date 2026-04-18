# Module Validation

## What This File Is For
- 写核心模块最常用的验证方式。
- 不求列全仓库所有命令，优先写最常改、最常出问题的模块。

## Modules

| Module | Role | Common Changes | Validation Command | Preconditions | High-Risk Dependencies | Check First When It Fails |
| --- | --- | --- | --- | --- | --- | --- |
| **[示例] API Gateway** | 外部请求入口、路由转发 | 路由规则、限流配置 | `pytest tests/gateway/ -v` | 服务需启动 | 用户服务、配置中心 | 检查路由配置文件、查看网关日志 |
| `<module>` | `<作用>` | `<常见改动类型>` | `<命令>` | `<前置条件>` | `<容易联动的模块>` | `<失败先看哪里>` |

> **注意：** 上方示例行仅供参考，初始化完成后请删除示例行，只保留真实的模块验证信息。

## Validation Notes
- `<补充说明>`
