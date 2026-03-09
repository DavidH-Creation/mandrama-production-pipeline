---
name: storyboard-shot-planner
description: >-
  将漫剧剧本和资产拆解为按集、按场、按镜头编排的分镜计划（shot-plan），
  包含景别、构图、运镜、角色站位和情绪节奏。
  当用户需要把剧本转成分镜脚本、规划每个镜头的画面内容、
  或编排一集的视觉节奏时触发。
---

# Storyboard Shot Planner

漫剧制作流程的第三个环节。把剧本文字和资产清单转化为可执行的分镜计划——每个镜头该拍什么、怎么拍、画面里有谁。

## 职责

- 将剧本按 **集 → 场 → 镜头** 三级拆解
- 为每个镜头指定景别、构图要点、运镜方式
- 标注镜头内的角色站位、表情状态、关键动作
- 编排情绪节奏曲线（紧张→释放→高潮→留白）
- 标注镜头间的转场方式
- 输出 shot-plan

## 不负责

- 资产提取或外观定义 → `script-asset-breakdown`
- 生成 prompt 编写 → `model-prompt-adapter-jimeng`
- 生成结果质检 → `shot-qc-and-edit-assembler`
- 画风和平台选择 → `format-style-planner`

## 输入

| 字段 | 必需 | 来源 |
|------|------|------|
| 剧本（全文或单集） | 是 | 用户提供 |
| project-spec | 是 | `format-style-planner` |
| asset-bible | 是 | `script-asset-breakdown` |

从 project-spec 中需要：画幅比例（影响构图规划）、单条时长限制（影响镜头数量）。
从 asset-bible 中需要：角色列表和场景列表（引用时用 ID 而非重复描述）。

## 输出

使用 [`templates/shot-plan.md`](templates/shot-plan.md) 模板输出 shot-plan。

## 工作流程

### Step 1 — 确认规格约束

从 project-spec 提取：
- 画幅比例 → 决定构图空间（竖屏构图和横屏构图差异大）
- 单集时长 → 估算总镜头数（漫剧通常 1-3 分钟/集，每镜头 2-5 秒）
- 视觉风格 → 影响运镜方式（2D 适合固定镜头 + 平移；3D 适合推拉摇移）

### Step 2 — 场景拆解

将剧本按场景边界分割，每个场景标注：
- 场景 ID（S01、S02...）
- 对应 asset-bible 中的场景条目
- 场景内出场角色
- 场景情绪基调

### Step 3 — 逐场景排镜头

读取 [`references/shot-language-guide.md`](references/shot-language-guide.md) 查景别/运镜术语。

每个镜头需填写：
- 镜头 ID（S01-001、S01-002...）
- 景别：特写 / 近景 / 中景 / 中全景 / 全景 / 远景
- 构图要点：角色位置（三分法/居中/对角）、视线方向、景深
- 运镜：固定 / 推 / 拉 / 左摇 / 右摇 / 上移 / 下移 / 跟拍
- 画面内容：谁在做什么、什么表情、关键动作
- 对白/旁白：该镜头覆盖的台词
- 预估时长（秒）
- 转场到下一镜头的方式：硬切 / 溶解 / 擦除 / 闪白 / 闪黑

### Step 4 — 编排节奏

读取 [`references/pacing-rhythm-rules.md`](references/pacing-rhythm-rules.md)，检查并调整：
- 连续同景别镜头不超过 3 个（避免视觉疲劳）
- 高潮场景用更短的镜头、更紧的景别
- 情绪转折点用适当的停顿镜头（空镜/反应镜头）
- 开场前 3 秒必须有强视觉钩子
- 每集总时长符合平台限制

### Step 5 — 标注情绪曲线

为每集绘制情绪标注：
- 标记每个镜头的情绪强度（1-5）
- 确认高潮点位置
- 确认节奏不是一路平或一路冲

### Step 6 — 填写 shot-plan

用模板组装完整的 shot-plan，交给用户确认。
