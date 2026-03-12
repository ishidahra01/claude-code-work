# CLAUDE.md — Repository Instructions for Claude Code

## Repository Purpose

This repository is a **slide-generation workflow** built on [Marp](https://marp.app/), Claude Code, Skills, and Git.  
Claude Code's role is to help plan, draft, and refine Markdown-based slide decks stored in `slides/deck.md`.

---

## Workflow: Plan First, Generate Second

**Never write a full deck immediately.** Always follow these steps in order:

### Step 1 — Clarify before writing

Before touching any file, ask the user to confirm:

| Question | Why it matters |
|----------|---------------|
| Who is the audience? | Tone, vocabulary, and detail level |
| What is the purpose? | Inform, persuade, instruct, demo? |
| How long is the presentation? | Determines slide count |
| How many slides are expected? | Sets scope before generation |

Do not proceed to Step 2 until these are answered.

### Step 2 — Create an outline first

Draft a plain-text outline (not Marp Markdown) and present it for approval.  
The outline must list every slide title and a one-line description of its content.

```
1. Title slide — deck name, author, date
2. Agenda — list of topics
3. Background — why this topic matters (2–3 bullets)
...
N. Thank You — questions prompt
```

**Wait for explicit approval before generating the deck.**

### Step 3 — Generate the deck Markdown

Only after the outline is approved:

- Edit `slides/deck.md` directly.
- Generate **one slide at a time** when iterating; show diffs rather than replacing the whole file.
- Respect the existing YAML front matter (`marp: true`, `theme: default`, `paginate: true`).

### Step 4 — Review

- Invite the user to run `git diff slides/deck.md` to inspect changes.
- Offer to revise individual slides on request.
- Do not re-generate the entire deck to fix a single slide.

### Step 5 — Export

When the deck is approved, remind the user to export:

```bash
npm run build:html   # no browser required
npm run build:pdf    # requires Chromium
npm run build:pptx   # requires Chromium
npm run build:all    # all three formats
```

---

## Slide Quality Guardrails

- **1 message per slide.** Each slide communicates exactly one idea.
- **Minimal text.** Use short bullets (≤ 8 words each). Avoid full sentences unless quoting.
- **3–5 bullets maximum** per slide. If you need more, split into two slides.
- **Clear, descriptive titles.** The title alone should communicate the slide's point.
- **No dense paragraphs.** Prose belongs in speaker notes, not slide body.
- **Consistent tone.** Match the vocabulary and formality level of the audience.
- **Respect theme conventions.** Do not override `theme:` in the front matter unless the user explicitly asks.
- **Keep front matter intact.** Always preserve `marp: true`, `theme: default`, `paginate: true`.

---

## Anti-Patterns — Never Do These

| Anti-pattern | Why it is harmful |
|---|---|
| Writing a full deck without an outline | Creates rework; ignores user intent |
| Overloading slides with text | Defeats the purpose of a slide medium |
| Mixing multiple messages into one slide | Confuses the audience |
| Generating the entire deck to fix one slide | Destroys user edits; hard to review |
| Changing the Marp theme or front matter silently | Breaks visual consistency |
| Ignoring the agreed slide count | Misaligns with the user's time budget |
| Using dense paragraphs instead of bullets | Makes slides unreadable during a talk |

---

## File Conventions

| Path | Purpose |
|------|---------|
| `slides/deck.md` | Single source of truth for the slide deck |
| `themes/default.css` | Custom Marp theme — edit for visual changes |
| `assets/` | Images and fonts referenced in slides |
| `dist/` | Export outputs (gitignored — do not commit) |
| `.claude/skills/` | Reusable prompt snippets for common tasks |
| `.claude/agents/` | Subagent definitions for specialised tasks |

---

## Notes

- This file optimises Claude Code's behaviour in this repository. It is not user-facing documentation.
- When in doubt, **ask before generating**. A short clarifying question is always better than a wrong deck.
