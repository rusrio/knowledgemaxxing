---
type: topic
slug: "<% tp.file.title %>"
created_at: "<% tp.date.now("YYYY-MM-DD") %>"
---

# <% tp.file.title %>

## Sources

```dataview
LIST title
FROM "sources"
WHERE contains(topics, "<% tp.file.title %>")
SORT processed_at DESC
```

## Concepts in this topic

```dataview
LIST
FROM "concepts"
WHERE contains(topics, "<% tp.file.title %>")
SORT file.name ASC
```
