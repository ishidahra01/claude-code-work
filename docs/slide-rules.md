# Slide Authoring Rules

Practical guardrails for writing clear, consistent slide decks in this repository.  
Follow these rules when authoring slides manually or when instructing Claude Code to generate content.

---

## Core Principle

> **One slide = one message.**  
> Every slide communicates exactly one idea. If you cannot state the slide's message in a single sentence, split it into two slides.

---

## Rules

### 1 — One message per slide

Each slide has a single core idea. The title alone should convey that idea.  
Avoid agenda-style slides that introduce multiple topics at once (except for an explicit Agenda slide).

**Good:** `## Automated tests cut defect escape rate by 40%`  
**Bad:** `## Testing, deployment, and monitoring`

---

### 2 — Keep bullet count ≤ 5

Use three to five bullets per slide. Never exceed five.  
If you need more points, either:
- Cut the least important items
- Split the slide into two focused slides

---

### 3 — Keep bullets short (≤ 8 words)

Each bullet should be a phrase, not a sentence.  
Remove articles, filler words, and elaboration — those belong in speaker notes.

**Good:** `- 40 % fewer production incidents`  
**Bad:** `- Our new monitoring approach has led to a reduction of approximately 40 % in the number of production incidents we observed during the pilot`

---

### 4 — Titles must be clear and descriptive

The title is the most visible text on the slide. Write it so the audience immediately understands the slide's point — even without reading the body.

- Use active-voice noun phrases or findings: `Pilot results confirm 3× throughput gain`
- Avoid vague labels: ~~`Results`~~, ~~`Overview`~~, ~~`Discussion`~~

---

### 5 — No dense paragraphs on slides

Prose belongs in speaker notes, not slide body. If you find yourself writing a paragraph, convert it to bullets or move it to notes.

```markdown
<!-- Speaker notes go here after a blank line at the bottom of the slide block -->

The detailed explanation can be written as a speaker note without cluttering the visual.
```

---

### 6 — Prefer visuals over bullets when data allows

When comparing numbers, showing a process, or demonstrating a relationship, a table, diagram, or chart is almost always clearer than a bullet list.

| Situation | Preferred format |
|-----------|-----------------|
| Comparing options | Table |
| Showing a sequence or pipeline | Numbered list or diagram |
| Presenting metrics | Table or callout |
| Abstract concepts without data | Bullets |

---

### 7 — Use slide classes intentionally

The theme provides three layout classes. Set them with a front-matter comment on the relevant slide.

| Class | Purpose | Usage |
|-------|---------|-------|
| *(none)* | Standard content slide | Default — no class needed |
| `title` | Opening / section divider with dark background | `<!-- _class: title -->` |
| `cols` | Two-column comparison layout | `<!-- _class: cols -->` |

---

### 8 — Maintain consistent front matter

Every deck must start with this block and must not change `marp`, `theme`, or `paginate` without explicit intent:

```yaml
---
marp: true
theme: default
paginate: true
---
```

---

### 9 — Reserve speaker notes for elaboration

Speaker notes are not slide overflow. Use them for:
- Data sources and citations
- Talking-point elaboration (2–4 sentences max)
- Questions to prompt audience discussion

---

### 10 — Anti-patterns to avoid

| Anti-pattern | Why it harms the deck |
|---|---|
| Full sentences as bullets | Hard to scan; forces audience to read, not listen |
| More than 5 bullets per slide | Splits audience attention; looks cluttered |
| Vague slide titles (`Overview`, `Details`) | Audience loses the point without reading the body |
| Dense paragraphs on slide body | Unreadable at presentation scale |
| Mixing multiple topics in one slide | Audience cannot follow a single narrative thread |
| Overriding theme silently | Breaks visual consistency across decks |
| Generating the whole deck to fix one slide | Destroys user edits; produces unnecessary diffs |
