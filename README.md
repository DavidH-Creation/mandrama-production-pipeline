# mandrama-production-pipeline

Seven modular skills for an AI-assisted manhua-drama production pipeline.

This repo is a **production workflow skill pack**, not a single monolithic skill. It breaks the pipeline into clear handoff stages:

1. `format-style-planner` -> decide format, aspect ratio, platform fit, and visual direction
2. `script-asset-breakdown` -> extract characters, scenes, props, costumes, and canonical prompts
3. `storyboard-shot-planner` -> convert script + assets into a shot-by-shot storyboard plan
4. `model-prompt-adapter-jimeng` -> adapt canonical descriptions into Jimeng/Dreamina-ready prompts
5. `consistency-keeper` -> detect cross-shot identity, costume, prop, environment, and style drift
6. `shot-qc-and-edit-assembler` -> review generated shots and produce QC + edit assembly guidance
7. `regeneration-router` -> convert QC failures into focused retry plans instead of full restarts

## What You Get

- A modular workflow instead of one overloaded skill
- Clear intermediate artifacts: `project-spec`, `asset-bible`, `canonical-prompts`, `shot-plan`, `generation-brief`, `consistency-report`, `qc-report`, `regeneration-brief`
- Dedicated references and templates for each production stage
- A Jimeng-specific prompt adapter while keeping upstream planning model-agnostic
- A closed repair loop for continuity drift and targeted regeneration
- JSON Schema definitions for the shared pipeline artifacts

## Repo Structure

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

## Installation

Copy one or more skill folders into your local skills directory.

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
  regeneration-router `
  -Destination $HOME\.claude\skills\ -Recurse
```

To install only one skill, copy just that folder.

## Recommended Usage Order

Run the skills in this order:

`format-style-planner -> script-asset-breakdown -> storyboard-shot-planner -> model-prompt-adapter-jimeng -> consistency-keeper -> shot-qc-and-edit-assembler -> regeneration-router`

Use `consistency-keeper` and `shot-qc-and-edit-assembler` as the review layer, then run `regeneration-router` when you need a targeted second pass instead of rebuilding the whole episode.

See [PIPELINE.md](PIPELINE.md) for the full pipeline overview, intermediate artifact map, and schema list.

## Related Project

- [mandrama-export-adaptation](https://github.com/DavidH-Creation/mandrama-export-adaptation) for export-market adaptation and packaging

## License

MIT
