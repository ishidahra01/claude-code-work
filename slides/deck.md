---
marp: true
theme: default
paginate: true
---

<!-- _class: title -->

# Reproducible Slides with Marp + Claude Code

How to plan, write, review, and export presentation decks  
as version-controlled Markdown

---

## Agenda

- Why this approach works
- The four-step workflow
- Demo: deck from prompt to export
- Guardrails that keep decks consistent
- Getting started today

---

## The Problem with Traditional Slide Tools

- Slides live in binary files — hard to diff or review
- AI output lands in a chat window, not in the file
- No repeatable quality bar across decks
- Export format locks you into one toolchain

---

## Why Marp + Claude Code

| Concern | Marp + Claude Code approach |
|---------|----------------------------|
| Source of truth | Plain Markdown — diffable, version-controlled |
| AI generation | Claude Code edits `.md` directly — no copy-paste |
| Export flexibility | One source → HTML, PDF, PPTX |
| Quality control | Guardrails and reviewer subagent built in |
| Collaboration | Git history captures every slide change |

---

## The Four-Step Workflow

1. **Plan** — describe the goal; planner subagent generates an outline
2. **Write** — Claude Code drafts `slides/deck.md` from the approved outline
3. **Review** — inspect the diff with `git diff slides/deck.md`
4. **Export** — run `npm run build:all` to produce HTML, PDF, and PPTX

---

## Step 1 — Plan with the Planner Subagent

The planner collects five inputs before writing anything:

- **Audience** — who attends and their expertise level
- **Purpose** — inform, persuade, instruct, or demo
- **Duration** — total presentation time in minutes
- **Slide count** — number of slides expected
- **Key message** — the single idea the audience must leave with

> No outline approved → no Markdown written.

---

## Step 2 — Write in Markdown

```markdown
---
marp: true
theme: default
paginate: true
---

<!-- _class: title -->

# Your Deck Title

Author · Date

---

## First Content Slide

- Bullet one
- Bullet two
- Bullet three
```

Claude Code edits this file directly — the diff is reviewable in Git.

---

## Step 3 — Review the Diff

```bash
git diff slides/deck.md
```

- Green lines = added content
- Red lines = removed content
- Each slide is clearly separated by `---`

Iterate on individual slides without regenerating the whole deck.

---

## Step 4 — Export

```bash
npm run build:html   # no browser required
npm run build:pdf    # requires Chromium
npm run build:pptx   # requires Chromium
npm run build:all    # all three at once
```

Output lands in `dist/` (gitignored).  
Commit `slides/deck.md`; export on demand.

---

<!-- _class: cols -->

## Guardrails Keep Decks Consistent

**What the rules enforce**

- One message per slide
- ≤ 5 bullets per slide
- ≤ 8 words per bullet
- No dense paragraphs on slides
- Visuals over bullets for data

**Why it matters**

- Audiences follow a single thread
- Slides stay scannable during a talk
- AI output stays within quality bounds
- Every deck looks and reads consistently

---

## Getting Started

1. Clone the repo and run `npm install`
2. Open Claude Code and describe your presentation
3. Approve the outline from the planner subagent
4. Review and export the generated deck

```bash
git clone <repo-url>
cd claude-code-work
npm install
npm run preview   # live preview at localhost:8080
```

See `docs/slide-rules.md` and `examples/prompts.md` for details.

---

<!-- _class: title -->

# Thank You

Questions?  
`docs/slide-rules.md` · `examples/prompts.md`

