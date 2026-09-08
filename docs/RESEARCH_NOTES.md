# Adding a research note

Create a Markdown file in `_research_notes/`. Use a short English filename, for example:

```text
_research_notes/attention-is-all-you-need.md
```

Copy this template into the new file:

```markdown
---
title: "Article title"
topic: recommender-systems
author: "Author name"
source: "Website or publication"
source_url: "https://example.com/original-article"
source_date: "2026-01-15"
saved_at: "2026-09-08"
summary: "A short summary shown on the reading-list card and note page."
takeaway: "Why I saved this article or the key idea I want to remember."
tags:
  - Representation Learning
  - Recommendation
featured: false
---

## What stood out

Write your summary or a short quotation here.

## My understanding

Write your own analysis here. Normal Markdown is supported, including lists,
links, images, code blocks, blockquotes, tables, and math syntax supported by
the site.

## Questions

- A question to revisit.
- A possible connection to another paper.

## Further thoughts

Add as many sections and paragraphs as you need.
```

The `topic` value must be one of:

- `recommender-systems`
- `reinforcement-learning-llms`
- `natural-language-processing`

Use `title`, `topic`, and `saved_at` for every note. Add `source_url` when the
note is based on someone else's article. Prefer summaries and short, properly
attributed quotations instead of reproducing an entire copyrighted article
without permission.
