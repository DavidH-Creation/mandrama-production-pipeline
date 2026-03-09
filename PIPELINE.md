# 漫剧制作流程 — 5 Skills Pipeline

```
format-style-planner ──project-spec──▶ script-asset-breakdown ──asset-bible + canonical-prompts──▶
storyboard-shot-planner ──shot-plan──▶ model-prompt-adapter-jimeng ──generation-brief──▶
shot-qc-and-edit-assembler ──qc-report──▶
```

## Skills

| # | Skill | 输入 | 输出 | 职责 |
|---|-------|------|------|------|
| 1 | [format-style-planner](format-style-planner/SKILL.md) | 题材/平台/受众 | project-spec | 视觉风格、画幅、平台规格、色调方向 |
| 2 | [script-asset-breakdown](script-asset-breakdown/SKILL.md) | 剧本 + project-spec | asset-bible, canonical-prompts | 角色/场景/道具提取 + 标准化描述 |
| 3 | [storyboard-shot-planner](storyboard-shot-planner/SKILL.md) | 剧本 + project-spec + asset-bible | shot-plan | 分镜编排（景别/运镜/节奏） |
| 4 | [model-prompt-adapter-jimeng](model-prompt-adapter-jimeng/SKILL.md) | shot-plan + canonical-prompts + project-spec | generation-brief | 转即梦可用 prompt + 参数 |
| 5 | [shot-qc-and-edit-assembler](shot-qc-and-edit-assembler/SKILL.md) | 生成结果 + shot-plan + asset-bible | qc-report | 质检评分 + 重生成建议 + 剪辑指引 |

## 安装

将任意 skill 目录复制到 `~/.claude/skills/` 即可在 Claude Code 中使用。

```bash
# 安装全部
cp -r format-style-planner script-asset-breakdown storyboard-shot-planner \
      model-prompt-adapter-jimeng shot-qc-and-edit-assembler ~/.claude/skills/

# 或安装单个
cp -r format-style-planner ~/.claude/skills/
```

Windows PowerShell:

```powershell
Copy-Item format-style-planner, script-asset-breakdown, storyboard-shot-planner, `
  model-prompt-adapter-jimeng, shot-qc-and-edit-assembler `
  -Destination $HOME\.claude\skills\ -Recurse
```

## 中间产物

| 产物 | 产出方 | 消费方 |
|------|--------|--------|
| project-spec | skill 1 | skill 2, 3, 4 |
| asset-bible | skill 2 | skill 3, 4, 5 |
| canonical-prompts | skill 2 | skill 4 |
| shot-plan | skill 3 | skill 4, 5 |
| generation-brief | skill 4 | skill 5 |
| qc-report | skill 5 | 用户 |

## 相关项目

- [mandrama-export-adaptation](https://github.com/DavidH-Creation/mandrama-export-adaptation) — 漫剧出海改编 skill（市场路由、文化改写、对白本地化）
