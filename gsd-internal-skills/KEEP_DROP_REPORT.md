# Keep / Drop Report

## 说明

本报告按“原始来源 -> 当前动作 -> 当前去向 -> 原因 -> 是否属于第一版保留范围”进行整理。

| 原始来源 | 当前动作 | 当前去向 | 原因 | 第一版保留 |
|---|---|---|---|---|
| `commands/gsd/new-project.md` | 保留并重写 | `skills/gsd-new-project/SKILL.md` | 新项目初始化是主链路入口 | 是 |
| `workflows/new-project.md` | 保留并重写 | `skills/gsd-new-project/SKILL.md` | 提供 questioning -> requirements -> roadmap 主流程 | 是 |
| `agents/gsd-project-researcher.md` | 保留为内嵌思路 | `skills/gsd-new-project/SKILL.md` | 作为研究角色，不单独暴露 skill | 是 |
| `agents/gsd-roadmapper.md` | 保留为内嵌思路 | `skills/gsd-new-project/SKILL.md` | 作为 roadmap 生成职责 | 是 |
| `commands/gsd/map-codebase.md` | 保留并重写 | `skills/gsd-map-codebase/SKILL.md` | 既有系统分析价值高 | 是 |
| `workflows/map-codebase.md` | 保留并重写 | `skills/gsd-map-codebase/SKILL.md` | 定义结构化建图输出 | 是 |
| `agents/gsd-codebase-mapper.md` | 保留为内嵌思路 | `skills/gsd-map-codebase/SKILL.md` | 保留角色，不单独公开 | 是 |
| `templates/codebase/*` | 合并重写 | `templates/CODEBASE_MAP.md` | 第一版不拆 7 份文件，先做统一模板 | 是 |
| `commands/gsd/discuss-phase.md` | 保留并重写 | `skills/gsd-discuss-phase/SKILL.md` | phase 约束澄清是主链路必需 | 是 |
| `workflows/discuss-phase.md` | 保留并重写 | `skills/gsd-discuss-phase/SKILL.md` | 保留灰区识别和决策锁定思路 | 是 |
| `workflows/discuss-phase-assumptions.md` 或 assumptions 模式 | 合并 | `skills/gsd-discuss-phase/SKILL.md` | 不单独暴露，作为模式保留 | 是 |
| `agents/gsd-assumptions-analyzer.md` | 保留为内嵌思路 | `skills/gsd-discuss-phase/SKILL.md` | 仅保留思路，不单独出 skill | 否 |
| `commands/gsd/plan-phase.md` | 保留并重写 | `skills/gsd-plan-phase/SKILL.md` | 规划是整个体系中枢 | 是 |
| `workflows/plan-phase.md` | 保留并重写 | `skills/gsd-plan-phase/SKILL.md` | 保留 research -> plan -> verify 流程 | 是 |
| `commands/gsd/research-phase.md` | 合并 | `skills/gsd-plan-phase/SKILL.md` | 研究是规划前的模式，不单列 | 是 |
| `agents/gsd-phase-researcher.md` | 保留为内嵌思路 | `skills/gsd-plan-phase/SKILL.md` | 保留角色职责 | 是 |
| `agents/gsd-planner.md` | 保留为内嵌思路 | `skills/gsd-plan-phase/SKILL.md` | 保留拆分规则与质量标准 | 是 |
| `agents/gsd-plan-checker.md` | 保留为内嵌思路 | `skills/gsd-plan-phase/SKILL.md` | 作为计划自检和校验规则 | 是 |
| `templates/phase-prompt.md` | 重写 | `templates/PLAN.md` | 调整为更适合内网 agent 的格式 | 是 |
| `commands/gsd/execute-phase.md` | 保留并重写 | `skills/gsd-execute-phase/SKILL.md` | 执行闭环必需 | 是 |
| `workflows/execute-phase.md` | 保留并重写 | `skills/gsd-execute-phase/SKILL.md` | 保留分波次、偏差处理、记录机制 | 是 |
| `agents/gsd-executor.md` | 保留为内嵌思路 | `skills/gsd-execute-phase/SKILL.md` | 不单独对外暴露 | 是 |
| `templates/summary*.md` | 合并重写 | `templates/TASKS.md` 和 `templates/VERIFY.md` | 第一版压缩模板数量 | 是 |
| `commands/gsd/verify-work.md` | 保留并重写 | `skills/gsd-verify-work/SKILL.md` | 验证与返工闭环必需 | 是 |
| `workflows/verify-work.md` | 保留并重写 | `skills/gsd-verify-work/SKILL.md` | 保留 UAT 与 gaps 回流 | 是 |
| `agents/gsd-verifier.md` | 保留为内嵌思路 | `skills/gsd-verify-work/SKILL.md` | 验证角色保留但不独立公开 | 是 |
| `templates/UAT.md` | 重写合并 | `templates/VERIFY.md` | 第一版统一验证记录 | 是 |
| `commands/gsd/debug.md` | 保留并重写 | `skills/gsd-debug/SKILL.md` | 排障高频且方法论成熟 | 是 |
| `agents/gsd-debugger.md` | 保留为内嵌思路 | `skills/gsd-debug/SKILL.md` | 作为排障角色说明 | 是 |
| `templates/DEBUG.md` | 暂不单独保留 | 暂无 | 第一版先在 skill 中定义记录方式 | 否 |
| `commands/gsd/quick.md` | 合并 | `skills/gsd-fast/SKILL.md` | 与 fast 能力重叠 | 是 |
| `workflows/quick.md` | 合并 | `skills/gsd-fast/SKILL.md` | 保留轻量规划思路 | 是 |
| `workflows/fast.md` | 保留并重写 | `skills/gsd-fast/SKILL.md` | 小任务快速处理必需 | 是 |
| `commands/gsd/help.md` | 合并 | `skills/gsd/SKILL.md` | 由总入口承担说明职责 | 是 |
| `commands/gsd/next.md` 或 `workflows/next.md` | 合并 | `skills/gsd/SKILL.md` | 由总入口承担路由职责 | 是 |
| `references/checkpoints.md` | 重写保留 | `skills/gsd/references/workflow.md` 等 | 保留 checkpoint 思想 | 是 |
| `references/verification-patterns.md` | 重写保留 | `skills/gsd-verify-work/SKILL.md` 与模板 | 保留验证思路 | 是 |
| `references/questioning.md` | 重写保留 | `skills/gsd-new-project/SKILL.md` | 保留提问与需求抽取思路 | 是 |
| `templates/project.md` | 重写 | `templates/PROJECT.md` | 保留核心字段，弱化 CLI 依赖 | 是 |
| `templates/requirements.md` | 重写 | `templates/REQUIREMENTS.md` | 保留范围与验收结构 | 是 |
| `templates/roadmap.md` | 重写 | `templates/ROADMAP.md` | 保留 phase 化结构 | 是 |
| `templates/state.md` | 重写 | `templates/STATE.md` | 保留项目状态总览 | 是 |
| `bin/lib/init.cjs` | 保留为参考，不迁移实现 | 文档和模板结构中吸收 | 只吸收 init 聚合思路 | 是 |
| `bin/lib/state.cjs` | 保留为参考，不迁移实现 | 文档和模板结构中吸收 | 只吸收 STATE 结构 | 是 |
| `bin/lib/phase.cjs` | 保留为参考，不迁移实现 | 文档和模板结构中吸收 | 只吸收 phase 编号与组织方式 | 是 |
| `bin/lib/verify.cjs` | 保留为参考，不迁移实现 | 文档和模板结构中吸收 | 只吸收验证规则 | 是 |
| `bin/lib/config.cjs` | 保留为参考，不迁移实现 | 文档和模板结构中吸收 | 只吸收配置维度，不复制 CLI | 否 |
| `commands/gsd/new-workspace.md` | 删除 | 无 | 非第一版核心 | 否 |
| `commands/gsd/list-workspaces.md` | 删除 | 无 | 非第一版核心 | 否 |
| `commands/gsd/remove-workspace.md` | 删除 | 无 | 非第一版核心 | 否 |
| `commands/gsd/ship.md` | 删除 | 无 | PR/发版不属于 skill 核心 | 否 |
| `commands/gsd/pr-branch.md` | 删除 | 无 | Git 外围能力 | 否 |
| `commands/gsd/manager.md` | 删除 | 无 | 复杂度高，非第一版 | 否 |
| `commands/gsd/workstreams.md` | 删除 | 无 | 复杂度高，非第一版 | 否 |
| `commands/gsd/join-discord.md` | 删除 | 无 | 社区外围 | 否 |
| `commands/gsd/update.md` | 删除 | 无 | 安装更新外围 | 否 |
| `commands/gsd/ui-phase.md` | 暂缓 | 无 | 后续可做增强 skill | 否 |
| `commands/gsd/ui-review.md` | 暂缓 | 无 | 第一版并入验证思路 | 否 |
| `commands/gsd/review.md` | 暂缓 | 无 | 属于增强能力 | 否 |
| `commands/gsd/autonomous.md` | 暂缓 | 无 | 先不做自动推进 | 否 |
| `commands/gsd/forensics.md` | 暂缓 | 无 | 先由 debug 覆盖 | 否 |

## 第一版最终公开 skill 清单

- `gsd`
- `gsd-new-project`
- `gsd-map-codebase`
- `gsd-discuss-phase`
- `gsd-plan-phase`
- `gsd-execute-phase`
- `gsd-verify-work`
- `gsd-debug`
- `gsd-fast`
