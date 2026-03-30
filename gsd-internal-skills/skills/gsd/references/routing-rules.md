# 路由规则

## 路由判断优先级

### 1. 先判断任务阶段

- 不知道做什么：总入口继续追问
- 知道目标但没结构：`gsd-new-project`
- 有代码但没全局理解：`gsd-map-codebase`
- 有 phase 但边界不清：`gsd-discuss-phase`
- 边界清晰但没计划：`gsd-plan-phase`
- 有计划要落地：`gsd-execute-phase`
- 已做完待确认：`gsd-verify-work`
- 问题原因未知：`gsd-debug`
- 明显是小任务：`gsd-fast`

### 2. 再判断资料是否缺失

缺少项目级上下文：
- 走 `gsd-new-project`

缺少代码级背景：
- 走 `gsd-map-codebase`

缺少 phase 决策：
- 走 `gsd-discuss-phase`

缺少执行拆解：
- 走 `gsd-plan-phase`

### 3. 判断是否降级或升级

当用户说“就顺手改一下”时，也要检查是否真的适合 `gsd-fast`：

- 如果需要跨模块、多文件、大改动，升级到 `gsd-plan-phase`
- 如果需要先定位原因，先转 `gsd-debug`
- 如果已经执行结束但缺验证，不要继续执行，改走 `gsd-verify-work`

## 路由输出格式建议

总入口输出建议至少包含：

- 当前判断：这是哪一类任务
- 推荐 skill：具体 skill 名称
- 原因：为什么这么判断
- 先读文件：建议优先读哪些 `.planning/` 文件
- 下一步：执行完该 skill 后通常接什么
