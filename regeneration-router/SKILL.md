---
name: regeneration-router
description: >-
  Turn qc-report and consistency-report into a retry plan for failed or unstable manhua-drama shots,
  including keep vs patch vs redo decisions, revised prompt strategy, seed/reference handling,
  and batch-ready regeneration-brief output.
  Use after QC when generated shots need targeted repair instead of a full restart. 将质检结果转成可执行的返工计划并输出 regeneration-brief。
---

# Regeneration Router

漫剧制作流程中的返工调度环节。它把 `shot-qc-and-edit-assembler` 和 `consistency-keeper` 的问题清单，转成下一轮可执行的重生成方案，而不是让用户手工重新整理全部 prompt。

## 职责

- 读取 `qc-report` 和 `consistency-report`，决定每个问题镜头应该 keep、patch 还是 redo
- 为需要返工的镜头选择最合适的修复策略
- 基于已有 `generation-brief` 生成可执行的 prompt 修补方案
- 规划 seed、参考图、角色锁定和批次重跑方式
- 输出供用户或下一轮 Jimeng 生成使用的 `regeneration-brief`

## 不负责

- 初次编写生成 prompt -> `model-prompt-adapter-jimeng`
- 单镜头剧情和剪辑判断 -> `shot-qc-and-edit-assembler`
- 跨镜头一致性判断 -> `consistency-keeper`
- 实际执行生成

## 输入

| 字段 | 必需 | 来源 |
|---|---|---|
| qc-report | 是 | `shot-qc-and-edit-assembler` |
| generation-brief | 是 | `model-prompt-adapter-jimeng` |
| shot-plan | 是 | `storyboard-shot-planner` |
| asset-bible | 建议 | `script-asset-breakdown` |
| consistency-report | 建议 | `consistency-keeper` |

## 输出

使用 [`templates/regeneration-brief.md`](templates/regeneration-brief.md) 输出 `regeneration-brief`。

## 工作流程

### Step 1 - 归类问题

读取 [`references/regeneration-strategy-matrix.md`](references/regeneration-strategy-matrix.md)，把问题归类为:

- identity drift
- composition mismatch
- emotion mismatch
- technical defect
- motion failure
- continuity break

### Step 2 - 决定处理路径

对每个问题镜头先决定:

- **Keep**: 不重生，直接保留
- **Patch**: 小修，不改主结构
- **Partial Redo**: 只重做单镜头或单批次
- **Full Redo**: 重新规划该镜头的完整 prompt 和参数

### Step 3 - 修补 prompt

读取 [`references/prompt-repair-patterns.md`](references/prompt-repair-patterns.md)，基于原始 `generation-brief`:

- 增加缺失锚点
- 删除误导性描述
- 强化角色、服装、道具、构图约束
- 调整 seed / 参考图 / 生成模式

### Step 4 - 批次规划

把需要返工的镜头按修复逻辑重新分组:

- 同场景一致性问题 -> 同批处理
- 单镜头技术瑕疵 -> 独立处理
- 需要共享参考图或 seed 的镜头 -> 放入同组

### Step 5 - 输出 regeneration-brief

明确:

- 哪些镜头直接保留
- 哪些镜头只做后期修补
- 哪些镜头需要重生成
- 每个返工镜头的 prompt 修订说明、参数覆盖、优先级和批次分组
