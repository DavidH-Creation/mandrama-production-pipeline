# Prompt 模式库 — 已验证有效模式

> `model-prompt-adapter-jimeng` Step 3 遇到特定场景类型时读取本文件，查已验证有效的 prompt 模式。

---

## 使用方式

本文件收录已在即梦上验证有效的 prompt 模式。使用时：
1. 找到与当前镜头类型最接近的模式
2. 替换 `{占位符}` 为具体的 canonical prompt 片段
3. 根据镜头需求调整细节

---

## 角色特写模式

### 情绪特写

```
{角色 canonical prompt core}, {表情 variant},
extreme close-up shot, shallow depth of field,
{光影描述}, {氛围关键词},
masterpiece, best quality, ultra-detailed
```

**负面模板：**
```
blurry, low quality, bad anatomy, extra fingers, watermark, text
```

### 侧脸/半侧脸特写

```
{角色 canonical prompt core}, {表情},
profile view / three-quarter view, looking {方向},
{光影描述}, cinematic composition,
masterpiece, best quality
```

---

## 对话场景模式

### 正反打 A（说话者）

```
{角色A canonical prompt core}, {outfit variant}, {expression variant},
medium close-up, facing camera, speaking,
{场景简要背景描述},
soft focus background, warm lighting,
masterpiece, best quality
```

### 正反打 B（听者/反应）

```
{角色B canonical prompt core}, {outfit variant}, {reaction expression},
medium close-up, over-the-shoulder composition,
blurred {角色A} silhouette in foreground,
{场景简要背景描述},
masterpiece, best quality
```

---

## 全景/建立镜头模式

### 室内全景

```
{场景 canonical prompt core},
wide shot, establishing shot, no people / {角色站位描述},
{时间光照 variant},
detailed interior, atmospheric perspective,
masterpiece, best quality, 8k
```

### 室外全景

```
{场景 canonical prompt core},
wide shot, panoramic view,
{天气描述}, {时间光照},
cinematic composition, epic scale,
masterpiece, best quality, 8k
```

---

## 动作/冲突场景模式

### 肢体冲突

```
{角色A canonical prompt}, {角色B canonical prompt},
{动作描述}, dynamic pose, motion blur,
medium shot, dutch angle,
dramatic lighting, high contrast,
intense atmosphere,
masterpiece, best quality
```

### 追逐/移动

```
{角色 canonical prompt}, running / walking fast,
{场景背景描述},
tracking shot composition, motion blur on background,
{光影描述},
masterpiece, best quality
```

---

## 情绪氛围模式

### 温馨/暖调

```
{画面内容描述},
warm golden light, soft glow, cozy atmosphere,
warm color palette, gentle shadows,
masterpiece, best quality
```

### 紧张/冷调

```
{画面内容描述},
cold blue-gray lighting, harsh shadows, tense atmosphere,
desaturated colors, high contrast,
masterpiece, best quality
```

### 悲伤/低沉

```
{画面内容描述},
dim lighting, overcast, muted colors,
melancholic atmosphere, soft rain / gray sky,
masterpiece, best quality
```

### 惊艳/华丽

```
{画面内容描述},
dramatic backlight, lens flare, particle effects,
vibrant saturated colors, cinematic lighting,
masterpiece, best quality, 8k
```

---

## 竖屏构图模式

### 竖屏角色居中

```
{角色 canonical prompt}, {outfit}, {expression},
centered composition, full body / upper body,
{背景描述},
portrait orientation, vertical frame,
masterpiece, best quality
```

### 竖屏上下分层

```
{上方元素描述} on top,
{中部角色描述} in center,
{下方元素描述} at bottom,
layered vertical composition,
masterpiece, best quality
```

---

## 视频生成提示模式

### 静态到微动（图生视频）

```
{画面内容描述},
subtle movement, gentle breeze, hair flowing,
slow camera push in,
cinematic, smooth motion
```

### 角色动作（文生视频）

```
{角色描述}, {具体动作，用动态动词},
{场景背景},
smooth animation, natural movement,
cinematic quality
```

**视频 prompt 注意：**
- 动作描述用简单明确的动词，避免复杂动作链
- 一个视频片段（4s）只描述一个主要动作
- 避免描述快速场景切换（模型无法处理）
