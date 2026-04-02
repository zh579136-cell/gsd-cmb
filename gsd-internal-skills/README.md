# GSD Internal Skills

这是一个面向内网 agent 的 GSD 精简迁移版目录。

它不是原版 Get Shit Done 仓库的镜像，也不是完整安装包，更不是多 runtime 适配层。这里保留的是最适合 skills 化落地的核心方法论：需求澄清、代码库建图、phase 规划、phase 执行、验证回流、排障，以及小任务快速处理。

## 这个目录和原版 GSD 的关系

- 来源：基于原版 GSD 的 `commands / workflows / agents / templates / references / state` 思路整理而成。
- 目标：把原版最有价值的工作流和结构化文件沉淀为内网 agent 可直接使用的 skills。
- 取舍：保留方法论主干，不保留安装器、hooks、多 runtime 绑定、社区和发布外围能力。
- 重写原则：尽量保持原版命名体系，但内容更适合内网协作、项目接手和持续维护。

## 为什么做裁剪

原版 GSD 很完整，但对内网 agent 落地来说，完整复刻会引入大量非必要复杂度：

- 不需要安装器和 runtime 分发
- 不需要工作区管理、多仓编排、社区和更新功能
- 不需要把每个子角色都暴露成公开 skill
- 更需要稳定的粗粒度流程入口和统一的状态文件结构

因此，本目录只保留第一版最值得落地的 9 个核心 skills，并给出一套足够轻量但可执行的模板体系。

## 当前保留的 skills

### 1. `gsd`

总入口与路由 skill。负责判断当前请求应走哪个子 skill，并给出从模糊需求到执行验证的推荐路径。

### 2. `gsd-new-project`

用于新项目或新需求初始化。负责沉淀项目目标、范围、约束、需求与 roadmap。

### 3. `gsd-map-codebase`

用于既有系统分析。负责梳理代码结构、模块边界、约定、测试方式、风险和历史包袱，为后续 planning 提供背景。对于 Java 后端项目，还会额外生成接口索引 `FEATURE_TREE.md`。

### 4. `gsd-discuss-phase`

用于某个 phase 的边界澄清和决策锁定。适合在规划前先把灰区、约束、参考资料和偏好固定下来。

### 5. `gsd-plan-phase`

用于研究、规划、任务拆分、依赖分析和验收标准定义。它是整个迁移版体系的中枢。

### 6. `gsd-execute-phase`

用于按计划执行一个 phase，记录执行日志、变更结果、偏差说明、未完成项和交接信息。

### 7. `gsd-verify-work`

用于执行自动验证、人工验收引导、问题记录和返工建议，形成验证闭环。

### 8. `gsd-debug`

用于系统化排障。按“症状 -> 假设 -> 验证 -> 根因 -> 修复建议”的方式处理问题。

### 9. `gsd-fast`

用于快速处理小改动、小缺陷、小范围调整。尽量不走完整 phase，但仍保留基本的记录和校验意识。

## 推荐工作流

### 场景一：新项目或新需求初始化

1. 使用 `gsd-new-project`
2. 如果是既有仓库，再补 `gsd-map-codebase`
3. 进入 `gsd-discuss-phase`
4. 再用 `gsd-plan-phase`
5. 然后 `gsd-execute-phase`
6. 最后 `gsd-verify-work`

### 场景二：接手既有系统

1. 先用 `gsd-map-codebase`
2. 如果需要新增 phase，补 `gsd-discuss-phase`
3. 再用 `gsd-plan-phase`
4. 执行时走 `gsd-execute-phase`
5. 收尾走 `gsd-verify-work`

### 场景三：线上问题或缺陷处理

1. 不清楚根因时先用 `gsd-debug`
2. 修复范围很小可直接走 `gsd-fast`
3. 修复范围较大时转 `gsd-plan-phase` -> `gsd-execute-phase` -> `gsd-verify-work`

## 在内网 agent skills 目录中的使用建议

建议把 `skills/` 目录整体接入到内网 agent 的 skills 根目录中，并保留 `templates/`、`examples/` 作为公共参考资产。

推荐使用方式：

- 用户请求先进入 `gsd`
- `gsd` 负责做场景识别和路由
- 具体执行时进入对应的 `gsd-*` 子 skill
- 每个子 skill 都优先读取 `.planning/` 中已有状态文件
- 没有状态文件时，按 `templates/` 中模板补齐

## 建议维护的状态文件

建议以 `.planning/` 为统一工作目录，至少保留以下文件：

- `PROJECT.md`：项目定义、核心价值、约束、关键决策
- `REQUIREMENTS.md`：当前需求、非目标、验收范围
- `ROADMAP.md`：phase 切分、顺序、目标、依赖
- `STATE.md`：当前进度、阻塞项、最近结论、下一步
- `CONTEXT.md`：某个 phase 的补充决策和上下文
- `PLAN.md`：实施计划
- `TASKS.md`：执行拆解与状态
- `VERIFY.md`：验证结论、问题和返工建议
- `CODEBASE_MAP.md`：既有系统地图
- `FEATURE_TREE.md`：后端服务项目的接口索引补充文件

## 原版 GSD 名称与当前目录的对应关系

| 原版 GSD | 当前目录 |
|---|---|
| `new-project` | `skills/gsd-new-project/` |
| `map-codebase` | `skills/gsd-map-codebase/` |
| `discuss-phase` | `skills/gsd-discuss-phase/` |
| `plan-phase` | `skills/gsd-plan-phase/` |
| `execute-phase` | `skills/gsd-execute-phase/` |
| `verify-work` | `skills/gsd-verify-work/` |
| `debug` | `skills/gsd-debug/` |
| `quick` + `fast` | `skills/gsd-fast/` |
| `next` + `help` 的路由职责 | `skills/gsd/` |

## 当前没有保留的原版能力

第一版没有独立迁移以下能力：

- `new-workspace / list-workspaces / remove-workspace`
- `ship / pr-branch`
- `manager / workstreams`
- `join-discord / update`
- `ui-phase` 独立 skill
- `review` 独立 skill
- `autonomous` 独立 skill

原因见 [MIGRATION_NOTES.md](/Users/hzde/Documents/GitHub/gsd-cmb/gsd-internal-skills/MIGRATION_NOTES.md) 和 [KEEP_DROP_REPORT.md](/Users/hzde/Documents/GitHub/gsd-cmb/gsd-internal-skills/KEEP_DROP_REPORT.md)。

## 目录结构

```text
gsd-internal-skills/
  README.md
  MIGRATION_NOTES.md
  KEEP_DROP_REPORT.md
  skills/
    gsd/
    gsd-new-project/
    gsd-map-codebase/
    gsd-discuss-phase/
    gsd-plan-phase/
    gsd-execute-phase/
    gsd-verify-work/
    gsd-debug/
    gsd-fast/
  templates/
  examples/
```

## 使用建议

- 把它当成内网 agent 的初始版本，而不是最终版本
- 先跑通主链路，再扩展 UI、review、多工作区等外围能力
- 优先保证模板字段稳定，不要频繁改动状态文件结构
- 如果后续要增强，优先补 `gsd-plan-phase`、`gsd-verify-work` 和 `gsd-map-codebase`
