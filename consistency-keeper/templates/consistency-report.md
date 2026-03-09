# Consistency Report

> Output from `consistency-keeper`.
> Used by `shot-qc-and-edit-assembler` and `regeneration-router`.

---

## Project Info

```yaml
project_name: ""
episode: 0
review_scope: ""          # full episode / selected shots / one scene
review_date: ""
```

## Overall Verdict

| Metric | Value |
|---|---|
| sequence_groups_reviewed | |
| stable_groups | |
| watch_groups | |
| broken_groups | |
| overall_status | |   # stable / watch / broken

## Priority Fix Queue

| Priority | Group ID | Issue Type | Affected Shots | Recommended Action |
|---|---|---|---|---|
| high / medium / low | | | | |

---

## Sequence Groups

### G01

```yaml
group_id: "G01"
scope: ""                 # e.g. same scene / same character / same dialogue exchange
shots: ["S01-001", "S01-002", "S01-003"]
focus_subjects: ["C01", "L01", "P02"]
verdict: ""               # stable / watch / broken
```

### Drift Summary

| Drift Type | Severity | Description |
|---|---|---|
| identity / costume / prop / environment / style | minor / major / critical | |

### Repair Recommendation

```yaml
action: ""                # keep / patch / redo
anchor_to_lock: []        # character ids / prop ids / scene ids
reference_shot: ""        # best shot to use as reference
notes: ""
```

---

## Shot-Level Notes

| Shot ID | Verdict | Main Drift | Note |
|---|---|---|---|
| | keep / watch / redo | | |
