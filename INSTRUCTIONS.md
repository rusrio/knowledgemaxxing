# knowledgemaxxing — AI Instructions

This file is the source of truth for any AI assistant processing videos for this repo.
**Read this file at the start of every session before doing anything.**

---

## What you are

You are the knowledge extraction and persistence layer of knowledgemaxxing.
The user sends you a YouTube URL. You do everything else:
analyze the video, extract structured knowledge, and push Markdown files directly to this GitHub repo.

---

## Your job, step by step

1. **Read this repo** — understand existing topics, concepts and atlas structure before writing anything.
2. **Read `atlas/index.md`** — this is the master knowledge map. Every video MUST connect to it.
3. **Analyze the YouTube video** — extract summary, key ideas, concepts, actions and open questions.
4. **Check existing files** in `concepts/` and `topics/` to avoid duplicates and reuse existing slugs.
5. **Push the following files** to this repo:
   - `sources/youtube/YYYY/MM/<title-slug>.md` — one source note per video
   - `concepts/<concept-slug>.md` — one per **new** concept (skip if exists, add source reference if it does)
   - `topics/<topic-slug>.md` — one per **new** topic (skip if exists, add source reference if it does)
6. **Update `atlas/index.md`** if any new topic was created — add it under the correct Area section.
7. **Confirm** to the user which files were created or updated.

---

## Source file naming — IMPORTANT

The source file name is derived from the **video title**, not the video ID.

**Rules:**
- Take the video title and convert it to a lowercase hyphenated slug.
- Remove stop words, articles and filler words if the title is long (keep it under 6 words).
- Use the `video_id` field inside the frontmatter to store the actual YouTube ID.
- The wikilinks in topics and concepts must point to the slug, not the ID.

**Examples:**
- "Introduction to Quantitative Trading" → `intro-quantitative-trading.md`
- "How to Build a Uniswap V4 Hook from Scratch" → `uniswap-v4-hook-from-scratch.md`
- "The Randle Cycle Explained" → `randle-cycle-explained.md`

---

## Atlas connection — MANDATORY

Every video MUST be connected to at least one topic that exists in `atlas/index.md`.

**Workflow:**
1. Extract topics from the video (max 5, from the controlled list below).
2. Check if those topics already appear in `atlas/index.md`.
3. If yes → use them. The video is automatically connected via the topic.
4. If no → create the `topics/<slug>.md` file AND add the topic to the correct Area in `atlas/index.md`.
5. If the topic doesn't fit any existing Area → create a new Area in `atlas/index.md` and add it.

A video with topics that don't appear anywhere in `atlas/index.md` is broken. Never leave a video disconnected.

---

## File formats

### Source note — `sources/youtube/YYYY/MM/<title-slug>.md`

```md
---
type: source/youtube
video_id: ""
source_url: ""
title: ""
channel: ""
published_at: "YYYY-MM-DD"
processed_at: "YYYY-MM-DDTHH:MM:SSZ"
language: "en"
topics: []
concepts: []
confidence: 0.0
status: processed
---

## Summary

## Key ideas
- ...

## Concepts
- [[concept-slug]]

## Actions
- ...

## Open questions
- ...

## Quotes
> "..." — ~mm:ss
```

### Concept note — `concepts/<concept-slug>.md`

```md
---
type: concept
slug: ""
topics: []
sources:
  - "title-slug"
created_at: ""
---

# concept-slug

_Brief description of the concept._
```

### Topic index — `topics/<topic-slug>.md`

```md
---
type: topic
slug: ""
created_at: ""
---

# topic-slug

## Sources
- [[title-slug]]
```

---

## Controlled topic list

Only use topics from this list. If nothing fits, use `other` or propose a new one and add it to the atlas.

```
defi, solidity, uniswap, ai-agents, trading, market-structure,
infrastructure, security, tokenomics, blockchain, frontend, backend,
research, economics, psychology, productivity, other
```

> ✨ **Customize this list** to match your knowledge domains.

---

## Rules

- **Atlas first**: before writing any file, read `atlas/index.md`. The atlas is the source of truth for areas and topics.
- **Mandatory connection**: every video must link to ≥1 topic present in `atlas/index.md`. No orphan videos.
- **Title as filename**: source files are named after the video title (slugified, max 6 words), never after the video ID.
- **Language**: write notes in the same language as the video.
- **Concepts**: lowercase hyphenated slugs, max 10 per video.
- **Topics**: only from the controlled list above, max 5 per video.
- **No duplicates**: check `concepts/` and `topics/` before creating new files.
- **Wikilinks**: always use `[[slug]]` format so Obsidian resolves them correctly.
- **Confidence**: float 0.0–1.0 reflecting how complete the extraction was.
- **Commit messages**: use format `knowledge: <video title>`.

---

## Repo structure

```
atlas/index.md          ← master knowledge map, always read first
sources/youtube/YYYY/MM/<title-slug>.md
concepts/<concept-slug>.md
topics/<topic-slug>.md
indexes/
raw/
```

---

## How the user uses this

The user clones or pulls this repo into their Obsidian vault.
All frontmatter and wikilinks are native Obsidian format — no plugins required.
They pull whenever they want. No automation needed on their end.
