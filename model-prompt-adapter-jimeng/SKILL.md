---
name: model-prompt-adapter-jimeng
description: >-
  将分镜计划和资产描述转换为即梦（Jimeng/Dreamina）可直接使用的
  图像和视频生成 prompt，输出 generation-brief。
  当用户需要为即梦生成 prompt、调整即梦参数、
  或批量生成即梦 API 调用格式时触发。
---

# Model Prompt Adapter — 即梦

漫剧制作流程的第四个环节。把通用的分镜描述和资产描述，翻译成即梦（Jimeng/Dreamina）能直接执行的 prompt 和参数组合。这一步是"创意语言"到"机器语言"的桥梁。

## 职责

- 将 shot-plan 中每个镜头的画面描述转为即梦 prompt
- 从 canonical-prompts 中提取对应角色/场景描述片段，拼接到镜头 prompt
- 适配即梦的参数体系（模型版本、尺寸、风格、负面提示词等）
- 区分图像生成和视频生成的 prompt 模式
- 为连续镜头设计一致性控制策略（seed 锁定、参考图、角色锁定）
- 输出 generation-brief

## 不负责

- 镜头内容决策 → `storyboard-shot-planner`
- 生成结果质量判断 → `shot-qc-and-edit-assembler`
- 适配其他模型（Midjourney、DALL-E、Stable Diffusion 等）
- 视觉风格选择 → `format-style-planner`

## 输入

| 字段 | 必需 | 来源 |
|------|------|------|
| shot-plan | 是 | `storyboard-shot-planner` |
| canonical-prompts | 是 | `script-asset-breakdown` |
| project-spec | 是 | `format-style-planner` |

从 project-spec 中需要：画幅比例（→ 即梦尺寸参数）、视觉风格关键词（→ 风格权重）。
从 canonical-prompts 中需要：角色和场景的标准描述片段。
从 shot-plan 中需要：每个镜头的画面内容、景别、运镜、情绪。

## 输出

使用 [`templates/generation-brief.md`](templates/generation-brief.md) 模板输出 generation-brief。

## 工作流程

### Step 1 — 读取即梦规格

读取 [`references/jimeng-api-spec.md`](references/jimeng-api-spec.md) 确认当前可用的：
- 模型版本及能力范围
- 支持的图像尺寸列表
- 视频生成的时长和分辨率限制
- prompt 长度限制
- 可用的风格预设和参数

### Step 2 — 映射画幅到即梦尺寸

根据 project-spec 的画幅比例：
- 9:16 竖屏 → 对应即梦竖屏尺寸
- 16:9 横屏 → 对应即梦横屏尺寸
- 1:1 → 对应即梦方图尺寸

### Step 3 — 逐镜头转写 prompt

对 shot-plan 中的每个镜头：

1. **组装主体描述**：从 canonical-prompts 提取出场角色和场景的核心描述
2. **添加镜头语言**：将景别和构图转为即梦理解的描述词
3. **添加风格控制**：从 project-spec 的视觉参考关键词中选取适用项
4. **添加情绪/氛围**：根据镜头情绪标注添加光影/色调描述
5. **编写负面提示词**：排除常见质量问题和不需要的元素

参考 [`references/prompt-pattern-library.md`](references/prompt-pattern-library.md) 查已验证有效的 prompt 模式。

### Step 4 — 一致性控制

为需要保持角色/场景一致的连续镜头：
- 标注哪些镜头应共享 seed
- 标注哪些镜头需要使用参考图（图生图模式）
- 标注角色锁定需求（同一角色跨镜头保持外貌一致）

### Step 5 — 区分生成模式

每个镜头标注生成类型：
- **文生图**：纯文本 prompt → 静态画面
- **图生图**：以上一镜头或参考图为基础 → 变化画面
- **文生视频**：文本 prompt → 短视频片段
- **图生视频**：静态画面 → 动态视频

### Step 6 — 组装 generation-brief

用模板填写完整的 generation-brief。每个镜头条目包含：完整 prompt、负面 prompt、参数配置、生成模式、一致性控制标注。
