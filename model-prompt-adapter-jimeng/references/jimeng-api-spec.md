# 即梦 API 规格与最佳实践

> `model-prompt-adapter-jimeng` Step 1 读取本文件，确认即梦的参数限制和最佳实践。
> 注意：即梦的产品迭代较快，以下参数以截至 2025 年中的版本为准，使用时应确认是否有更新。

---

## 生成模式

### 文生图 (Text-to-Image)

输入纯文本 prompt，输出静态图像。

```yaml
参数:
  prompt: string          # 正向提示词，最长约 500 字符
  negative_prompt: string # 负面提示词
  size: string            # 图像尺寸
  model: string           # 模型版本
  num_images: 1-4         # 单次生成数量
  seed: int | null        # 随机种子（固定则复现）
```

### 图生图 (Image-to-Image)

以一张参考图为基础，通过 prompt 引导变化。

```yaml
参数:
  reference_image: file   # 参考图
  prompt: string
  negative_prompt: string
  strength: 0.0-1.0       # 参考图影响强度（越低越接近原图）
  size: string
  seed: int | null
```

### 文生视频 (Text-to-Video)

输入文本描述，输出短视频片段。

```yaml
参数:
  prompt: string
  duration: 2-5           # 视频时长（秒），通常 4s
  size: string            # 视频尺寸
  fps: 24 | 30            # 帧率
```

### 图生视频 (Image-to-Video)

以一张静态图为起始帧，生成视频。

```yaml
参数:
  reference_image: file   # 起始帧图像
  prompt: string          # 描述运动和变化
  duration: 2-5
  size: string
```

---

## 支持的尺寸

| 画幅 | 尺寸选项 |
|------|----------|
| 竖屏 9:16 | 720×1280, 1080×1920 |
| 横屏 16:9 | 1280×720, 1920×1080 |
| 方图 1:1 | 1024×1024, 1080×1080 |
| 横屏 3:2 | 1080×720 |
| 竖屏 2:3 | 720×1080 |

---

## Prompt 编写最佳实践

### 结构顺序

即梦的 prompt 理解对顺序敏感。推荐按以下顺序组织：

```
[主体描述] + [动作/姿态] + [环境/背景] + [光影/氛围] + [风格/质量词] + [镜头语言]
```

### 有效的风格控制词

| 类别 | 关键词示例 |
|------|-----------|
| 画质 | masterpiece, best quality, ultra-detailed, 8K |
| 动漫风 | anime style, cel shading, vibrant colors |
| 写实风 | photorealistic, hyperrealistic, studio photography |
| 光影 | dramatic lighting, cinematic lighting, golden hour, volumetric light |
| 镜头 | close-up, wide angle, depth of field, bokeh |
| 氛围 | moody, warm tone, cold tone, noir |

### 常用负面提示词

```
low quality, blurry, deformed, extra fingers, extra limbs,
bad anatomy, bad proportions, watermark, text,
logo, signature, cropped, out of frame,
worst quality, jpeg artifacts, duplicate
```

### Prompt 长度建议

- 正向 prompt：150-350 字符效果最佳，超过 500 字符权重会稀释
- 负面 prompt：50-150 字符，覆盖常见缺陷即可
- 过长的 prompt 会导致模型"选择性忽略"部分描述

---

## 一致性控制策略

### Seed 控制

- 相同 prompt + 相同 seed → 高度相似的输出
- 改变 prompt 细节但保持 seed → 轻微变化
- 用途：同一场景不同角度、同一角色不同表情

### 参考图控制

- img2img 模式下，`strength` 参数控制变化程度：
  - 0.1-0.3：微调（颜色/光影变化，构图基本不变）
  - 0.4-0.6：中度变化（可改变表情/姿态，保持角色特征）
  - 0.7-0.9：大幅变化（仅保留大致构图，重新生成细节）

### 角色一致性建议

1. **固定 canonical prompt 核心段**：每个镜头的角色描述保持相同的核心词汇
2. **使用 img2img 延续**：生成满意的角色图后，后续镜头以此为参考
3. **seed 组策略**：同场景的多个镜头使用相近的 seed 值

---

## 常见问题与对策

| 问题 | 对策 |
|------|------|
| 多余手指/肢体 | 在负面 prompt 中加强：extra fingers, extra limbs, bad hands |
| 角色外貌不一致 | 锁定 canonical prompt 核心段 + img2img 参考 |
| 背景文字/水印 | 负面 prompt 加：text, watermark, logo, sign |
| 人物过于正中 | prompt 中明确构图位置：standing on the left third |
| 光影不匹配 | 在 prompt 中明确光源方向和类型 |
| 画面过于拥挤 | 减少 prompt 中的元素数量，聚焦关键主体 |
