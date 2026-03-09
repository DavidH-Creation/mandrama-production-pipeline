# Manhua-Drama Production Pipeline

```text
format-style-planner -> project-spec
script-asset-breakdown -> asset-bible + canonical-prompts
storyboard-shot-planner -> shot-plan
model-prompt-adapter-jimeng -> generation-brief
consistency-keeper -> consistency-report
shot-qc-and-edit-assembler -> qc-report
regeneration-router -> regeneration-brief
```

## Skills

| # | Skill | Input | Output | Responsibility |
|---|---|---|---|---|
| 1 | [format-style-planner](format-style-planner/SKILL.md) | concept / platform / audience | project-spec | decide format, aspect ratio, platform fit, visual direction |
| 2 | [script-asset-breakdown](script-asset-breakdown/SKILL.md) | script + project-spec | asset-bible, canonical-prompts | extract characters, scenes, props, costumes, visual anchors |
| 3 | [storyboard-shot-planner](storyboard-shot-planner/SKILL.md) | script + project-spec + asset-bible | shot-plan | turn script into scene and shot structure |
| 4 | [model-prompt-adapter-jimeng](model-prompt-adapter-jimeng/SKILL.md) | shot-plan + canonical-prompts + project-spec | generation-brief | adapt canonical descriptions into Jimeng-ready prompts |
| 5 | [consistency-keeper](consistency-keeper/SKILL.md) | generated results + asset-bible + shot-plan | consistency-report | check cross-shot identity, costume, prop, environment, and style stability |
| 6 | [shot-qc-and-edit-assembler](shot-qc-and-edit-assembler/SKILL.md) | generated results + shot-plan + asset-bible + consistency-report | qc-report | judge story/shot match and prepare edit assembly guidance |
| 7 | [regeneration-router](regeneration-router/SKILL.md) | qc-report + generation-brief + shot-plan + consistency-report | regeneration-brief | convert failures into a focused retry plan |

## Installation

Copy any skill folders you want into `~/.claude/skills/`.

### macOS / Linux

```bash
cp -r format-style-planner script-asset-breakdown storyboard-shot-planner \
      model-prompt-adapter-jimeng consistency-keeper shot-qc-and-edit-assembler \
      regeneration-router ~/.claude/skills/
```

### Windows PowerShell

```powershell
Copy-Item format-style-planner, script-asset-breakdown, storyboard-shot-planner, `
  model-prompt-adapter-jimeng, consistency-keeper, shot-qc-and-edit-assembler, `
  regeneration-router -Destination $HOME\.claude\skills\ -Recurse
```

## Intermediate Artifacts

| Artifact | Produced By | Consumed By |
|---|---|---|
| project-spec | skill 1 | skills 2, 3, 4 |
| asset-bible | skill 2 | skills 3, 5, 6, 7 |
| canonical-prompts | skill 2 | skill 4 |
| shot-plan | skill 3 | skills 4, 5, 6, 7 |
| generation-brief | skill 4 | skills 6, 7 |
| consistency-report | skill 5 | skills 6, 7 |
| qc-report | skill 6 | skill 7 |
| regeneration-brief | skill 7 | user / next generation pass |

## JSON Schemas

Machine-readable validation schemas live under [`schemas/`](schemas):

- `project-spec.schema.json`
- `asset-bible.schema.json`
- `canonical-prompts.schema.json`
- `shot-plan.schema.json`
- `generation-brief.schema.json`
- `consistency-report.schema.json`
- `qc-report.schema.json`
- `regeneration-brief.schema.json`

## Recommended Loop

Use the main path for the first generation pass:

`format-style-planner -> script-asset-breakdown -> storyboard-shot-planner -> model-prompt-adapter-jimeng`

Then use the quality loop:

`consistency-keeper -> shot-qc-and-edit-assembler -> regeneration-router`

If regeneration is needed, run the new `regeneration-brief` back through your generation workflow and review again.
