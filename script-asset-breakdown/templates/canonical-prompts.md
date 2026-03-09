# Canonical Prompts

> 由 `script-asset-breakdown` 输出，供 `model-prompt-adapter-jimeng` 消费。
> 每个资产对应一段标准化的英文视觉描述，作为生图时的一致性锚点。

---

## 使用说明

- **核心描述（core）**：每次引用该资产时必须包含，确保跨镜头一致性
- **状态变体（variants）**：特定场景追加，覆盖或补充核心描述的部分特征
- 所有描述使用英文，因为主流生图模型对英文 prompt 效果更好
- 句式保持统一，便于拼接到镜头 prompt 中

---

## 角色 Canonical Prompts

### [C01] — [角色名]

**Core prompt:**
```
[标准化英文外貌描述，包含面部特征、发型发色、体型、标志性特征]
```

**Outfit variants:**
```yaml
C01-O1 (日常装): "[服装描述英文]"
C01-O2 (职业装): "[服装描述英文]"
```

**Expression variants:**
```yaml
neutral: "[默认表情描述]"
angry: "[愤怒表情描述]"
sad: "[悲伤表情描述]"
```

---

*(为每个角色重复以上结构)*

---

## 场景 Canonical Prompts

### [L01] — [场景名]

**Core prompt:**
```
[标准化英文环境描述，包含空间类型、光照、氛围、关键视觉元素]
```

**Time variants:**
```yaml
daytime: "[白天变体]"
night: "[夜晚变体]"
sunset: "[黄昏变体]"
```

---

*(为每个场景重复以上结构)*

---

## 道具 Canonical Prompts

### [P01] — [道具名]

**Core prompt:**
```
[标准化英文道具描述]
```

**State variants:**
```yaml
intact: "[完好状态]"
damaged: "[损坏状态]"
```

---

*(为每个关键道具重复以上结构)*

---

## Prompt 拼接示例

生成镜头 prompt 时的拼接顺序参考：

```
[场景 core prompt], [角色 core prompt], [角色 outfit variant], [角色 expression variant], [镜头特有描述], [风格关键词]
```
