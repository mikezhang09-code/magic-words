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

Each card contains five beats plus a chant:

1. **Headword line** — `### {word}  /{IPA or pinyin}/  {一句话给小朋友的意思 / kid-friendly gloss}`
2. 🎬 **看见画面 / See It** — the word's most fun, concrete mini-cartoon (the etymological image, story-fied), with emoji.
3. ✨ **魔法公式 / Magic Formula** — a silly, sticky "X + Y = Z" formula.
4. 🪄 **记忆咒语 / Memory Spell** — one sound-game/mnemonic (rhyme, "sounds like…", a hidden little word).
5. 🗣️ **用一用 / Use It** — one example sentence from a kid's real day.
6. 🎯 **小挑战 / Mini Quest** — a light task or question inviting the child to speak/act.
7. **Chant** — one bilingual fun口诀 in a `>` blockquote. The two cards carry **distinct** chants (different angles), not the same one twice.

**Cross-language / reverse lookup:** when input and card language differ, the card uses the truest kid-appropriate equivalent word as its headword (e.g. Chinese input `勇敢` → the English card teaches `brave`).

**Auto-scale:** dial complexity by word difficulty — simpler/younger words lean cuter and sillier with almost no etymology; harder/older words may carry a real mini-story and a light touch of the word's "老家" (origin). Always stay encouraging.

## Gotcha to respect

- **Scope boundary / sibling skill.** This skill is for a *single word* (English or Chinese). Its `description` delegates **multi-word concepts and ideas** to a separate skill, `ljg-explain-concept` — that's the line, single lexical item vs. multi-word idea. Preserve it in the `description` (it's what Claude uses to route), and don't broaden this skill to cover concepts.

> Note: this repo was forked from the adult "Word Soul Master" and rebuilt as a **new, independent** kid skill named `magic-words` (command `/magic-words`, marketplace `1.0.0`) — *not* a new version of `ljg-explain-words`, which is published separately and stays installed. The skill id, both manifests, `README.md`, and this file were all renamed off the `ljg-` prefix; only the sibling-delegation reference to `ljg-explain-concept` intentionally remains. `SKILL.md` is authoritative; keep the manifests and README in sync on future behavior changes.
