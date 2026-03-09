# Regeneration Brief

> Output from `regeneration-router`.
> Used to run a focused second-pass generation instead of rebuilding the whole episode.

---

## Project Info

```yaml
project_name: ""
episode: 0
source_qc_report: ""
source_generation_brief: ""
generated_at: ""
```

## Retry Summary

| Metric | Value |
|---|---|
| keep | |
| patch | |
| partial_redo | |
| full_redo | |
| total_retry_batches | |

## Retry Batches

### Batch R01

```yaml
batch_id: "R01"
strategy: ""              # patch / partial_redo / full_redo
shots: ["S01-003", "S01-004"]
shared_reference_shot: ""
shared_seed_group: ""
priority: ""              # high / medium / low
reason: ""
```

### Shot Actions

| Shot ID | Action | Failure Type | Prompt Change | Param Override |
|---|---|---|---|---|
| | keep / patch / partial_redo / full_redo | | | |

---

## Revised Shot Specs

### S01-003

```yaml
shot_ref: "S01-003"
action: ""                # keep / patch / partial_redo / full_redo
failure_type: []          # identity / composition / emotion / technical / motion / continuity
reference_shot: ""
seed_group: ""
gen_mode_override: ""     # optional
```

```text
prompt_delta:
- add:
- remove:
- emphasize:
```

```yaml
param_overrides:
  size: ""
  style_weight: null
  seed: null
  reference_strength: null
```

```text
operator_note:
```

---

## Keep As-Is List

| Shot ID | Why It Stays |
|---|---|
| | |
