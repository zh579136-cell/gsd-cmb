# 示例：使用 GSD Internal Skills 后的项目结构

下面是一个建议的 `.planning/` 组织方式。这个示例不是强制规范，但适合作为内网 agent 的初始约定。

```text
project-root/
  src/
  tests/
  .planning/
    PROJECT.md
    REQUIREMENTS.md
    ROADMAP.md
    STATE.md
    CODEBASE_MAP.md
    phases/
      phase-01-foundation/
        CONTEXT.md
        PLAN.md
        TASKS.md
        VERIFY.md
      phase-02-integration/
        CONTEXT.md
        PLAN.md
        TASKS.md
        VERIFY.md
      phase-03-hardening/
        CONTEXT.md
        PLAN.md
        TASKS.md
        VERIFY.md
```

## 文件职责说明

### 项目根级

- `PROJECT.md`
  - 描述项目是什么、为什么做、关键约束和核心价值

- `REQUIREMENTS.md`
  - 描述要交付什么、不交付什么、验收边界是什么

- `ROADMAP.md`
  - 把工作切成 phase，并说明 phase 之间的顺序和依赖

- `STATE.md`
  - 给任何接手的人一个最短路径：现在做到哪了、卡在哪、下一步是什么

- `CODEBASE_MAP.md`
  - 适合既有系统，用来沉淀架构、模块、约定、风险

### phase 级

- `CONTEXT.md`
  - 当前 phase 的边界、决策、参考资料和代码上下文

- `PLAN.md`
  - 当前 phase 的实施计划、任务分解和验收标准

- `TASKS.md`
  - 执行日志、偏差记录、阻塞项和未完成项

- `VERIFY.md`
  - 自动验证、人工验收和返工建议

## 推荐使用顺序

### 新项目

1. 用 `gsd-new-project` 生成根级四个核心文件
2. 进入具体 phase 前用 `gsd-discuss-phase` 生成 `CONTEXT.md`
3. 用 `gsd-plan-phase` 生成 `PLAN.md` 和 `TASKS.md`
4. 用 `gsd-execute-phase` 更新 `TASKS.md` 和 `STATE.md`
5. 用 `gsd-verify-work` 写 `VERIFY.md`

### 既有系统

1. 先用 `gsd-map-codebase` 生成 `CODEBASE_MAP.md`
2. 后续流程与新项目一致

## 一个最小的 phase 生命周期

```text
gsd-map-codebase
  -> gsd-discuss-phase
  -> gsd-plan-phase
  -> gsd-execute-phase
  -> gsd-verify-work
```

如果在执行或验证中发现问题：

```text
gsd-debug
  -> gsd-fast
  或
gsd-debug
  -> gsd-plan-phase
```

## 实践建议

- 不要一次生成过多 phase 目录，先生成当前正在做的 phase
- `STATE.md` 保持简洁，优先记录当前状态和下一步
- `TASKS.md` 不要只写“已完成”，要写清楚偏差和未完成项
- `VERIFY.md` 不要只有结论，要保留验证证据和后续建议
