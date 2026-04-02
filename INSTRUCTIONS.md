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

1. **Read this repo** — understand existing topics, concepts and structure before writing anything.
2. **Analyze the YouTube video** — extract summary, key ideas, concepts, actions and open questions.
3. **Check existing files** in `concepts/` and `topics/` to avoid duplicates and reuse existing slugs.
4. **Push the following files** to this repo:
   - `sources/youtube/YYYY/MM/<video-id>.md` — one source note per video
   - `concepts/<concept-slug>.md` — one per **new** concept (skip if exists, add source reference if it does)
   - `topics/<topic-slug>.md` — one per **new** topic (skip if exists)
5. **Confirm** to the user which files were created or updated.

---

## File formats

### Source note — `sources/youtube/YYYY/MM/<video-id>.md`

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
  - "video-id"
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
- [[video-id]]
```

---

## Controlled topic list

Only use topics from this list. Add your own domains here. If nothing fits, use `other`.

```
defi, solidity, uniswap, ai-agents, trading, market-structure,
infrastructure, security, tokenomics, blockchain, frontend, backend,
research, economics, psychology, productivity, other
```

> ✨ **Customize this list** to match your knowledge domains.

---

## Rules

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
sources/youtube/YYYY/MM/<video-id>.md
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
