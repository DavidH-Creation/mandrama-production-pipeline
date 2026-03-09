# Project Spec

> 由 `format-style-planner` 输出，供 `script-asset-breakdown`、`storyboard-shot-planner`、`model-prompt-adapter-jimeng` 消费。

---

## 项目基本信息

```yaml
project_name: ""
genre: ""            # 题材：都市/古装/玄幻/悬疑/甜宠/逆袭/...
logline: ""          # 一句话概要
total_episodes: 0
episode_duration_sec: 0   # 单集目标时长（秒）
```

## 目标平台

```yaml
primary_platform: ""      # 抖音 / 快手 / YouTube Shorts / B站 / 微信视频号
secondary_platforms: []   # 可选次要平台
```

## 画幅与分辨率

```yaml
aspect_ratio: ""          # 9:16 / 16:9 / 1:1
resolution: ""            # 1080x1920 / 1920x1080 / 1080x1080
safe_zone_notes: ""       # 安全区备注（标题遮挡区、互动按钮区）
```

## 视觉风格

```yaml
style_route: ""           # 2D插画 / 3D渲染 / 真人仿真3D / 动态漫画 / 混合
style_substyle: ""        # 进一步细分：赛璐璐/厚涂/写实CG/半写实/...
```

## 色调与光影

```yaml
primary_palette: []       # 主色调，3-5个色彩关键词或色值
secondary_palette: []     # 辅助色
lighting_style: ""        # 高对比 / 柔光 / 赛博霓虹 / 自然光 / 影棚 / 黄金时段
texture: ""               # 胶片颗粒 / 干净数码 / 水彩 / 漫画网点 / 磨砂质感
```

## 视觉参考关键词

> 5-8 个关键词，后续用于 prompt 中的风格控制。

```yaml
visual_keywords:
  - ""
  - ""
  - ""
  - ""
  - ""
```

## 受众画像

```yaml
target_age: ""            # 18-24 / 25-34 / 全年龄 / ...
target_gender: ""         # 女性向 / 男性向 / 中性
target_region: ""         # 国内 / 出海-英语市场 / 出海-日本市场 / ...
```

## 产能约束

```yaml
budget_level: ""          # 低 / 中 / 高
turnaround: ""            # 快速（日更）/ 平衡（周更）/ 精品（月更）
ai_pipeline: []           # 使用的AI工具：即梦 / Midjourney / ComfyUI / ...
```

## 决策记录

| 决策项 | 选择 | 理由 | 排除项 |
|--------|------|------|--------|
| 视觉风格 | | | |
| 画幅比例 | | | |
| 主色调 | | | |

## 备注

> 任何补充说明、用户特殊要求、已知限制。
