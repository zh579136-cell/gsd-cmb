---
name: gsd-internal-skills
description: 用于内网研发场景的工程工作流技能，适合既有系统分析、新需求初始化、phase 澄清、phase 规划、执行、验证、排障和小任务快修。
---

# gsd

## 作用

这是一个面向内网研发场景的通用工程技能。

它用于把一项工作从“目标不清”推进到“可规划、可执行、可验证”的状态，并统一使用 `.planning/` 目录维护上下文、计划、执行记录和验证结果。

适合覆盖的场景：

- 新需求初始化
- 既有系统分析
- phase 边界澄清
- phase 规划
- phase 执行
- 验证与返工建议
- 排障
- 小任务快速处理

## 适用方式

把整个当前目录放到内网 agent 的全局 skills 根目录下即可：

```text
global-skills/
  gsd-internal-skills/
    SKILL.md
    skills/
    templates/
    examples/
```

## 内部结构

### `skills/`

这里是当前技能的内部子流程说明：

- `skills/gsd/`
- `skills/gsd-new-project/`
- `skills/gsd-map-codebase/`
- `skills/gsd-discuss-phase/`
- `skills/gsd-plan-phase/`
- `skills/gsd-execute-phase/`
- `skills/gsd-verify-work/`
- `skills/gsd-debug/`
- `skills/gsd-fast/`

当需要进入某一子流程时，应继续读取对应目录下的 `SKILL.md`。

### `templates/`

这里是公共模板库。执行任何阶段性工作时，都应优先复用这些模板，而不是临时自造文件结构。

### `examples/`

这里提供 `.planning/` 组织结构示例，帮助统一目录约定。

## 使用原则

### 原则 1：先判断场景，再进入子流程

收到请求后，先判断用户处于哪类场景，再读取对应内部文档：

- 新需求初始化
  - 读取 `skills/gsd-new-project/SKILL.md`
- 既有系统分析
  - 读取 `skills/gsd-map-codebase/SKILL.md`
- phase 澄清
  - 读取 `skills/gsd-discuss-phase/SKILL.md`
- phase 规划
  - 读取 `skills/gsd-plan-phase/SKILL.md`
- phase 执行
  - 读取 `skills/gsd-execute-phase/SKILL.md`
- 验证
  - 读取 `skills/gsd-verify-work/SKILL.md`
- 排障
  - 读取 `skills/gsd-debug/SKILL.md`
- 小改动
  - 读取 `skills/gsd-fast/SKILL.md`

### 原则 2：优先读模板，不要临时发挥

如果项目里还没有 `.planning/`，优先用下面模板初始化：

- `templates/PROJECT.md`
- `templates/REQUIREMENTS.md`
- `templates/ROADMAP.md`
- `templates/STATE.md`
- `templates/CONTEXT.md`
- `templates/PLAN.md`
- `templates/TASKS.md`
- `templates/VERIFY.md`
- `templates/CODEBASE_MAP.md`

### 原则 3：统一维护 `.planning/`

建议所有项目统一使用：

```text
.planning/
```

作为状态文件根目录。

## 推荐工作流

### 新需求

1. 进入 `skills/gsd-new-project/SKILL.md`
2. 初始化 `PROJECT.md`、`REQUIREMENTS.md`、`ROADMAP.md`、`STATE.md`
3. 进入 `skills/gsd-discuss-phase/SKILL.md`
4. 再进入 `skills/gsd-plan-phase/SKILL.md`
5. 然后进入 `skills/gsd-execute-phase/SKILL.md`
6. 最后进入 `skills/gsd-verify-work/SKILL.md`

### 既有系统

1. 进入 `skills/gsd-map-codebase/SKILL.md`
2. 产出 `CODEBASE_MAP.md`
3. 再按 discuss -> plan -> execute -> verify 顺序推进

### 问题处理

1. 进入 `skills/gsd-debug/SKILL.md`
2. 若问题小且根因清晰，转 `skills/gsd-fast/SKILL.md`
3. 若问题大或涉及结构调整，转 `skills/gsd-plan-phase/SKILL.md`

## 输入要求

至少应有以下信息之一：

- 用户当前目标
- 当前项目状态
- 代码仓库
- 已有 `.planning/` 文件

## 输出要求

输出应明确：

- 当前判断属于哪类场景
- 应读取哪个内部子流程文档
- 应生成或更新哪些 `.planning/` 文件
- 完成后下一步建议是什么

## 联动方式

在这个技能中，不依赖平台做 skill 间自动跳转。

联动方式是：

- 由当前入口判断场景
- 继续读取 `skills/*/SKILL.md`
- 共享同一套 `templates/*`
- 统一写入 `.planning/`

## 建议优先读取的文件

收到请求后，按优先级读取：

1. `skills/gsd/SKILL.md`
2. `skills/gsd/references/routing-rules.md`
3. `skills/gsd/references/status-files.md`
4. 对应场景的 `skills/gsd-*/SKILL.md`
5. 相关 `templates/*`
