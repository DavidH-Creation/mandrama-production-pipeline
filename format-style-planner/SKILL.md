---
name: format-style-planner
description: >-
  Plan the production format and visual direction for a manhua-drama project, including 2D vs 3D vs photoreal 3D,
  horizontal vs vertical framing, target platform fit, and a final project-spec output.
  Use when starting a new comic-drama project, deciding visual style direction, choosing platform specs,
  or comparing vertical short-form vs horizontal long-form presentation. 为漫剧项目确定视觉风格、画幅比例、
  平台适配和整体视觉方向，输出 project-spec。
---

# Format & Style Planner

漫剧制作流程的第一个环节。在动手拆剧本或画分镜之前，先把视觉基调和技术规格锁死，避免后续返工。

## 职责

- 根据题材、受众、平台匹配视觉风格路线（2D插画 / 3D渲染 / 真人仿真3D / 混合）
- 确定画幅比例（9:16 竖屏 / 16:9 横屏 / 1:1 方屏）
- 查平台技术规格（分辨率、时长限制、安全区）并写入 project-spec
- 定义色调方向、光影风格、视觉参考关键词
- 输出完整 project-spec 供下游 skill 消费

## 不负责

- 剧本拆解或资产提取 → `script-asset-breakdown`
- 分镜编排 → `storyboard-shot-planner`
- 生成 prompt → `model-prompt-adapter-jimeng`
- 市场路由或文化改编 → `mandrama-export-adaptation`

## 输入

用户提供以下信息（部分可选）：

| 字段 | 必需 | 说明 |
|------|------|------|
| 题材/剧本概要 | 是 | 一句话或一段概要 |
| 目标平台 | 是 | 抖音/快手/YouTube Shorts/B站/微信视频号/其他 |
| 目标受众 | 建议 | 年龄段、性别偏向、地域 |
| 预算/产能约束 | 可选 | 影响风格选择（低成本倾向2D，高成本可3D） |
| 已有视觉参考 | 可选 | 图片链接或风格关键词 |

## 输出

使用 [`templates/project-spec.md`](templates/project-spec.md) 模板输出 project-spec。

## 工作流程

### Step 1 — 收集输入

向用户确认题材、平台、受众。缺失信息标注默认值并注明假设。

### Step 2 — 查平台规格

读取 [`references/platform-spec-matrix.md`](references/platform-spec-matrix.md)，查目标平台的：
- 推荐分辨率和画幅
- 单条内容时长上限
- 安全区规范（标题/互动按钮遮挡区域）

### Step 3 — 选择视觉风格

读取 [`references/visual-style-taxonomy.md`](references/visual-style-taxonomy.md)，按决策树匹配：
- 题材情绪基调 → 风格候选集
- 受众偏好 → 缩小候选
- 产能约束 → 最终推荐

输出推荐风格并说明理由，附排除项及原因。

### Step 4 — 定义视觉方向

确定：
- 主色调和辅助色
- 光影风格（高对比/柔光/赛博霓虹/自然光等）
- 视觉参考关键词（5-8个，供后续 prompt 使用）
- 画面质感（胶片颗粒/干净数码/水彩/漫画网点等）

### Step 5 — 填写 project-spec

用 [`templates/project-spec.md`](templates/project-spec.md) 填写完整 project-spec，交给用户确认。
