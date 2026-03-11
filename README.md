# mandrama-production-pipeline

> Modular production workflow skill pack for AI-assisted manhua-drama creation.

## 导览 / Overview

- 中文说明见下方 `中文`
- English documentation starts at `English`
- 核心目录：各 skill 文件夹、`schemas/`、`PIPELINE.md`

## 中文

一个面向 AI 辅助漫剧制作流程的七段式模块化 skill 仓库。

这个仓库是一个**制作工作流 skill 包**，不是单一的大而全 skill。它把流程拆成了清晰的交接阶段：

1. `format-style-planner` -> 决定形式、画幅比例、平台适配和视觉方向
2. `script-asset-breakdown` -> 提取角色、场景、道具、服装和规范化提示词
3. `storyboard-shot-planner` -> 把剧本和资产转成逐镜头分镜方案
4. `model-prompt-adapter-jimeng` -> 把规范化描述转成适配即梦 / Dreamina 的 prompts
5. `consistency-keeper` -> 检测跨镜头的人设、服装、道具、环境和风格漂移
6. `shot-qc-and-edit-assembler` -> 审核生成镜头，并输出质检和剪辑组装建议
7. `regeneration-router` -> 把质检失败转成聚焦型重试方案，而不是整段推倒重来

### 你能得到什么

- 一个模块化流程，而不是单个超载的 skill
- 清晰的中间产物：`project-spec`、`asset-bible`、`canonical-prompts`、`shot-plan`、`generation-brief`、`consistency-report`、`qc-report`、`regeneration-brief`
- 每个制作阶段独立的 references 和 templates
- 一个即梦专用的 prompt 适配器，同时保持上游规划模型无关
- 一个用于连续性漂移和定向重生成的闭环修复流程
- 共享流程产物的 JSON Schema 定义

### 仓库结构

```text
format-style-planner/
script-asset-breakdown/
storyboard-shot-planner/
model-prompt-adapter-jimeng/
consistency-keeper/
shot-qc-and-edit-assembler/
regeneration-router/
schemas/
PIPELINE.md
```

每个 skill 文件夹都包含：

- `SKILL.md`：触发条件和工作流说明
- `references/`：只在需要时加载的更深入指南
- `templates/`：标准化输出模板

仓库还包含 `schemas/`，用于对主要中间产物做机器可读的结构校验。

### 安装方式

#### Codex

先克隆仓库：

```bash
git clone https://github.com/DavidH-Creation/mandrama-production-pipeline.git
```

再把一个或多个 skill 文件夹复制到你的本地 Codex skills 目录：

```bash
cp -r format-style-planner script-asset-breakdown storyboard-shot-planner \
      model-prompt-adapter-jimeng consistency-keeper shot-qc-and-edit-assembler \
      regeneration-router ~/.codex/skills/
```

#### Claude Code

先克隆仓库：

```bash
git clone https://github.com/DavidH-Creation/mandrama-production-pipeline.git
```

再把一个或多个 skill 文件夹复制到你的本地 Claude Code skills 目录。

##### macOS / Linux

```bash
cp -r format-style-planner script-asset-breakdown storyboard-shot-planner \
      model-prompt-adapter-jimeng consistency-keeper shot-qc-and-edit-assembler \
      regeneration-router ~/.claude/skills/
```

##### Windows PowerShell

```powershell
Copy-Item format-style-planner, script-asset-breakdown, storyboard-shot-planner, `
  model-prompt-adapter-jimeng, consistency-keeper, shot-qc-and-edit-assembler, `
  regeneration-router `
  -Destination $HOME\.claude\skills\ -Recurse
```

如果只安装一个 skill，就只复制对应文件夹即可。

### 推荐使用顺序

按这个顺序运行：

`format-style-planner -> script-asset-breakdown -> storyboard-shot-planner -> model-prompt-adapter-jimeng -> consistency-keeper -> shot-qc-and-edit-assembler -> regeneration-router`

把 `consistency-keeper` 和 `shot-qc-and-edit-assembler` 当成审核层，在需要有针对性的二次修复而不是整集重做时，再运行 `regeneration-router`。

完整流程说明、中间产物映射和 schema 列表见 [PIPELINE.md](PIPELINE.md)。

### 相关项目

- [mandrama-export-adaptation](https://github.com/DavidH-Creation/mandrama-export-adaptation) 用于出海市场改编和包装

### 许可证

MIT

---

## English

Seven modular skills for an AI-assisted manhua-drama production pipeline.

This repo is a **production workflow skill pack**, not a single monolithic skill. It breaks the pipeline into clear handoff stages:

1. `format-style-planner` -> decide format, aspect ratio, platform fit, and visual direction
2. `script-asset-breakdown` -> extract characters, scenes, props, costumes, and canonical prompts
3. `storyboard-shot-planner` -> convert script + assets into a shot-by-shot storyboard plan
4. `model-prompt-adapter-jimeng` -> adapt canonical descriptions into Jimeng/Dreamina-ready prompts
5. `consistency-keeper` -> detect cross-shot identity, costume, prop, environment, and style drift
6. `shot-qc-and-edit-assembler` -> review generated shots and produce QC + edit assembly guidance
7. `regeneration-router` -> convert QC failures into focused retry plans instead of full restarts

### What You Get

- A modular workflow instead of one overloaded skill
- Clear intermediate artifacts: `project-spec`, `asset-bible`, `canonical-prompts`, `shot-plan`, `generation-brief`, `consistency-report`, `qc-report`, `regeneration-brief`
- Dedicated references and templates for each production stage
- A Jimeng-specific prompt adapter while keeping upstream planning model-agnostic
- A closed repair loop for continuity drift and targeted regeneration
- JSON Schema definitions for the shared pipeline artifacts

### Repository Structure

```text
format-style-planner/
script-asset-breakdown/
storyboard-shot-planner/
model-prompt-adapter-jimeng/
consistency-keeper/
shot-qc-and-edit-assembler/
regeneration-router/
schemas/
PIPELINE.md
```

Each skill folder contains:

- `SKILL.md` for trigger and workflow instructions
- `references/` for deeper guidance loaded only when needed
- `templates/` for standardized outputs

The repo also includes `schemas/` with JSON Schema files for machine-readable validation of the main intermediate artifacts.

### Installation

#### Codex

Clone the repo first:

```bash
git clone https://github.com/DavidH-Creation/mandrama-production-pipeline.git
```

Then copy one or more skill folders into your local Codex skills directory:

```bash
cp -r format-style-planner script-asset-breakdown storyboard-shot-planner \
      model-prompt-adapter-jimeng consistency-keeper shot-qc-and-edit-assembler \
      regeneration-router ~/.codex/skills/
```

#### Claude Code

Clone the repo first:

```bash
git clone https://github.com/DavidH-Creation/mandrama-production-pipeline.git
```

Then copy one or more skill folders into your local Claude Code skills directory.

##### macOS / Linux

```bash
cp -r format-style-planner script-asset-breakdown storyboard-shot-planner \
      model-prompt-adapter-jimeng consistency-keeper shot-qc-and-edit-assembler \
      regeneration-router ~/.claude/skills/
```

##### Windows PowerShell

```powershell
Copy-Item format-style-planner, script-asset-breakdown, storyboard-shot-planner, `
  model-prompt-adapter-jimeng, consistency-keeper, shot-qc-and-edit-assembler, `
  regeneration-router `
  -Destination $HOME\.claude\skills\ -Recurse
```

To install only one skill, copy just that folder.

### Recommended Usage Order

Run the skills in this order:

`format-style-planner -> script-asset-breakdown -> storyboard-shot-planner -> model-prompt-adapter-jimeng -> consistency-keeper -> shot-qc-and-edit-assembler -> regeneration-router`

Use `consistency-keeper` and `shot-qc-and-edit-assembler` as the review layer, then run `regeneration-router` when you need a targeted second pass instead of rebuilding the whole episode.

See [PIPELINE.md](PIPELINE.md) for the full pipeline overview, intermediate artifact map, and schema list.

### Related Project

- [mandrama-export-adaptation](https://github.com/DavidH-Creation/mandrama-export-adaptation) for export-market adaptation and packaging

### License

MIT
