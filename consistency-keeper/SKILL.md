---
name: consistency-keeper
description: >-
  Check cross-shot and cross-scene visual consistency for manhua-drama production, including character identity,
  costume state, props, environments, and style stability, then output consistency-report.
  Use after AI images or clips are generated when a user needs to verify that the same character, outfit, prop,
  or location stays visually stable across a sequence. 检查跨镜头和跨场景的一致性并输出 consistency-report。
---

# Consistency Keeper

漫剧制作流程中的一致性检查环节。它不判断剧情对不对，也不负责初次写 prompt，而是专门检查 AI 多轮生成后最常见的问题: 人脸漂移、服装错乱、道具消失、场景不连贯、风格跳变。

## 职责

- 检查同一角色在连续镜头中的脸部、发型、体型、服装是否稳定
- 检查同一道具、场景、时间段在跨镜头中的连续性
- 检查画风、色调、材质感是否在同一序列内保持一致
- 标记哪些问题可以接受，哪些需要监控，哪些必须返工
- 输出供 `shot-qc-and-edit-assembler` 和 `regeneration-router` 消费的 `consistency-report`

## 不负责

- 单镜头是否符合剧情和分镜意图 -> `shot-qc-and-edit-assembler`
- 初次生成 Jimeng prompt -> `model-prompt-adapter-jimeng`
- 实际执行图像或视频生成
- 分镜设计或资产抽取

## 输入

| 字段 | 必需 | 来源 |
|---|---|---|
| generated results | 是 | AI 生成出的图像或视频结果 |
| asset-bible | 是 | `script-asset-breakdown` |
| shot-plan | 是 | `storyboard-shot-planner` |
| generation-brief | 建议 | `model-prompt-adapter-jimeng` |

## 输出

使用 [`templates/consistency-report.md`](templates/consistency-report.md) 输出 `consistency-report`。

## 工作流程

### Step 1 - 建立锚点

读取 [`references/identity-anchor-rules.md`](references/identity-anchor-rules.md)，从 `asset-bible` 中提取每个角色和场景的稳定锚点:

- 角色稳定特征: 发型、发色、脸型、标志性服装、配饰
- 状态变更点: 换装、受伤、昼夜变化、场景切换
- 道具锚点: 颜色、形状、是否持有、损坏状态

### Step 2 - 建立连续性分组

根据 `shot-plan` 将生成结果分为需要连续一致的检查组:

- 同一场景内连续镜头
- 同一角色的连续特写组
- 同一动作段落或对话往返镜头
- 同一环境和时间段的镜头组

### Step 3 - 逐组检查

读取 [`references/consistency-checklist.md`](references/consistency-checklist.md) 并逐组检查:

- identity drift
- costume/state drift
- prop drift
- environment drift
- style drift

对每组给出 `stable / watch / broken` 结论。

### Step 4 - 标记修复路径

对发现的问题标记建议路径:

- **Watch**: 允许进入 QC，但在后期或下一轮生成中重点关注
- **Patch**: 可通过局部裁切、调色、参考图强化解决
- **Redo**: 必须进入 `regeneration-router` 重新规划

### Step 5 - 输出 consistency-report

填写模板并明确:

- 哪些镜头组稳定
- 哪些镜头组存在一致性风险
- 哪些镜头必须返工
- 修复时需要锁定的参考图、seed、角色锚点
