# QC Report

> 由 `shot-qc-and-edit-assembler` 输出，供用户消费。
> 逐镜头质检结果 + 重生成建议 + 剪辑合成指引。

---

## 项目信息

```yaml
project_name: ""
episode: 0
total_shots_reviewed: 0
review_date: ""
```

## 质检总览

| 指标 | 值 |
|------|-----|
| 总镜头数 | |
| 通过 (Pass) | |
| 需微调 (Adjust) | |
| 需重生成 (Redo) | |
| 通过率 | |

### 问题分类统计

| 问题类型 | 出现次数 | 占比 |
|----------|----------|------|
| 角色一致性 | | |
| 构图偏差 | | |
| 情绪不符 | | |
| 技术缺陷（畸变/伪影） | | |
| 叙事断裂 | | |

---

## 逐镜头质检

### S01-001

```yaml
shot_ref: "S01-001"
verdict: ""               # Pass / Adjust / Redo

# 评分（每项 1-5）
scores:
  character_consistency: 0   # 角色一致性
  composition_match: 0       # 构图匹配度
  emotion_match: 0           # 情绪匹配度
  technical_quality: 0       # 技术质量
  narrative_continuity: 0    # 叙事连贯性

# 问题描述（仅 Adjust/Redo 时填写）
issues:
  - type: ""              # character_consistency / composition / emotion / technical / narrative
    severity: ""          # minor / major / critical
    description: ""       # 具体问题描述

# 修改建议（仅 Adjust/Redo 时填写）
fix_suggestion:
  action: ""              # 后期裁剪 / 调色 / 修改prompt重生成 / 换参考图 / ...
  prompt_adjustment: ""   # 具体的 prompt 修改建议
  notes: ""               # 补充说明
```

---

### S01-002

*(重复以上结构)*

---

## 重生成清单

> 汇总所有需要重生成的镜头，方便批量操作。

| 镜头ID | 主要问题 | 修改方向 | 优先级 |
|--------|----------|----------|--------|
| | | | 高/中/低 |

---

## 剪辑合成建议

### 镜头排列确认

> 是否需要调整 shot-plan 中的镜头顺序。

```yaml
order_changes:
  - original: "S01-003"
    move_to: "after S01-005"
    reason: ""
```

### 转场效果

| 转场位置 | 效果 | 时长(帧) | 说明 |
|----------|------|----------|------|
| S01-001 → S01-002 | 硬切 | 0 | |
| S01-002 → S01-003 | 溶解 | 15 | |

### 配乐/音效节点

| 时间点(秒) | 类型 | 内容 | 情绪 |
|------------|------|------|------|
| 0.0 | BGM切入 | | 紧张/温暖/... |
| 5.2 | 音效 | | |
| 12.0 | BGM转调 | | |

### 字幕/对白条

```yaml
subtitle_style: ""        # 底部居中 / 顶部 / 角色旁气泡 / ...
font_suggestion: ""       # 字体建议
timing_notes: ""          # 字幕节奏备注
```

### 片头/片尾

```yaml
intro: ""                 # 片头处理：标题卡 / 冷开场 / ...
outro: ""                 # 片尾处理：下集预告 / 黑屏+文字 / ...
```

---

## 预估工作量

| 项目 | 数量 | 预估耗时 |
|------|------|----------|
| 重生成镜头 | | |
| 后期微调镜头 | | |
| 剪辑合成 | | |
