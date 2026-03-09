# Generation Brief — 即梦

> 由 `model-prompt-adapter-jimeng` 输出，供 `shot-qc-and-edit-assembler` 和用户消费。
> 每个镜头条目包含可直接用于即梦生成的完整参数。

---

## 全局参数

```yaml
project_name: ""
episode: 0
model_version: ""         # 即梦模型版本
default_size: ""          # 默认图像尺寸（如 1080x1920）
default_style_preset: ""  # 默认风格预设（如有）
global_negative_prompt: "" # 全局负面提示词
```

---

## 逐镜头 Prompt

### S01-001

```yaml
shot_ref: "S01-001"       # 对应 shot-plan 中的镜头ID
gen_mode: ""              # text2img / img2img / text2video / img2video

# === Prompt ===
prompt: |
  [完整的即梦 prompt，包含场景+角色+动作+构图+风格]

negative_prompt: |
  [负面提示词：排除不需要的元素和常见质量问题]

# === 参数 ===
params:
  size: ""                # 图像尺寸
  style_weight: 0         # 风格权重 (0-1)
  seed: null              # 种子值（null=随机，指定值=锁定）
  steps: 0                # 推理步数
  cfg_scale: 0            # 提示词引导强度
  reference_image: ""     # 参考图路径（img2img 模式）
  reference_strength: 0   # 参考图影响强度 (0-1)

# === 一致性控制 ===
consistency:
  character_lock: []      # 需要角色锁定的角色ID列表
  seed_group: ""          # 种子组标识（同组镜头共享种子基数）
  reference_shot: ""      # 参考镜头ID（使用其生成结果作为参考）

# === 质检预期 ===
expected:
  characters: ["C01"]     # 预期出现的角色
  scene: "L01"            # 预期场景
  shot_type: ""           # 预期景别
  key_elements: []        # 画面中必须出现的关键元素
```

---

### S01-002

*(重复以上结构)*

---

## 生成批次规划

> 按一致性需求分组，同组镜头建议连续生成以利用 seed 控制。

| 批次 | 镜头列表 | 共享控制 | 说明 |
|------|----------|----------|------|
| Batch-1 | S01-001, S01-002, S01-003 | seed_group: sg01 | 同场景连续镜头 |
| Batch-2 | S01-004, S01-005 | character_lock: C01 | 角色特写组 |

---

## 统计

| 指标 | 值 |
|------|-----|
| 总 prompt 数 | |
| text2img 数量 | |
| img2img 数量 | |
| text2video 数量 | |
| img2video 数量 | |
| 需角色锁定的镜头数 | |
| seed 组数 | |
