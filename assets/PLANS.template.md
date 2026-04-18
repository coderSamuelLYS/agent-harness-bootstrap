# PLANS

## Active Work
- <当前正在处理的任务>

## Next
- <下一步动作>

## Blockers
- <当前 blocker，没有则写 None>

## Validation Rule
- 在任何代码修改完成后，必须自主运行 `gradlew test` 或 `mvn test`。如果测试失败、编译报错或架构检查不通过，严禁直接向人类求助。必须自主读取终端的错误日志（LogQL/Stacktrace），分析原因并进行修复，直至测试 100% 绿灯，再向人类汇报。

## Blocker Handling
- 如果失败来自权限、网络、证书、缺失环境变量或外部依赖，先记录 blocker，再决定是否需要外部支持。
- blocker 记录应包含执行命令、失败摘要、关键日志和已尝试的修复。

## Active Plans
- `docs/exec-plans/active/`
