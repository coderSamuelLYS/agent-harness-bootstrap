# CI & Validation Pipeline

## Build & Test Commands

| Phase | Command | Description | Run In |
| --- | --- | --- | --- |
| **[示例] Build** | `npm run build` | 编译 TypeScript / 构建 bundle | Local + CI |
| **[示例] Unit Test** | `npm test` | 运行单元测试 | Local + CI |
| **[示例] Integration Test** | `npm run test:integration` | 运行集成测试 | CI only |
| **[示例] Lint** | `npm run lint` | 代码风格检查 | Local + CI |
| **[示例] Type Check** | `npm run type-check` | TypeScript 类型检查 | Local + CI |
| `<phase>` | `<command>` | `<description>` | `<Local / CI / Both>` |

> **注意：** 上方示例行仅供参考，初始化完成后请删除示例行，只保留真实的验证命令。

## CI Stages

### Stage 1: Quick Validation
- **Purpose:** 快速验证基础正确性，快速反馈
- **Runs on:** Every push and PR
- **Steps:**
  1. `<step 1>`
  2. `<step 2>`
  3. `<step 3>`

### Stage 2: Full Validation
- **Purpose:** 完整的回归测试
- **Runs on:** PR to main branch
- **Steps:**
  1. `<step 1>`
  2. `<step 2>`
  3. `<step 3>`

### Stage 3: Release Validation
- **Purpose:** 发布前的完整验证
- **Runs on:** Release tag
- **Steps:**
  1. `<step 1>`
  2. `<step 2>`
  3. `<step 3>`

## Test Coverage

| Component | Target Coverage | Current Coverage | Owner |
| --- | --- | --- | --- |
| `<component>` | `<%>` | `<%>` | `<team/person>` |

## Quality Gates

- **All tests must pass** before merge
- **No new warnings** introduced
- **Code coverage** should not decrease below threshold
- **Security scans** should find no critical/high vulnerabilities

## Local Development Checklist

Before pushing code:
- [ ] Run local build: `<command>`
- [ ] Run unit tests: `<command>`
- [ ] Run lint: `<command>`
- [ ] Manual smoke test: `<steps>`

## Troubleshooting

### Common CI Failures

| Error Pattern | Common Cause | Fix |
| --- | --- | --- |
| **[示例] Timeout** | 测试运行超时 | 检查测试数据量，优化查询或增加超时时间 |
| **[示例] OOM** | 内存不足 | 减少并发测试数，或增加 CI runner 内存 |
| `<error>` | `<cause>` | `<fix>` |

> **注意：** 上方示例行仅供参考，初始化完成后请删除示例行，只保留真实的故障排查信息。

---

> **维护规则：**
> - 新增验证命令或 CI 阶段时，同步更新此文档
> - 定期更新覆盖率数据
> - 记录常见的 CI 失败模式和解决方法
