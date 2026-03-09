# Asset Bible

> 由 `script-asset-breakdown` 输出，供 `storyboard-shot-planner`、`model-prompt-adapter-jimeng`、`shot-qc-and-edit-assembler` 消费。

---

## 角色资产

### [角色ID] — [角色名]

```yaml
character_id: "C01"
name: ""
role: ""                  # 主角 / 配角 / 龙套 / 反派
first_appearance: ""      # 首次出场：集数-场景

# 外观档案
appearance:
  gender: ""
  age_apparent: ""        # 外观年龄
  height: ""              # 高/中/矮
  build: ""               # 体型：纤细/匀称/壮硕/微胖
  face_shape: ""          # 脸型
  skin_tone: ""
  hair:
    style: ""             # 发型
    color: ""
    length: ""
  eyes:
    shape: ""
    color: ""
  distinguishing_features: []   # 疤痕/胎记/纹身/配饰等

# 服装档案（可多套）
outfits:
  - outfit_id: "C01-O1"
    name: ""              # 日常装 / 职业装 / 战斗装 / ...
    description: ""
    scenes_used: []       # 出现在哪些场景

# 常见表情/姿态
expressions:
  - neutral
  - angry
  - sad
  - surprised
  - smiling

# 状态变化记录
state_changes:
  - episode: 0
    scene: ""
    change: ""            # 换装 / 受伤 / 变身 / ...
```

---

*(为每个角色重复以上结构)*

---

## 场景资产

### [场景ID] — [场景名]

```yaml
scene_id: "L01"
name: ""
type: ""                  # 室内 / 室外 / 半室外
setting: ""               # 办公室 / 街道 / 古代庭院 / 酒吧 / ...

environment:
  time_of_day: ""         # 白天 / 黄昏 / 夜晚 / 不定
  weather: ""             # 晴 / 阴 / 雨 / 雪 / 不适用
  lighting: ""            # 自然光 / 灯光 / 混合 / 昏暗
  atmosphere: ""          # 温馨 / 压抑 / 紧张 / 奢华 / ...

key_props: []             # 场景内的关键道具
background_elements: []   # 背景元素（不影响剧情但影响画面）

# 状态变化
state_changes:
  - episode: 0
    change: ""            # 被破坏 / 装饰变化 / 昼夜切换
```

---

*(为每个场景重复以上结构)*

---

## 道具资产

### [道具ID] — [道具名]

```yaml
prop_id: "P01"
name: ""
description: ""
owner: ""                 # 所属角色（如有）
significance: ""          # 剧情关键 / 视觉标志 / 普通道具
first_appearance: ""
state_changes: []
```

---

*(为每个关键道具重复以上结构)*

---

## 资产统计

| 类别 | 数量 |
|------|------|
| 角色 | |
| 场景 | |
| 道具 | |
| 服装套数 | |
| 状态变化点 | |
