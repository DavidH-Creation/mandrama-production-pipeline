# Shot Plan

> 由 `storyboard-shot-planner` 输出，供 `model-prompt-adapter-jimeng` 和 `shot-qc-and-edit-assembler` 消费。

---

## 项目信息

```yaml
project_name: ""
episode: 0
total_scenes: 0
total_shots: 0
estimated_duration_sec: 0
```

## 情绪节奏曲线

> 标注本集的情绪走势和关键转折点。

```
镜头序号:  001  002  003  004  005  006  007  008  ...
情绪强度:   2    2    3    4    5    3    2    4   ...
           ──── 铺垫 ───  ─ 升温 ─ ★高潮  ─ 回落 ─ ★二次高潮
```

---

## 分镜明细

### 场景 S01 — [场景名]

**场景信息:**
```yaml
scene_id: "S01"
location_ref: "L01"       # 对应 asset-bible 中的场景ID
characters_present: ["C01", "C02"]
scene_mood: ""            # 紧张 / 温馨 / 压抑 / 欢快 / ...
```

---

#### S01-001

```yaml
shot_id: "S01-001"
duration_sec: 3
shot_type: ""             # 特写 / 近景 / 中景 / 中全景 / 全景 / 远景 / 大远景
framing: ""               # 三分法偏左 / 居中 / 对角线 / 过肩 / 俯拍 / 仰拍
camera_move: ""           # 固定 / 推 / 拉 / 左摇 / 右摇 / 上移 / 下移 / 跟拍
depth_of_field: ""        # 浅景深 / 中景深 / 深景深

# 画面内容
characters:
  - id: "C01"
    outfit: "C01-O1"
    expression: "neutral"
    position: ""          # 画面中的位置描述
    action: ""            # 正在做的动作
    gaze_direction: ""    # 视线方向

content_description: ""   # 画面内容的自然语言描述
dialogue: ""              # 该镜头覆盖的台词（如有）
sfx_note: ""              # 音效提示（如有）

# 情绪标注
emotion_intensity: 0      # 1-5
emotion_note: ""          # 补充说明

# 转场
transition_to_next: ""    # 硬切 / 溶解 / 擦除 / 闪白 / 闪黑 / 淡出
```

---

#### S01-002

*(重复以上结构)*

---

### 场景 S02 — [场景名]

*(重复场景+镜头结构)*

---

## 汇总统计

| 指标 | 值 |
|------|-----|
| 总镜头数 | |
| 特写镜头占比 | |
| 近景/中景占比 | |
| 全景/远景占比 | |
| 平均镜头时长 | |
| 最长镜头 | |
| 最短镜头 | |
| 总预估时长 | |
