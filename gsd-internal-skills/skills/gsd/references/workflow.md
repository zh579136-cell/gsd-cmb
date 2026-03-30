# 推荐工作流

## 总体原则

内网版 GSD 建议遵循“先理解，再收敛，再规划，再执行，再验证”的顺序，不鼓励直接跳过上下文进入实现。

推荐主链路：

1. `gsd-new-project` 或 `gsd-map-codebase`
2. `gsd-discuss-phase`
3. `gsd-plan-phase`
4. `gsd-execute-phase`
5. `gsd-verify-work`

补充链路：

- 问题定位：`gsd-debug`
- 小任务快修：`gsd-fast`

## 场景一：新项目

1. 用 `gsd-new-project` 写清楚项目目标、需求、roadmap
2. 如果项目很快就进入具体 phase，立即补 `gsd-discuss-phase`
3. 用 `gsd-plan-phase` 把 phase 拆成可执行任务
4. 用 `gsd-execute-phase` 落地
5. 用 `gsd-verify-work` 做验证与回流

## 场景二：既有系统

1. 先用 `gsd-map-codebase` 形成项目地图
2. 再用 `gsd-discuss-phase` 锁定当前 phase 的范围和约束
3. 用 `gsd-plan-phase` 生成实施计划
4. 用 `gsd-execute-phase` 执行
5. 用 `gsd-verify-work` 验证

## 场景三：线上问题

1. 先用 `gsd-debug` 收集症状与根因
2. 根因很小、修复范围很清楚时转 `gsd-fast`
3. 根因明确但改动较大时转 `gsd-plan-phase`
4. 修复完成后用 `gsd-verify-work`

## 场景四：小改动

1. 先判断是否满足 `gsd-fast` 条件
2. 如果超出轻量阈值，立即升级为 `gsd-plan-phase`
3. 如果走了 `gsd-fast`，也应补最小变更记录和基础验证
