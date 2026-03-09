---
name: shot-qc-and-edit-assembler
description: >-
  Review AI-generated images or video clips against the shot-plan and story intent, then produce qc-report
  with quality scoring, regeneration guidance, and edit assembly recommendations.
  Use when generated shots need approval, triage, fix notes, or post-production sequencing guidance.
  检查 AI 生成结果是否符合分镜计划和剧情要求，并给出质检和剪辑建议。
---

# Shot QC & Edit Assembler

漫剧制作流程的最后一个环节。拿到 AI 生成的图像/视频后，逐镜头质检，标出需要重做的镜头并给出修改方向，同时给出最终剪辑合成的建议。

## 职责

- 逐镜头对比生成结果与 shot-plan 的要求
- 检查角色一致性（外貌是否匹配 asset-bible）
- 检查构图、景别、情绪是否符合分镜标注
- 对每个镜头给出判定：通过 / 需微调 / 需重生成
- 为需重生成的镜头提供具体的 prompt 修改建议
- 给出剪辑合成建议：镜头排列确认、转场效果、配乐节点、字幕时机
- 输出 qc-report

## 不负责

- 编写或修改生成 prompt → `model-prompt-adapter-jimeng`
- 执行实际的图像/视频生成或渲染
- 画风和平台决策 → `format-style-planner`
- 剧本拆解 → `script-asset-breakdown`
- 分镜编排 → `storyboard-shot-planner`

## 输入

| 字段 | 必需 | 来源 |
|------|------|------|
| 生成结果 | 是 | 即梦生成的图像/视频（文件路径或截图描述） |
| shot-plan | 是 | `storyboard-shot-planner` |
| asset-bible | 是 | `script-asset-breakdown` |
| generation-brief | 建议 | `model-prompt-adapter-jimeng`（用于给出 prompt 修改建议） |

## 输出

使用 [`templates/qc-report.md`](templates/qc-report.md) 模板输出 qc-report。

## 工作流程

### Step 1 — 建立质检基线

读取 [`references/qc-checklist.md`](references/qc-checklist.md)，确认质检维度和评分标准：
- 角色一致性（外貌匹配度）
- 构图匹配度（景别/角色位置/视线方向）
- 情绪匹配度（色调/光影/表情是否传达正确情绪）
- 技术质量（畸变、伪影、多余肢体、文字水印等）
- 叙事连贯性（与前后镜头的衔接是否合理）

### Step 2 — 逐镜头审查

对每个镜头：

1. **对照 shot-plan** 检查画面内容是否匹配镜头描述
2. **对照 asset-bible** 检查角色外貌是否一致（发型、服装、面部特征）
3. **检查技术质量** 识别明显缺陷（变形手指、多余肢体、画面模糊等）
4. **打分** 每个维度 1-5 分
5. **判定** 综合评分给出结论：
   - **通过（Pass）**：所有维度 ≥ 3，无关键缺陷
   - **需微调（Adjust）**：可通过后期裁剪/调色修复，不需重新生成
   - **需重生成（Redo）**：存在无法后期修复的问题

### Step 3 — 给出重生成建议

对判定为"需重生成"的镜头：
- 指出具体问题（如"角色发色偏差""景别偏远""表情不符"）
- 建议 prompt 修改方向（添加/删除/强调哪些描述词）
- 如有 generation-brief，标注原 prompt 中可能导致问题的部分

### Step 4 — 剪辑合成建议

读取 [`references/edit-assembly-guide.md`](references/edit-assembly-guide.md)，给出：
- 镜头最终排列顺序确认（是否需要调整 shot-plan 中的顺序）
- 每个转场的具体效果建议和时长
- 配乐/音效节点标注（哪一秒切入什么情绪的音乐）
- 字幕/对白条时机和样式建议
- 片头/片尾处理方式

### Step 5 — 汇总统计

- 总镜头数 / 通过数 / 需调整数 / 需重生成数
- 通过率
- 主要问题分类统计（一致性问题占比、技术问题占比等）
- 预估重生成工作量

### Step 6 — 填写 qc-report

用模板组装完整报告，交给用户。
