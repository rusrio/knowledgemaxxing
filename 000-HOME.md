---
tags: [home, dashboard]
---

# 🧠 knowledgemaxxing

> *Every YouTube URL is a knowledge deposit.*

---

## 📊 Stats

```dataview
TABLE WITHOUT ID
  length(rows) AS "Total sources"
FROM "sources"
FLATTEN file.name AS name
```

---

## 🔍 Recently processed

```dataview
TABLE title AS "Title", channel AS "Channel", topics AS "Topics"
FROM "sources/youtube"
SORT processed_at DESC
LIMIT 10
```

---

## 🏷️ Topics

```dataview
TABLE WITHOUT ID
  link(file.link, slug) AS "Topic",
  length(file.inlinks) AS "🔗 Links in"
FROM "topics"
SORT length(file.inlinks) DESC
```

---

## 🧩 Most connected concepts

```dataview
TABLE WITHOUT ID
  link(file.link, slug) AS "Concept",
  topics AS "Topics",
  length(sources) AS "🎥 Sources"
FROM "concepts"
SORT length(sources) DESC
LIMIT 20
```

---

## 📅 Sources by month

```dataview
TABLE WITHOUT ID
  dateformat(date(processed_at), "yyyy-MM") AS "Month",
  length(rows) AS "Videos"
FROM "sources/youtube"
GROUP BY dateformat(date(processed_at), "yyyy-MM")
SORT dateformat(date(processed_at), "yyyy-MM") DESC
```

---

## 📍 Atlas

- [[atlas/index|Knowledge Map]]

---

## ⚙️ Quick actions

- [[inbox/unsorted|Inbox]]
- Use `Ctrl+T` to create a note from template
- Run `git pull` to sync latest knowledge from GitHub
