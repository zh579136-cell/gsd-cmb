---
name: gsd
description: 作为总入口使用，在用户目标还不够明确时判断应该进入哪条工程子流程，例如新需求初始化、代码库分析、phase 规划、执行、验证、排障或快修。
---

# gsd

## 作用

`gsd` 是总入口，用于判断当前用户请求最适合走哪条工作流，并把请求路由到合适的子流程。它不负责替代所有子流程的细节执行，而负责：

- 识别当前处于哪种项目状态
- 判断用户现在需要的是分析、初始化、澄清、规划、执行、验证、排障还是快修
- 推荐下一步使用哪个 `gsd-*` 子流程
- 提醒应读取哪些状态文件

## 适用场景

- 用户只说了一个模糊目标，不知道先走哪一步
- 接手一个项目，但不确定应该先分析代码还是先写计划
- 已经有 `.planning/` 文件，但不确定该继续讨论、规划还是验证
- 用户描述了一个问题，需要判断是走 `gsd-debug` 还是 `gsd-fast`

## 不适用场景

- 用户已经明确要执行某个 phase 的规划或执行
- 用户已经点名要使用某个具体 `gsd-*` 子流程
- 任务已经非常明确，只需直接调用对应子 skill

## 输入要求

至少需要以下一种输入：

- 用户当前目标
- 当前项目上下文
- `.planning/` 中已有状态文件
- 当前代码库是否为新项目还是既有系统

## 输出要求

输出应包含：

- 当前判断的场景类型
- 推荐子流程
- 推荐先读取的文件
- 建议工作顺序
- 若需要补前置条件，要明确指出

## 建议读取的状态/模板文件

优先读取：

- `.planning/STATE.md`
- `.planning/PROJECT.md`
- `.planning/ROADMAP.md`
- `.planning/CONTEXT.md`
- `.planning/PLAN.md`
- `.planning/VERIFY.md`
- `.planning/CODEBASE_MAP.md`

若文件不存在，可参考：

- [`workflow.md`](/Users/hzde/Documents/GitHub/gsd-cmb/gsd-internal-skills/skills/gsd/references/workflow.md)
- [`routing-rules.md`](/Users/hzde/Documents/GitHub/gsd-cmb/gsd-internal-skills/skills/gsd/references/routing-rules.md)
- [`status-files.md`](/Users/hzde/Documents/GitHub/gsd-cmb/gsd-internal-skills/skills/gsd/references/status-files.md)

## 工作步骤

### 1. 判断当前对象

先判断当前更像哪种情况：

- 新项目 / 新需求
- 既有系统接手
- 某个 phase 待澄清
- 某个 phase 待规划
- 某个 phase 待执行
- 某个 phase 待验证
- 问题定位与排障
- 小任务快修

### 2. 判断当前资料完整度

检查是否已有以下信息：

- 项目目标和边界
- 当前 phase 是否已定义
- 是否已有上下文决策
- 是否已有执行计划
- 是否已有验证记录

### 3. 按路由规则推荐 skill

常用路由：

- 没有项目定义：`gsd-new-project`
- 是既有系统且缺背景图谱：`gsd-map-codebase`
- phase 边界不清：`gsd-discuss-phase`
- phase 已清晰但无计划：`gsd-plan-phase`
- 已有计划要落地：`gsd-execute-phase`
- 已执行完需要确认效果：`gsd-verify-work`
- 用户描述故障、异常、根因不明：`gsd-debug`
- 任务非常小、改动很轻：`gsd-fast`

### 4. 明确建议顺序

如果用户目标还比较模糊，优先按下面的顺序推荐：

1. `gsd-new-project` 或 `gsd-map-codebase`
2. `gsd-discuss-phase`
3. `gsd-plan-phase`
4. `gsd-execute-phase`
5. `gsd-verify-work`

### 5. 给出下一步动作

不要只说“建议使用某个 skill”，而要明确说明：

- 为什么推荐它
- 进入它之前该准备什么
- 执行后下一步通常接什么

## 常见场景路由表

| 用户请求 | 推荐 skill | 说明 |
|---|---|---|
| “我有个新需求，帮我梳理一下怎么做” | `gsd-new-project` | 先收敛目标、范围、约束 |
| “这个老系统我先想看清楚结构” | `gsd-map-codebase` | 先建图再规划 |
| “这个 phase 该怎么做还没想清楚” | `gsd-discuss-phase` | 先把灰区和决策锁住 |
| “这个 phase 已经明确了，帮我拆计划” | `gsd-plan-phase` | 研究、拆分、依赖分析 |
| “计划有了，开始落地” | `gsd-execute-phase` | 按任务执行并记录结果 |
| “做完了，帮我验收一下” | `gsd-verify-work` | 自动验证 + 人工确认 |
| “线上这个问题不知道根因” | `gsd-debug` | 先排障，不要盲修 |
| “只是改个文案/配置/小 bug” | `gsd-fast` | 轻量直达 |

## 约束与注意事项

- `gsd` 不应该抢子 skill 的工作
- 识别不清时，优先补最小必要上下文，不要直接跳执行
- 如果缺的是“代码库背景”，优先推荐 `gsd-map-codebase`
- 如果缺的是“实现边界和决策”，优先推荐 `gsd-discuss-phase`
- 如果缺的是“执行拆解”，优先推荐 `gsd-plan-phase`

## 与其他子流程的衔接关系

- `gsd` -> `gsd-new-project`
- `gsd` -> `gsd-map-codebase`
- `gsd` -> `gsd-discuss-phase`
- `gsd` -> `gsd-plan-phase`
- `gsd` -> `gsd-execute-phase`
- `gsd` -> `gsd-verify-work`
- `gsd` -> `gsd-debug`
- `gsd` -> `gsd-fast`
