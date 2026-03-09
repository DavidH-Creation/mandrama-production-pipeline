# Canonical Prompt 编写指南

> `script-asset-breakdown` Step 4 读取本文件，确保每个资产的标准化描述格式统一。

---

## 什么是 Canonical Prompt

Canonical prompt 是为每个视觉资产（角色/场景/道具）编写的一段标准化英文描述。它的作用是：

- **一致性锚点**：后续所有镜头引用该资产时，都从 canonical prompt 中提取描述片段，确保角色/场景外观跨镜头一致
- **拼接基础**：`model-prompt-adapter-jimeng` 会将 canonical prompt 片段拼接到每个镜头的完整 prompt 中

---

## 编写规则

### 语言

使用英文。主流生图模型（即梦/Midjourney/SDXL）对英文 prompt 的理解和生成质量显著优于中文。

### 结构

每个 canonical prompt 分为两部分：

1. **Core prompt**：每次引用该资产时必须包含的核心特征
2. **Variants**：特定场景下追加或替换的变体描述

### 句式规范

- 使用逗号分隔的描述性短语，不用完整句子
- 从最重要的特征开始，按重要性递减排列
- 避免叙事性语言（不要写"她走进房间"，只写外观特征）
- 避免情绪化形容（不要写"beautiful"、"handsome"，写具体特征）

---

## 角色 Canonical Prompt 模板

### Core Prompt 结构

```
[性别], [年龄段], [体型], [面部特征], [发型发色], [肤色], [标志性特征]
```

**示例：**
```
young woman, early 20s, slim build, oval face, large expressive eyes,
long straight black hair with bangs, fair skin, small mole below left eye
```

**反例（不要这样写）：**
```
A beautiful young girl who looks mysterious and elegant  ← 太笼统，没有具体特征
```

### Outfit Variant 结构

```
wearing [服装类型], [颜色], [材质], [关键细节]
```

**示例：**
```
wearing tailored navy blue blazer over white blouse, black pencil skirt,
pearl earrings, black stiletto heels
```

### Expression Variant 结构

```
[表情描述], [关联的面部动作]
```

**示例：**
```
angry expression, furrowed brows, clenched jaw, intense glare
```

---

## 场景 Canonical Prompt 模板

### Core Prompt 结构

```
[空间类型], [具体场景], [光照], [氛围关键词], [关键视觉元素]
```

**示例：**
```
modern office interior, floor-to-ceiling windows with city skyline view,
bright natural daylight, clean minimalist design, glass desk,
potted plants, warm wood accents
```

### Time Variant 结构

```
[时间条件], [光照变化], [氛围变化]
```

**示例：**
```
nighttime, city lights visible through windows, warm desk lamp glow,
dim ambient lighting, lonely atmosphere
```

---

## 道具 Canonical Prompt 模板

```
[物品名称], [材质], [颜色], [尺寸], [关键细节], [状态]
```

**示例：**
```
antique jade pendant, translucent green jade, gold chain,
small size fits in palm, intricate dragon carving, slight crack on edge
```

---

## 风格适配

canonical prompt 的措辞应匹配 project-spec 中的视觉风格：

| 视觉风格 | 措辞特点 |
|----------|----------|
| 2D 赛璐璃/动漫 | 可用 anime-style、cel-shaded 等前缀；发色/瞳色可用非自然色（粉色、紫色） |
| 厚涂/半写实 | 用 painted、rich texture 等；特征描述更注重色彩层次 |
| 3D 写实/真人仿真 | 用 realistic、photorealistic 等前缀；发色/肤色必须自然 |

---

## 拼接示例

生成一个镜头 prompt 时，从各 canonical prompt 中提取片段拼接：

```
[场景 core] + [角色 core] + [角色 outfit variant] + [角色 expression variant] + [镜头独有描述] + [风格关键词]
```

**完整示例：**
```
modern office interior, floor-to-ceiling windows with city skyline view,
bright natural daylight, clean minimalist design,
young woman, early 20s, slim build, long straight black hair with bangs,
wearing tailored navy blue blazer over white blouse,
angry expression, furrowed brows, clenched jaw,
standing at glass desk slamming documents down,
close-up shot, dramatic lighting,
photorealistic, cinematic composition, 8k quality
```
