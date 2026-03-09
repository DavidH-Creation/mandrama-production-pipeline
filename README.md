# mandrama-production-pipeline

Five modular skills for an AI-assisted manhua-drama production pipeline.

This repo is a **production workflow skill pack**, not a single monolithic skill. It breaks the pipeline into clear handoff stages:

1. `format-style-planner` -> decide format, aspect ratio, platform fit, and visual direction
2. `script-asset-breakdown` -> extract characters, scenes, props, costumes, and canonical prompts
3. `storyboard-shot-planner` -> convert script + assets into a shot-by-shot storyboard plan
4. `model-prompt-adapter-jimeng` -> adapt canonical descriptions into Jimeng/Dreamina-ready prompts
5. `shot-qc-and-edit-assembler` -> review generated shots and produce QC + edit assembly guidance

## What You Get

- A modular workflow instead of one overloaded skill
- Clear intermediate artifacts: `project-spec`, `asset-bible`, `canonical-prompts`, `shot-plan`, `generation-brief`, `qc-report`
- Dedicated references and templates for each production stage
- A Jimeng-specific prompt adapter while keeping upstream planning model-agnostic

## Repo Structure

```text
format-style-planner/
script-asset-breakdown/
storyboard-shot-planner/
model-prompt-adapter-jimeng/
shot-qc-and-edit-assembler/
PIPELINE.md
```

Each skill folder contains:

- `SKILL.md` for trigger and workflow instructions
- `references/` for deeper guidance loaded only when needed
- `templates/` for standardized outputs

## Installation

Copy one or more skill folders into your local skills directory.

### macOS / Linux

```bash
cp -r format-style-planner script-asset-breakdown storyboard-shot-planner \
      model-prompt-adapter-jimeng shot-qc-and-edit-assembler ~/.claude/skills/
```

### Windows PowerShell

```powershell
Copy-Item format-style-planner, script-asset-breakdown, storyboard-shot-planner, `
  model-prompt-adapter-jimeng, shot-qc-and-edit-assembler `
  -Destination $HOME\.claude\skills\ -Recurse
```

To install only one skill, copy just that folder.

## Recommended Usage Order

Run the skills in this order:

`format-style-planner -> script-asset-breakdown -> storyboard-shot-planner -> model-prompt-adapter-jimeng -> shot-qc-and-edit-assembler`

See [PIPELINE.md](PIPELINE.md) for the Chinese pipeline overview and intermediate artifact map.

## Related Project

- [mandrama-export-adaptation](https://github.com/DavidH-Creation/mandrama-export-adaptation) for export-market adaptation and packaging

## License

MIT
