# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

A **Claude Code Skill plugin** ("单词灵魂解剖师" / Word Soul Master) that deconstructs a single word — **English or Chinese** — into its core semantics and a bilingual epiphany. There is no application code, build, lint, or test — the entire product is a prompt. "Running" it means installing the plugin into Claude Code and invoking `/ljg-explain-words <word>`.

The long-term plan (not yet built) is to wrap this skill in a dead-simple, Google-style single-box **mobile dictionary** app. Phase 1 (current) is making the skill bilingual; keep the skill's output structurally stable so it can later be parsed/cached into app cards without rework.

## Repository layout

- `skills/ljg-explain-words/SKILL.md` — **the actual product.** YAML frontmatter (`name`, `description`) controls when the skill triggers; the Markdown body is the prompt that defines the output. Editing the skill = editing this file.
- `.claude-plugin/plugin.json` — plugin manifest (name, author).
- `.claude-plugin/marketplace.json` — marketplace manifest; `plugins[].source: "./"` points at this repo root.
- `README.md` — install/usage docs (Chinese).

Install/usage (from README):
```
/plugin marketplace add lijigang/ljg-skill-explain-words
/plugin install ljg-explain-words
/ljg-explain-words Serendipity
```

## The output contract (SKILL.md body)

This is the spec — changes to behavior must preserve or deliberately revise this structure. Output is Markdown emitted directly into the conversation (no files, no HTML), authored as a "语言哲学大师" voice. The skill **auto-detects input language** and always emits **two parallel sections in a fixed order**, `## 中文` then `## English`. The two are *native deconstructions of the same meaning, not translations of each other*. Those two `##` headers are the stable split points the future app will parse on — keep them verbatim.

Each section contains:

1. **Headword line** — `### {word}  /{IPA or pinyin}/  {中文释义}`
2. **核心语义 / core semantics** — `原始画面` / `Original Image` (most physical etymological image) + `核心意象` / `Core Metaphor` (a "X + Y = Z" formula) + an insight-driven `解释` / `Insight` with **bolded** keywords (English side traces Latin/Greek/Old English roots).
3. **一语道破 / epiphany** — one bilingual aphorism in a `>` blockquote. The two sections carry **distinct** aphorisms (different angles), not the same one twice.

**Cross-language / reverse lookup:** when input and section language differ, the section uses the truest equivalent word as its headword (e.g. Chinese input `缘分` → the English section deep-dives `serendipity / affinity / fated connection`).

## Gotcha to respect

- **Scope boundary / sibling skill.** This skill is for a *single word* (English or Chinese). Its `description` delegates **multi-word concepts and ideas** to a separate skill, `ljg-explain-concept` — that's the line, single lexical item vs. multi-word idea. Preserve it in the `description` (it's what Claude uses to route), and don't broaden this skill to cover concepts.

> Note: an earlier inconsistency (manifests describing removed "Museum Quality HTML cards / nuance spectrum / visual topology") has been reconciled — `plugin.json` / `marketplace.json` now match the bilingual markdown behavior. `SKILL.md` remains authoritative; keep the manifests in sync on future behavior changes.
