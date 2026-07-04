# magic-words

单词魔法师 (Word Wizard) — 一个给小朋友的 [Claude Code](https://docs.anthropic.com/en/docs/claude-code) Skill。它把一个词变成**一幅画 + 一个搞笑公式 + 一句记忆咒语 + 一个小挑战**，让孩子"啊哈"一声就记住。**支持中英双语**：输入中文或英文皆可，输出「中文」与「English」两张母语级卡片，难度随词自动调节（适合约 4–12 岁）。

## 功能 (v1.1)

- 🪄 **魔法师口吻**：好玩、温暖、爱欢呼，绝不说教。
- 🎬 **看见画面**：每个词都变成一幅好玩的小动画。**遵循语言特定的“真实来源”**：中文卡优先拆解字形故事（象形/会意，如“休” = 🧍人靠在🌳树旁休息），英文卡讲解真实的词源（Word's Home）。对拿不准的词源一律以“想象一下…”/“Imagine...”开头，绝不把假知识教给孩子。
- 🧪 **魔法公式**：把意思熬成一锅傻气好记的魔药（emoji ＋ emoji ＝ emoji 结果）。**加数必须是配料或原因，绝不能是近义词**（如：😨怕怕 ＋ 🚶还是去 ＝ 💪勇敢）。
- ✨ **记忆咒语**：押韵、能大声喊出来的两行小口诀，**咒语中必须包含目标词本身**（或完整谐音）以作记忆锚点，且中英两张卡片采用两句独立不同的咒语。
- 🔤 **拼读发音**：为孩子提供直接可读的拼读版（school → skool，curious → KYOOR-ee-us），重音用大写；国际音标留给大人。
- 💬 **用一用 ｜ 双语翻译**：源于孩子日常生活的例句，并附带另一语言的翻译。
- 🎯 **小挑战**：设计一个轻松、孩子能立即动嘴或动手完成的小任务。
- 🌏 **双语 & 反向查词**：输入中文或英文，自动查找最贴切的跨语言对应词，并输出中文与 English 两张卡片。
- 🎚️ **自动调节与年龄提示**：难度随词难度自动调节（适合 4–12 岁）。**支持在输入中显式提供年龄提示**（如 `brave 5岁`）来覆盖自动难度。
- 🧑‍🎓 **闪回复习（v1.1 新增）**：单次对话中学习多个单词时，在新词开始前会花两秒钟快速闪回复习上一个单词，答不上来时会给予首音提示。
- 🔒 **封印仪式（v1.1 新增）**：当孩子回答小挑战后，针对回答进行具体欢呼（而不是泛泛夸奖），并引导孩子大声喊出目标词进行“封印”，锁定记忆。
- 🛡️ **敏感词与一词多义（v1.1 新增）**：多义词仅教授孩子最常用的一项意思（好玩的第二义可在小挑战中作为彩蛋）；若输入敏感词（如粗话），魔法师会温和拒绝并推荐新词，不解释也不重复输入词。
- 🪶 直接在对话中 Markdown 输出，轻量无依赖。

## 安装

```bash
/plugin marketplace add mikezhang09-code/magic-words
/plugin install magic-words
```

## 使用

在 Claude Code 中输入（英文或中文皆可）：

```
/magic-words brave
/magic-words 勇敢
```

## 输出示例

输入一个词后，输出「中文」「English」两张卡片（节选）：

```
## 中文

### 勇敢 /yǒng gǎn/ — brave

🎬 想象一下：🦁 一只小狮子虽然腿在发抖，可还是抬起头，朝着大大的黑山洞一步步走了进去。
🧪 😨怕怕 ＋ 🚶还是去 ＝ 💪勇敢
✨ 战胜了怕怕，大声喊**勇敢**！ ／ 迈出第一步，小手攥得紧！
💬 第一次自己睡觉，我有点怕，但我很勇敢。 ｜ The first time I slept alone I was a bit scared, but I was brave.
🎯 你能说一件让你觉得自己很勇敢的事吗？

## English

### brave /breɪv/ · say it: BRAYV — 勇敢

🎬 Imagine: 🦁 a tiny lion, knees shaking, lifts its chin and walks right into the big dark cave.
🧪 😨scared ＋ 🚶go anyway ＝ 💪brave
✨ Knees can shake, but I am **brave**! ／ Into the cave, a big step I made!
💬 I was scared on the high slide, but I was brave and went down. ｜ 高滑梯让我害怕，但我很勇敢，滑了下去。
🎯 Strike your bravest superhero pose — what are you brave enough to try today?
```

## 致谢 Credits

灵感来自 [lijigang](https://github.com/lijigang) 的原作 **单词灵魂解剖师 (Word Soul Master)** —— 一个面向成人的深度词源解构 Skill。本项目是它的**儿童版独立衍生作品**：保留"词源即画面"的内核，重写为给小朋友的魔法师口吻。原版仍独立存在、各自安装互不影响。

Inspired by [lijigang](https://github.com/lijigang)'s original **Word Soul Master** (单词灵魂解剖师), a deep etymological deconstruction skill for adults. This is a standalone **kids' derivative** — it keeps the "etymology-as-picture" core and rewrites it in a playful Word Wizard voice. The original remains separate; the two install side by side without conflict.

## License

MIT
