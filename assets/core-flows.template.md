# Core Flows

## What This File Is For
- 写项目里真正重要的调用链路。
- 不求全，只写最常见、最值钱、最容易出问题的主链路。

## Main Modules

| Module | Role | In Main Path | Notes |
| --- | --- | --- | --- |
| `<module>` | `<这个模块负责什么>` | `<yes / no>` | `<补充说明>` |

## Core Flow 1

### Trigger
- `<这个链路从哪里进入>`

### Path
1. `<入口模块 / 类 / 接口>`
2. `<中间模块 / 服务>`
3. `<关键存储 / 表 / 外部依赖>`
4. `<返回或后续处理>`

### Key Objects
- `<领域对象 / DTO / 表 / 索引 / 消息体>`

### Branches
- `<常见分叉点>`

### Where Problems Usually Show Up
- `<这个链路最常见的问题点>`

### What Changes Are Risky
- `<改这里通常会牵连什么>`

## Core Flow 2
- `<如果还有第二条主链路，按上面的格式继续写>`

## Notes
- `<补充说明>`
