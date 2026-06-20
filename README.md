# ljg-skill-explain-words

单词灵魂解剖师 (Word Soul Master) — 一个 [Claude Code](https://docs.anthropic.com/en/docs/claude-code) Skill，深度解构一个词的核心语义，直击词的灵魂。**支持中英双语**：输入中文或英文皆可，输出「中文」与「English」两个母语级版本。

## 功能

- 双语解构：「中文」「English」两个区块，各为母语级原创解释（非互译）
- 核心语义：原始画面 + 核心意象公式 + 深层解释
- 反向查词 (reverse lookup)：输入中文词，自动给出最贴切的英文对应词再深度解构（例：缘分 → serendipity）
- 一语道破：每个区块各一句独立的中英双语哲学金句
- 直接在对话中 Markdown 输出，轻量无依赖

## 安装

```bash
/plugin marketplace add mikezhang09-code/ljg-skill-explain-words-bilingual
/plugin install ljg-explain-words
```

## 使用

在 Claude Code 中输入（英文或中文皆可）：

```
/ljg-explain-words Serendipity
/ljg-explain-words 缘分
```

## 输出示例

输入一个词后，输出「中文」「English」两个区块（节选）：

```
## 中文

### serendipity /ˌserənˈdɪpəti/ 机缘巧合；意外发现珍宝的能力

- 原始画面：三位锡兰（Serendip）王子在旅途中，总能从看似无关的线索里
  推断出自己并未寻找的真相。
- 核心意象：不刻意寻找 + 敏锐的眼睛 + 偶然的相遇 = 命运的馈赠
- 解释：serendipity 不是单纯的"运气"。运气是**被动**地撞上好事；它则是
  当幸运降临时，你**有能力认出它**……

> "You cannot search for serendipity; you can only become worthy of it.
> 机缘无法被搜寻，只能被配得上。"

## English

### serendipity /ˌserənˈdɪpəti/ — 机缘巧合

- Original Image: three princes of *Serendip* who keep deducing things
  they were never looking for.
- Core Metaphor: not seeking + a sharp eye + a chance encounter = a gift
  you didn't ask for
- Insight: coined by Horace Walpole in 1754. Serendipity is not luck —
  luck is **passive**; this is the **active faculty** of recognizing
  fortune when it arrives by accident…

> "Chance favors the connected mind. 偶然，偏爱善于联结的头脑。"
```

## License

MIT
