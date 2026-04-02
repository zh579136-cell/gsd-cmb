---
name: gsd-map-codebase
description: 用于既有系统分析，在接手老项目、做新功能前或重构排障前梳理代码结构、模块边界、依赖、约定和风险；若识别到 Java 后端接口层，则额外输出 FEATURE_TREE.md。
---

# gsd-map-codebase

## 作用

用于既有系统分析，帮助内网 agent 在规划或改造前建立一份可复用的代码库地图。

重点关注：

- 架构与目录结构
- 核心模块与边界
- 主要技术栈与外部依赖
- 编码约定与测试方式
- 风险点、脆弱区与历史包袱
- 后端接口暴露面

## 适用场景

- 接手陌生代码库
- 在老系统上做新需求前需要补背景
- 重构、改造、排障前需要建立全局理解

## 不适用场景

- 新项目还没有实际代码
- 代码量极小、结构一眼可见
- 只是一次单文件小修

## 输入要求

至少需要：

- 代码仓库根目录
- 当前关注的业务范围或模块
- 是否存在已知问题区域

## 输出要求

默认输出为一份 `CODEBASE_MAP.md`，至少包含：

- 项目概览
- 技术栈
- 目录与模块结构
- 关键流程和调用链
- 约定与测试方式
- 风险与建议关注点

当识别为 Java 后端项目且存在接口层时，额外输出：

- `FEATURE_TREE.md`

`FEATURE_TREE.md` 的定位是后端接口索引文档，不重复承担架构分析职责。

## 建议读取的状态/模板文件

- `templates/CODEBASE_MAP.md`
- `templates/FEATURE_TREE.md`
- `.planning/PROJECT.md`
- `.planning/STATE.md`

## 工作步骤

### 1. 识别扫描范围

先明确本次建图是：

- 全库分析
- 子系统分析
- 某个模块链路分析

### 2. 判断是否需要生成 `FEATURE_TREE.md`

只有满足后端特征时，才生成 `FEATURE_TREE.md`。

建议使用以下判断标准：

- 存在 `pom.xml` / `build.gradle` / `build.gradle.kts`
- 存在 `src/main/java` 或 `src/main/kotlin`
- 存在 Spring Web 接口层特征，例如：
  - `@RestController`
  - `@Controller`
  - `@RequestMapping`
  - `@GetMapping`
  - `@PostMapping`
  - `@PutMapping`
  - `@DeleteMapping`
  - `@PatchMapping`

如果只是：

- 纯前端项目
- Java 工具库
- 无 Web 接口层的后端基础库

则不要生成 `FEATURE_TREE.md`，并在结果中明确说明未检测到后端接口层。

### 3. 收集结构信息

梳理：

- 根目录结构
- 入口模块
- 核心目录职责
- 关键依赖与基础设施

### 4. 收集工程约定

重点看：

- 命名方式
- 分层风格
- 错误处理方式
- 配置管理方式
- 测试组织方式

### 5. 收集业务与风险信息

重点定位：

- 高耦合模块
- 历史包袱
- 大文件和脆弱逻辑
- 外部依赖点
- 可能影响后续 phase 的隐性风险

### 6. 生成 `FEATURE_TREE.md`（仅后端项目）

当判定为 Java 后端项目时，按以下优先级生成 `FEATURE_TREE.md`：

#### 扫描来源优先级

1. Java Controller
2. OpenAPI / Swagger / yaml 契约文件

常见契约文件候选：

- `openapi.yaml`
- `openapi.yml`
- `swagger.yaml`
- `swagger.yml`
- `api-contract.yaml`

#### Controller 解析规则

- 解析类级路径，例如 `@RequestMapping("/users")`
- 解析方法级路径，例如 `@GetMapping("/{id}")`
- 组合类级与方法级路径得到完整接口
- 提取 HTTP 方法、完整端点和描述

#### 描述提取规则

按以下顺序回退：

1. OpenAPI / Swagger 的 `summary` 或 `description`
2. Java 注解中的说明，例如 `@Operation(summary = "...")`
3. 根据方法名或控制器职责生成简短中文描述

#### 分组规则

- 优先按 URL 前缀聚类，例如 `/api/users/*` -> `Users`
- 若 URL 前缀不稳定，可按明确的 Controller 业务职责分组
- 分组标题应稳定、简洁，不要直接把原始类名堆出来

#### 输出边界

`FEATURE_TREE.md` 只记录：

- 接口方法
- 端点
- 描述
- 来源

不要把 Service、Repository、数据库表、内部实现细节重新塞进 `FEATURE_TREE.md`。

#### 生成方式

默认由技能按规则直接生成。

如果项目已经提供脚本或后续补充脚本，优先使用固定命令重生成，例如：

`python3 scripts/feature-tree-generator.py --save`

文档头部应保留 `update_policy`，并提醒不要手动编辑自动生成的接口表。

### 7. 输出代码库地图与接口索引

输出要能支持后续：

- `gsd-discuss-phase`
- `gsd-plan-phase`
- `gsd-debug`

如果生成了 `FEATURE_TREE.md`，要让后续流程把它当成接口边界和影响面索引使用。

## 约束与注意事项

- 不要只做文件列表，要总结模块关系和工程规律
- 不要泛泛而谈，要写可执行的建议
- 风险项要说明影响面和可能后果
- 如果只聚焦某一子系统，必须明确写出“本次未覆盖的区域”
- `CODEBASE_MAP.md` 负责项目级结构、约定和风险；`FEATURE_TREE.md` 只负责后端接口索引
- 若存在 OpenAPI 契约，描述优先用契约补全；但端点来源仍应优先参考源码 Controller
- 若检测到 Java 工程但没有接口层，要明确说明“不生成 FEATURE_TREE.md 的原因”

## 与其他 skills 的衔接关系

- 建图完成后，通常进入 `gsd-discuss-phase` 或 `gsd-plan-phase`
- 若是在排障前使用，后续进入 `gsd-debug`
- 对后端项目，`FEATURE_TREE.md` 应作为后续 discuss / plan / verify 的接口边界参考
