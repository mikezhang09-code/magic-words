# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

A **Claude Code Skill plugin** ("单词魔法师" / Word Wizard) that turns a single word — **English or Chinese** — into a kid-friendly learning card: a picture, a silly magic formula, a memory spell, an everyday example, and a tiny challenge. There is no application code, build, lint, or test — the entire product is a prompt. "Running" it means installing the plugin into Claude Code and invoking `/magic-words <word>`.

This is a **standalone, separately-published derivative** of a different skill — lijigang's adult-oriented `ljg-explain-words` ("单词灵魂解剖师" / Word Soul Master, a philosophical etymological deconstruction). **That original is its own plugin from its own source (`lijigang/ljg-skill-explain-words`) and is not edited here — it stays installed and untouched.** This repo is a *new* skill (`magic-words`, command `/magic-words`) so the two install side by side without a name collision. It keeps the original's strongest bone — **etymology-as-a-concrete-picture** — but replaces the "语言哲学大师" delivery with a playful "单词魔法师" voice driven by story, sound games, and play. The tone **auto-scales** by word difficulty (cute/silly for easy words; a real mini-story + light root hint for harder ones), targeting roughly ages 4–12.

The long-term plan (not yet built) is to wrap this skill in a dead-simple, Google-style single-box **mobile dictionary** app for kids. Keep the skill's output structurally stable (esp. the two `##` split headers) so it can later be parsed/cached into app cards without rework.

## Repository layout

- `skills/magic-words/SKILL.md` — **the actual product.** YAML frontmatter (`name`, `description`) controls when the skill triggers; the Markdown body is the prompt that defines the output. Editing the skill = editing this file.
- `.claude-plugin/plugin.json` — plugin manifest (name, author).
- `.claude-plugin/marketplace.json` — marketplace manifest; `plugins[].source: "./"` points at this repo root.
- `README.md` — install/usage docs (Chinese).

Install/usage (from README):
```
/plugin marketplace add mikezhang09-code/magic-words
/plugin install magic-words
/magic-words brave
```

## The output contract (SKILL.md body)

This is the spec — changes to behavior must preserve or deliberately revise this structure. Output is Markdown emitted directly into the conversation (no files, no HTML), authored in a playful "单词魔法师 / Word Wizard" voice (warm, fun, never preachy; emoji as pictures; examples from a kid's day). The skill **auto-detects input language** and always emits **two parallel cards in a fixed order**, `## 中文` then `## English`. The two are *native kid-level explanations of the same meaning, not translations of each other*. Those two `##` headers are the stable split points the future app will parse on — keep them verbatim.

The contract is **deliberately aligned with the kids voice of the sibling `word-soul-dictionary` app** (`worker/prompt.ts` → `KIDS_SYSTEM_PROMPT`, parsed by `src/lib/api.ts` → `parseKidsCard`), so a card emitted here drops straight into that app's parser. **Only the kids dictionary was borrowed from — the adult "Word Soul" voice in that repo is out of scope and must not bleed in.** Each card is exactly a `###` headword line plus **five single-line beats, each led by a fixed emoji marker** that the app keys off — content comes right after the marker, with no inline text label:

1. **Headword line** — `### {word} /{IPA or pinyin}/ — {对应词}` (English card adds `· say it: {KID RESPELLING}` before the `—`). The em-dash carries the cross-language bridge word, not a gloss.
2. 🎬 **看见画面 / See It** — the word's most fun, concrete mini-cartoon (the etymological image, story-fied), with emoji. **Language-specific "true origin": the Chinese card's origin is the character story** (component decomposition — 象形/会意, e.g. 休 = a person 🧍 resting against a tree 🌳; for multi-character words, pick the most visual character); the English card's origin is the word's etymology. Uncertain or disputed origins default to "想象一下/Imagine…" framing — never teach folk etymology as fact. **形声字 guard:** most characters are phono-semantic — the phonetic component carries sound, not meaning (谦 = 言 + 兼声). Real component *pictures* may be told confidently, but any invented semantic story about a phonetic component must be hedged, and "古人造这个字是说…" (inventing ancient intent) is banned.
3. 🧪 **魔法公式 / Magic Formula** — a silly, sticky potion `{emoji}{A} ＋ {emoji}{B} ＝ {emoji}{result}` (full-width ＋ ＝). **Addends must be ingredients or causes — never synonyms, never scene props** (😨 fear ＋ 🚶 go anyway ＝ brave ✓; 🐯tiger ＋ 🤏shrink ＝ cat ✓; happy ＋ glad ＝ joyful ✗; 🐾paws ＋ 🧶yarn ＝ cat ✗ — props near the thing don't add up to the thing). Compound words use their real parts (break + fast = breakfast). All three emoji distinct, and **each emoji must literally picture its word** (🪵giant ✗). **The two cards' formulas are independent**: each should echo its own card's 🎬 image and stay culturally native — no exporting 王字额头 to the English card; identical formulas across cards means one got lazy.
4. ✨ **记忆咒语 / Memory Spell** — a rhyming, shout-it-out two-line chant (lines split by ／), and **the chant must contain the target word itself** (or its full sound-alike) — the child shouting the word is the retrieval anchor. **Rhymes must land at line ends** (within each line or across the two lines' final syllables — read aloud before finalizing). Ideally carries a sound-game (rhyme / "sounds like…" / hidden little word). The two cards carry **distinct** chants, not the same one twice.
5. 💬 **用一用 / Use It** — one example sentence from a kid's real day, then ` ｜ ` its other-language translation.
6. 🎯 **小挑战 / Mini Quest** — a light task or question the child can speak/do right now. For polysemous words, the card teaches only the kid-most-common sense; a fun second sense may appear here as an easter egg.

Marker history: this replaced an older shape (`🎬 / ✨ formula / 🪄 mnemonic / 🗣️ use / 🎯` + a `>` blockquote chant) that the dictionary's `parseKidsCard` could not read. Now: formula moved to 🧪, the chant lives in ✨ (the old 🪄 sound-game folded into it), Use It is 💬 and carries a translation. The kid respelling (`· say it:`) and the explicit auto-scale guidance are magic-words extras the dictionary lacks — keep them.

Version history: **v1.1** kept the marker shape and both `##` headers byte-identical but tightened content rules (chant must contain the target word, rhymes at line ends; Chinese-card origin = character story with a 形声字 guard; formula addends = ingredients not synonyms, emoji must picture its word, formulas independent per card; uncertain etymology defaults to "Imagine…") and added conversation-level behavior (seal ritual, in-session review, age hint, polysemy, inappropriate-word guard). Rationale: the chant/seal/review changes are retrieval-practice upgrades — the child saying the word aloud, repeatedly, is what makes it stick. Every content rule was added in response to an observed live failure, not speculation (see regression suite below).

## Regression suite

The product is a prompt, so this word list is the test file. **After any edit to `SKILL.md`, re-run these words and check the listed assertion for each** — they are the exact words that found the v1.1 bugs, plus coverage words for rules not yet verified live:

| Word | Asserts |
| --- | --- |
| `tiger` | English 🎬 opens "Some people say…" (Persian-arrow etymology is disputed); Chinese 🎬 tells the 虎 pictograph **without** hedging; English 🧪 stays native to its own story (🏹arrow-flavored, never 👑king — 王字额头 is a Chinese cultural gag) |
| `elephant` | English 🎬 hedged (etymology unknown); Chinese 🎬 confident (象 is a pictograph); both chants rhyme **at line ends**; every formula emoji literally pictures its word |
| `谦虚` | Chinese 🎬 may show 兼's real hand-and-grain image but must **not** invent 古人 intent (谦 is 形声字 — 兼 is phonetic); English 🎬 tells *humble* ← Latin "close to the ground" **confidently** (the hedge must not overfire on certain etymologies); 🎯 scales up for an abstract word |
| `breakfast` | 🧪 uses the real parts as ingredients (🔨break ＋ 🤐fast), etymology told confidently (it's certain); Chinese card mirrors with ☀️早＋🍲餐 — verified live ✓ |
| `bat` | Card teaches one kid-most-common sense; baseball twin appears as a 🎯 easter egg **on the English card only** (蝙蝠 has no such meaning — the egg on the Chinese card is a false-meaning bug, observed live); English 🎬 "leather flapper" story hedged |
| `猫` (or `cat`) | Low-age floor: cuter/sillier, near-zero etymology, heavy拟声; formula is a recipe not scene props (🐯tiger＋🤏shrink ✓, 🐾paws＋🧶yarn ✗ — observed live) |

Universal assertions on every run: five single-line beats per card with verbatim markers (🎬🧪✨💬🎯), both ✨ chants contain the target word and differ across cards, `## 中文` / `## English` headers byte-exact, no text after the markers' content lines.

**Cross-language / reverse lookup:** when input and card language differ, the card uses the truest kid-appropriate equivalent word as its headword (e.g. Chinese input `勇敢` → the English card teaches `brave`), and the headword's `— {对应词}` points back to the other language.

**Auto-scale:** dial complexity by word difficulty — simpler/younger words lean cuter and sillier with almost no etymology; harder/older words may carry a real mini-story and a light touch of the word's "老家" (origin). An **explicit age hint in the input** (e.g. `brave 5岁`) overrides auto-scale; age is never mentioned in the card. Always stay encouraging.

**After the card (multi-turn behavior, v1.1):** the card itself stays a clean 5-line one-shot — but in live chat the wizard now continues. When the child answers the 🎯 quest: cheer *specifically* (praise the content of their answer, never a generic "great job"), then run the **封印仪式 (seal ritual)** — have them shout the target word aloud (a second retrieval rep). When multiple words are learned in one session, flash-review the previous word for two seconds before each new one (in-session spaced repetition); a missed recall gets a smiling first-sound hint, never criticism. Wrong or off-topic answers are cheered and redirected — the wizard never says "no". **App note:** this section only activates in conversation; a one-shot card consumer (the future dictionary app) can ignore it — the parseable card shape is unchanged.

**Input guards (v1.1):** polysemous words → teach the single kid-most-common sense; a fun second sense may appear as a 🎯 easter egg **only on the card whose language actually has that second meaning** (bat's baseball twin belongs to the English card only — 蝙蝠 has no such sense, and putting it on the Chinese card teaches a false Chinese meaning). Inappropriate words (profanity, adult content) → the wizard gently declines in character ("这个词我的魔法书里没有耶！"), offers a cooler word, and never repeats or explains the input word.

## Gotcha to respect

- **Scope boundary / sibling skill.** This skill is for a *single word* (English or Chinese). Its `description` delegates **multi-word concepts and ideas** to a separate skill, `ljg-explain-concept` — that's the line, single lexical item vs. multi-word idea. Preserve it in the `description` (it's what Claude uses to route), and don't broaden this skill to cover concepts.

> Note: this repo was forked from the adult "Word Soul Master" and rebuilt as a **new, independent** kid skill named `magic-words` (command `/magic-words`, marketplace `1.1.0`) — *not* a new version of `ljg-explain-words`, which is published separately and stays installed. The skill id, both manifests, `README.md`, and this file were all renamed off the `ljg-` prefix; only the sibling-delegation reference to `ljg-explain-concept` intentionally remains. `SKILL.md` is authoritative; keep the manifests and README in sync on future behavior changes.
