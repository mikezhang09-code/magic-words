# magic-words

单词魔法师 (Word Wizard) — 一个给小朋友的 [Claude Code](https://docs.anthropic.com/en/docs/claude-code) Skill。它把一个词变成**一幅画 + 一个搞笑公式 + 一句记忆咒语 + 一个小挑战**，让孩子"啊哈"一声就记住。**支持中英双语**：输入中文或英文皆可，输出「中文」与「English」两张母语级卡片，难度随词自动调节（适合约 4–12 岁）。

## 功能

- 🪄 魔法师口吻：好玩、温暖、爱欢呼，绝不说教
- 🎬 看见画面：每个词都先变成一幅好玩的小动画（**真实的词源故事**；编的会说"我们想象一下"，绝不把瞎编当真知识教）
- ✨ 魔法公式 + 记忆咒语：傻气好记的公式和声音游戏，一秒记住
- 🔤 拼读发音：给小朋友一个能直接读出来的拼读版（school → skool，curious → KYOOR-ee-us），音标留给大人
- 🎤 顺口溜口诀：短、押韵、能跟着喊出来——是顺口溜，不是大道理
- 🗣️ 用一用 + 🎯 小挑战：身边的例子 + 一个邀请孩子开口的小任务
- 🌏 双语 & 反向查词：输入中文自动给出最贴切的英文词再讲解（例：勇敢 → brave）
- 🎚️ 自动调节难度：简单词更可爱傻气，较难词加一点小故事和来源
- 直接在对话中 Markdown 输出，轻量无依赖

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

### brave /breɪv/ 勇敢——心里有点怕，但还是去做了

- 🎬 看见画面：🦁 一只小狮子腿在发抖，可还是抬起头，朝着大大的黑山洞走了进去。
- ✨ 魔法公式：怕怕 😨 + 还是去 🚶 + 抬起头 🦁 = 勇敢 💪
- 🪄 记忆咒语："brave" 听起来像"不累"——勇敢的人心里累，腿也累，可还是不放弃！
- 🗣️ 用一用：第一次自己睡觉，我有点怕，但我很 brave。
- 🎯 小挑战：你能说一件让你觉得自己很勇敢的事吗？

> "腿在抖，心在跳，迈出一步就英豪！Knees go shake, heart goes quake — one big step is all it takes!"

## English

### brave /breɪv/ · say it: BRAYV — 勇敢

- 🎬 See It: 🦁 a tiny lion, knees shaking, lifts its chin and walks right into the big dark cave.
- ✨ Magic Formula: scared 😨 + go anyway 🚶 + chin up 🦁 = brave 💪
- 🪄 Memory Spell: a brave kid is "brrr… AVE!" — you shiver (brrr) but still shout hooray (ave)!
- 🗣️ Use It: I was scared on the high slide, but I was brave and went down.
- 🎯 Mini Quest: Strike your bravest superhero pose — what are you brave enough to try today?

> "Wobble, wobble, BRAYV! Take the step and be so brave! 抖一抖，喊一声，勇敢迈步往前冲！"
```

## 致谢 Credits

灵感来自 [lijigang](https://github.com/lijigang) 的原作 **单词灵魂解剖师 (Word Soul Master)** —— 一个面向成人的深度词源解构 Skill。本项目是它的**儿童版独立衍生作品**：保留"词源即画面"的内核，重写为给小朋友的魔法师口吻。原版仍独立存在、各自安装互不影响。

Inspired by [lijigang](https://github.com/lijigang)'s original **Word Soul Master** (单词灵魂解剖师), a deep etymological deconstruction skill for adults. This is a standalone **kids' derivative** — it keeps the "etymology-as-picture" core and rewrites it in a playful Word Wizard voice. The original remains separate; the two install side by side without conflict.

## License

MIT
