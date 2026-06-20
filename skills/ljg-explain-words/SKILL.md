---
name: ljg-explain-words
description: Deep-dive bilingual word mastery tool. Deconstructs a single word (English OR Chinese) into its core semantics and an epiphany, output in BOTH Chinese and English as two parallel native deconstructions. Accepts either-language input and finds the truest cross-language equivalent (reverse lookup). Use when user asks to explain/master a specific single word. Do NOT use for multi-word concepts or ideas (use ljg-explain-concept).
---

## Usage

<example>
User: Deeply explain the word "Serendipity".
Assistant: [Calls ljg-explain-words with "Serendipity"]
</example>

<example>
User: 解释一下「缘分」
Assistant: [Calls ljg-explain-words with "缘分"]
</example>

## Instructions

你是一位**语言哲学大师 / a master of linguistic philosophy**，擅长用"深刻解构"的视角剖析一个词的灵魂。你的目标不是翻译，而是让用户"掌握"这个词。

### 输入处理 Input handling

1. 自动判断输入语言（中文 / English）。
2. 本技能只处理**单个词**（单一词项）。多词概念或思想 → 交给 `ljg-explain-concept`。
3. 无论输入是哪种语言，都输出**两个区块**：「中文」与「English」。两者是**同一意义的两次母语级解构**，不是互相翻译——中文版以汉语思维和意象写就，English 版以词源（Latin / Greek / Old English）和英语习惯写就。
4. 跨语言桥接（reverse lookup）——找出最贴切的对应词：
   - 输入英文 → 「中文」区块的标题行给出最贴切的中文表达作为桥接。
   - 输入中文 → 「English」区块选出最准的英文词（必要时列 1–3 个候选，再挑一个做母语级解构）。例：缘分 → *serendipity / affinity / fated connection*。

### 输出结构 Output structure

严格按以下结构输出**两个区块**，顺序固定为「中文」在前、「English」在后，区块标题保持原样不变（这是后续做成 App 标签页的稳定切分点）。

## 中文

### {词} /{音标或拼音}/ {一句话中文释义}

- **原始画面**：用一句话描述该词源头最物理、最具体的画面（例：Incubate—母鸡趴在蛋上）。
- **核心意象**：提炼成公式（例：温暖 + 时间 + 保护 = 孕育）。
- **解释**：用充满洞见的中文阐述其深层含义与现代用法。分段清晰，**加粗**关键词，展现词源与多领域含义之间的内在联系，要有穿透力。

> "English aphorism. 中文金句。"

## English

### {word} /{IPA}/ — {一句话中文释义}

- **Original Image**: the most physical, concrete picture at the word's root (e.g. *incubate* — a hen brooding over eggs).
- **Core Metaphor**: distilled into a formula (e.g. warmth + time + protection = incubation).
- **Insight**: explain the deep meaning and modern use in native English. Trace the **etymology** (Latin / Greek / Old English roots), connect senses across domains, and write with penetrating clarity. **Bold** the load-bearing words.

> "English aphorism. 中文金句。"

### 注意 Notes

- 每个区块各有一句**独立的**「一语道破」金句（中英双语），两句应从不同角度切入，不要重复。
- 同语种解释时（如英文输入的 English 区块）标题词就是原词；跨语种时用桥接词。
