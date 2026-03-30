# Migration Notes

## 迁移目标

本次迁移的目标不是部署完整 GSD，而是抽取最适合内网 agent 的方法论和 skill 结构，形成一个可直接接入内网环境的初版 skills 目录。

迁移时遵循以下原则：

- 保留原版 GSD 的命名体系
- 优先保留粗粒度流程 skill
- 优先保留 phase-driven、spec-driven、verify-driven 能力
- 不复刻安装器、多 runtime 绑定、发布与社区外围
- 模板和状态文件优先稳定、可读、可维护

## 哪些内容来自原版 GSD

以下内容直接继承或强参考了原版 GSD：

- `new-project` 的项目初始化骨架
- `map-codebase` 的既有系统分析思路
- `discuss-phase` 的 phase 讨论与上下文锁定机制
- `plan-phase` 的研究、规划、校验闭环
- `execute-phase` 的“按计划执行 + 记录偏差”思路
- `verify-work` 的验证与问题回流机制
- `debug` 的系统化排障思路
- `quick / fast` 的小任务快速路径
- `.planning/` 目录下的项目状态文件体系

## 哪些内容被重写了

以下部分不是原文照搬，而是面向内网场景重新组织：

### 1. skill 文案与结构

原版 GSD 的 prompt 主要服务于 Claude Code / Codex / OpenCode 等运行时命令入口。这里统一重写为内网 agent 可直接读取的 `SKILL.md`。

### 2. 状态文件模板

原版 GSD 的模板较多、粒度较细，且与 CLI 工具有较强耦合。本目录把状态文件缩减为：

- `PROJECT.md`
- `REQUIREMENTS.md`
- `ROADMAP.md`
- `STATE.md`
- `CONTEXT.md`
- `PLAN.md`
- `TASKS.md`
- `VERIFY.md`
- `CODEBASE_MAP.md`

目标是让内网 agent 和人工协作者都能稳定理解与维护。

### 3. 路由入口

原版通过多个 command 和 `/gsd:next` 驱动。这里改为 `gsd` 作为总入口 skill，在内部做路由判断和建议。

### 4. `quick` 与 `fast`

原版两者定位接近，但对内网落地来说区分成本偏高，因此合并为 `gsd-fast` 一个统一入口。

## 哪些内容被裁剪了

### 已裁剪

- 安装器与 runtime 绑定
- hooks 体系
- 多语言文档
- 社区与升级能力
- 多 workspace / 多 repo 管理
- PR / ship / 发布类命令
- manager / workstreams 管理视角

### 裁剪原因

- 与 skill 化落地关系不大
- 会显著增加目录复杂度
- 会稀释第一版的主链路质量
- 很多能力更适合在内网平台层实现，而不是 skill 层实现

## 哪些内容暂未保留

以下能力不是完全否定，而是暂缓进入第一版：

- `ui-phase`
- `ui-review`
- `review`
- `autonomous`
- `forensics`

原因：

- 第一版先聚焦主链路
- 这些能力依赖更强的上下文或更细的组织方式
- 后续可以在现有 skills 之上作为增强包补入

## 如果后续要增强，建议从原仓库哪些区域继续补

### 第一优先级

- [`get-shit-done-main/get-shit-done/workflows/plan-phase.md`](/Users/hzde/Documents/GitHub/gsd-cmb/get-shit-done-main/get-shit-done/workflows/plan-phase.md)
- [`get-shit-done-main/agents/gsd-planner.md`](/Users/hzde/Documents/GitHub/gsd-cmb/get-shit-done-main/agents/gsd-planner.md)
- [`get-shit-done-main/get-shit-done/workflows/verify-work.md`](/Users/hzde/Documents/GitHub/gsd-cmb/get-shit-done-main/get-shit-done/workflows/verify-work.md)
- [`get-shit-done-main/agents/gsd-verifier.md`](/Users/hzde/Documents/GitHub/gsd-cmb/get-shit-done-main/agents/gsd-verifier.md)

用途：增强规划质量、验收闭环和返工建议。

### 第二优先级

- [`get-shit-done-main/get-shit-done/workflows/map-codebase.md`](/Users/hzde/Documents/GitHub/gsd-cmb/get-shit-done-main/get-shit-done/workflows/map-codebase.md)
- [`get-shit-done-main/agents/gsd-codebase-mapper.md`](/Users/hzde/Documents/GitHub/gsd-cmb/get-shit-done-main/agents/gsd-codebase-mapper.md)
- [`get-shit-done-main/get-shit-done/templates/codebase/`](/Users/hzde/Documents/GitHub/gsd-cmb/get-shit-done-main/get-shit-done/templates/codebase)

用途：增强既有系统分析产物的质量与稳定性。

### 第三优先级

- [`get-shit-done-main/get-shit-done/references/checkpoints.md`](/Users/hzde/Documents/GitHub/gsd-cmb/get-shit-done-main/get-shit-done/references/checkpoints.md)
- [`get-shit-done-main/get-shit-done/references/verification-patterns.md`](/Users/hzde/Documents/GitHub/gsd-cmb/get-shit-done-main/get-shit-done/references/verification-patterns.md)
- [`get-shit-done-main/get-shit-done/references/questioning.md`](/Users/hzde/Documents/GitHub/gsd-cmb/get-shit-done-main/get-shit-done/references/questioning.md)

用途：增强人机协作细节、验收质量和提问质量。

## 当前版本的边界判断

这个目录已经能作为“内网 agent 初始版 skills 包”使用，但它不是完整平台。

它适合：

- 既有系统分析
- 新项目初始化
- phase 讨论与规划
- phase 执行与验证
- 问题排查
- 快速处理小改动

它暂时不负责：

- 安装与运行时适配
- 自动分发到不同 agent 运行环境
- 全套审计和多人工作区管理
- 发布流和 PR 自动化

## 建议的演进方向

1. 先让内网 agent 跑通主链路
2. 在真实项目中稳定模板格式
3. 再补 UI、review、autonomous 等增强能力
4. 最后才考虑更复杂的 workspace / ship / manager 能力
