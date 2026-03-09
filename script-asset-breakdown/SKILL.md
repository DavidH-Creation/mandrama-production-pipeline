---
name: script-asset-breakdown
description: >-
  从漫剧剧本中系统提取人物、场景、道具、服装、表情状态等视觉资产，
  生成 asset-bible 和 canonical-prompts。
  当用户提供了剧本并需要拆解角色外观、场景设定、道具清单，
  或需要为 AI 生图建立角色一致性描述时触发。
---

# Script Asset Breakdown

漫剧制作流程的第二个环节。拿到剧本和 project-spec 后，系统化提取所有需要视觉化的资产，并为每个资产写好标准化描述（canonical-prompt），确保后续生图时角色和场景的一致性。

## 职责

- 逐场景扫描剧本，提取全部视觉资产（人物、场景、道具、服装）
- 为每个角色建立外观档案：面部特征、体型、发型、标志性服装、常见表情/姿态
- 为每个场景建立环境档案：空间类型、光照条件、关键道具摆放、氛围
- 跟踪资产状态变化：角色换装、道具损坏/出现/消失、场景昼夜/天气切换
- 为每个资产生成 canonical-prompt：一段标准化的英文视觉描述，作为生图时的一致性锚点
- 输出 asset-bible + canonical-prompts

## 不负责

- 画风或平台规格决策 → `format-style-planner`
- 镜头编排和分镜 → `storyboard-shot-planner`
- 转为特定模型 prompt 语法 → `model-prompt-adapter-jimeng`
- 质检生成结果 → `shot-qc-and-edit-assembler`

## 输入

| 字段 | 必需 | 来源 |
|------|------|------|
| 剧本全文或分集大纲 | 是 | 用户提供 |
| project-spec | 是 | `format-style-planner` 输出 |

project-spec 中需要的关键信息：视觉风格（2D/3D/真人仿真）、色调方向、画面质感关键词。这些会影响 canonical-prompt 的措辞方式。

## 输出

- asset-bible → 使用 [`templates/asset-bible.md`](templates/asset-bible.md)
- canonical-prompts → 使用 [`templates/canonical-prompts.md`](templates/canonical-prompts.md)

## 工作流程

### Step 1 — 读取 project-spec

确认视觉风格和色调方向，因为 canonical-prompt 的措辞需要匹配风格（2D插画用不同描述词汇于3D写实）。

### Step 2 — 通读剧本，建立资产清单

读取 [`references/asset-extraction-rules.md`](references/asset-extraction-rules.md) 了解提取规则，然后：

- **角色扫描**：记录每个出场角色的名字、首次出场场景、外观描述
- **场景扫描**：记录每个场景的名称、空间类型、光照、氛围
- **道具扫描**：记录剧情关键道具（不是背景装饰）
- **服装扫描**：记录角色服装变化节点
- **状态跟踪**：标注资产在剧情中的变化（受伤、换装、昼夜切换）

### Step 3 — 补全隐含信息

剧本通常不会写清所有视觉细节。对缺失信息：
- 根据角色性格和题材类型推断合理的外观默认值
- 明确标注哪些是剧本原文描述、哪些是推断补全
- 让用户确认关键推断（主角外貌等）

### Step 4 — 写 canonical-prompts

读取 [`references/canonical-prompt-guide.md`](references/canonical-prompt-guide.md)，为每个资产写标准化描述：

- 使用英文（生图模型对英文 prompt 效果更好）
- 保持句式统一，便于拼接到镜头 prompt 中
- 区分"核心特征"（每次必带）和"可选特征"（特定场景追加）

### Step 5 — 组装输出

填写 asset-bible 和 canonical-prompts 模板，交给用户确认。
