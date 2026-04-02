# 🧠 knowledgemaxxing

> Turn any YouTube URL into structured knowledge — powered by Perplexity AI + GitHub + Obsidian.

## What is this?

**knowledgemaxxing** is a personal knowledge system where you paste a YouTube URL into Perplexity AI, and the knowledge gets automatically extracted, categorized, and pushed to this GitHub repo as structured Markdown files — ready to be pulled into your Obsidian vault.

No backend. No scripts. No automation required. Just you, Perplexity, and Git.

---

## How it works

```
1. You paste a YouTube URL into Perplexity AI
2. Perplexity reads INSTRUCTIONS.md and extracts the knowledge
3. Perplexity pushes structured .md files directly to this repo
4. You run `git pull` and the notes appear in Obsidian
```

---

## Repo structure

```
sources/youtube/YYYY/MM/<video-id>.md   ← one note per video
concepts/<concept-slug>.md              ← atomic concept notes
topics/<topic-slug>.md                  ← topic index pages
indexes/                                ← auto-generated indexes
raw/                                    ← raw JSON from Perplexity (optional)
```

---

## Setup (5 minutes)

### 1. Use this template

Click **"Use this template"** → **"Create a new repository"** on GitHub.
Make it private (recommended) or public.

### 2. Clone into your Obsidian vault

```bash
# Option A: clone directly inside your vault
cd /path/to/your/obsidian-vault
git clone https://github.com/YOUR_USERNAME/YOUR_REPO_NAME knowledge

# Option B: clone anywhere and symlink
git clone https://github.com/YOUR_USERNAME/YOUR_REPO_NAME ~/knowledgemaxxing
```

Or use the [Obsidian Git](https://github.com/denolehov/obsidian-git) plugin to auto-pull on a schedule.

### 3. Connect Perplexity to your repo

Perplexity AI has a native GitHub connector. Connect it to your repo so it can read context and push files.

> **Settings → Connectors → GitHub → connect your repo**

### 4. Start a session

At the beginning of each Perplexity session, say:

```
Read the INSTRUCTIONS.md from my knowledgemaxxing repo and process this video: [YouTube URL]
```

Perplexity will:
- Read `INSTRUCTIONS.md` to understand the structure
- Check existing `concepts/` and `topics/` to avoid duplicates
- Extract and structure the knowledge from the video
- Push all `.md` files directly to your repo

### 5. Pull and open in Obsidian

```bash
git pull
```

All files use standard YAML frontmatter and `[[wikilinks]]` — Obsidian reads them natively.

---

## Customizing your topic list

Edit the **Controlled topic list** section in `INSTRUCTIONS.md` to match your interests.

Default topics:
```
defi, solidity, uniswap, ai-agents, trading, market-structure,
infrastructure, security, tokenomics, blockchain, frontend, backend,
research, economics, psychology, productivity, other
```

Replace with whatever domains you study.

---

## Example output

After processing a video, you get:

**`sources/youtube/2026/04/dQw4w9WgXcQ.md`**
```yaml
---
type: source/youtube
video_id: "dQw4w9WgXcQ"
title: "..."
channel: "..."
topics: ["productivity"]
concepts: ["deep-work", "flow-state"]
confidence: 0.95
status: processed
---
## Summary
...
## Key ideas
- ...
## Concepts
- [[deep-work]]
- [[flow-state]]
## Actions
- ...
## Open questions
- ...
```

**`concepts/deep-work.md`** — atomic concept note, auto-created and linked across videos.

---

## Tips

- **Dataview**: use the `type: source/youtube` frontmatter to query all your video notes in Obsidian.
- **Graph view**: concepts and topics create a knowledge graph automatically via wikilinks.
- **Deduplication**: Perplexity checks existing concepts before creating new ones, so your graph stays clean.
- **Language**: notes are written in the same language as the video by default.

---

## Built by

[@rusrio](https://github.com/rusrio) — fork it, adapt it, make it yours.
