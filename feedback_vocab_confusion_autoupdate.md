---
name: vocab-confusion-autoupdate
description: "User maintains a master vocabulary-confusion file on Desktop; every time they ask a word comparison (\"A vs B\", \"A 和 B 区别\", etc.), auto-append a new entry to it"
metadata: 
  node_type: memory
  type: feedback
  originSessionId: bf9065ff-7965-404e-9793-67aa31d0a021
---

# 易混词辨析手册 — 自动追加规则

**文件位置**:`C:\Users\y3264\Desktop\英语易混词辨析.md`

**触发条件** —— 用户问以下任一类型的问题时,**回答的同时必须追加到文件**(不必再次询问确认):
- "A vs B" / "A 和 B 区别" / "A 跟 B 有什么不同" / "A vs B 什么区别"
- 涉及两个或多个英文单词的辨析、对比、用法区别
- 用户拼错也算(如 svarce → scarce)

**追加位置**:文件末尾的 `<!-- 新词条追加到此行之后 -->` 注释**之前**,新词条紧贴该注释。

**追加流程**:
1. Read 当前文件,拿到现有词条数
2. 在目录(`## 目录`)末尾追加新链接 `N+1. [A vs B](#N1-a-vs-b)`
3. 更新顶部"最后更新"日期和"词条数"
4. 在末尾追加新词条,严格按以下模板
5. 保留末尾 `<!-- 新词条追加到此行之后 -->` 标记

**模板**(必须遵守):

```markdown
## N. word1 vs word2

**核心区别**:[一句话,15字内]

**视觉**:
\`\`\`
[ASCII 对比,简洁]
\`\`\`

### 使用场景

| 场景 | 用 |
|------|----|
| ... | **wordX** — 例句 |
(至少 6 行,涵盖典型 + 边缘场景)

### 一句话口诀

> **核心对比**。
> [一句生活化的对照]。

---
```

**风格要求**(对应用户偏好):
- 中文为主,英文例句保留原形
- 必须有视觉对比(ASCII / 表格 / 时间轴)
- 必须有"使用场景表"和"一句话口诀"
- 用户词汇量 9035,**不要解释基础词** —— 直接对比、不要 padding
- 用户的真盲点是**熟词冷义**(felt = 毛毡那种),如果两词中有这类陷阱要标出

**告知用户**:追加完后只需简短确认(如"已追加到第 N 条"),不必重复文件全文。
