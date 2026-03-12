# claude-code-work

A slide-generation workflow powered by [Marp](https://marp.app/), Claude Code, Skills, and Git.

## What This Repo Is

This repository is a **reusable baseline** for generating presentation slides with Claude Code.  
It combines Markdown-based slide authoring (via Marp) with Claude Code's AI capabilities so you can plan, write, review, and export slide decks in a consistent, repeatable way.

The intended workflow is:

1. **Plan** – describe the presentation goal to Claude Code
2. **Write** – Claude Code drafts or updates `slides/deck.md`
3. **Review** – inspect and refine the Markdown via Git diff
4. **Export** – run an npm script to produce HTML, PDF, or PPTX

## Why Marp + Claude Code

| Concern | Marp approach |
|---------|--------------|
| Source of truth | Plain Markdown — readable, diffable, version-controlled |
| AI generation | Claude Code edits `.md` files directly — no special plugin needed |
| Export flexibility | One source → HTML, PDF, PPTX with a single CLI command |
| Theme control | CSS-based themes are easy to customise and share |
| Collaboration | Git history captures every change to every slide |

## Directory Structure

```text
repo-root/
├─ .claude/
│  ├─ agents/      # Claude Code subagent definitions
│  └─ skills/      # Reusable Claude Code skills
├─ slides/
│  └─ deck.md      # Marp slide source
├─ dist/           # Generated export outputs (gitignored)
├─ themes/
│  └─ default.css  # Custom Marp theme
├─ assets/         # Images, fonts, and other static assets
├─ scripts/        # Build and utility scripts
├─ examples/       # Example slide decks
├─ .github/
│  └─ workflows/   # CI/CD workflows
├─ package.json
├─ README.md
└─ .gitignore
```

## Setup

### Prerequisites

- [Node.js](https://nodejs.org/) 18+
- A Chromium-based browser for PDF/PPTX export (see [Export slides](#export-slides))

### Install dependencies

```bash
npm install
```

This installs [Marp CLI](https://github.com/marp-team/marp-cli) locally via npm — no global installation required.

## How to Create Slides

Slides live in `slides/deck.md`. Each slide is separated by `---`.  
The file starts with a YAML front matter block that enables Marp and sets the theme:

```markdown
---
marp: true
theme: default
paginate: true
---

# Slide Title

Slide content goes here.

---

## Next Slide

More content.
```

To **preview** slides in a browser with live reload:

```bash
npm run preview
```

Open the URL printed in the terminal (usually `http://localhost:8080`) to see the rendered deck.  
Any save to `slides/deck.md` automatically refreshes the preview.

### Customising the theme

Edit `themes/default.css` to adjust colours, fonts, and layout.  
The file uses CSS custom properties, so most visual changes are a one-line edit.

### Adding images and assets

Place images and fonts in `assets/` and reference them in Markdown with a relative path:

```markdown
![diagram](../assets/diagram.png)
```

## Export Slides

All outputs are written to the `dist/` directory (created automatically, gitignored).

```bash
# Export to HTML (no browser required)
npm run build:html

# Export to PDF (requires Chromium)
npm run build:pdf

# Export to PPTX (requires Chromium)
npm run build:pptx

# Export all three formats at once
npm run build:all
```

### Installing Chromium for PDF/PPTX export

PDF and PPTX export require a Chromium-based browser to be installed on your system.

- **Linux (Debian/Ubuntu):** `sudo apt-get install -y chromium-browser`
- **macOS:** Install [Google Chrome](https://www.google.com/chrome/) or run `brew install --cask chromium`
- **Windows:** Install [Google Chrome](https://www.google.com/chrome/) or [Chromium](https://www.chromium.org/getting-involved/download-chromium/)

## Recommended Claude Code Workflow

Claude Code works best in this repo when given a clear goal and allowed to edit `slides/deck.md` directly.

### Typical session

1. **Open** the repo in Claude Code (or use the CLI: `claude`).
2. **Describe** the presentation you need, e.g.:
   > "Create a 10-slide deck introducing our Q2 product roadmap. Use the existing theme."
3. **Review** the generated diff with `git diff slides/deck.md` before accepting.
4. **Iterate** — ask Claude Code to revise specific slides, add sections, or adjust tone.
5. **Export** when satisfied:
   ```bash
   npm run build:all
   ```

### Tips

- Keep `slides/deck.md` as the single slide source; avoid maintaining multiple decks for the same presentation.
- Use `.claude/skills/` to store reusable prompt snippets (e.g. "add a summary slide", "apply brand colours").
- Use `.claude/agents/` to define subagents for specialised tasks (e.g. a "diagram generator" agent).
- Commit often so you can revert to an earlier draft with `git checkout`.

## Known Limitations

| Limitation | Detail |
|------------|--------|
| **PPTX editability** | Marp exports PPTX as static slides rendered from HTML. Shapes and text are embedded as images or fixed elements, so fine-grained editing in PowerPoint is limited. If you need a fully editable PPTX, consider a PPTX-native tool or accept that post-export editing will be manual. |
| **Complex layouts** | Marp supports a subset of CSS layouts. Highly complex multi-column or overlay designs require custom CSS and may not render identically across export formats. |
| **No speaker notes** | Marp does not currently export speaker notes to PPTX. HTML export preserves notes when using presenter mode. |
| **Chromium dependency** | PDF and PPTX export require a local Chromium installation. In headless CI environments, ensure Chromium is available or use the HTML export only. |
| **Single deck per run** | The npm scripts target `slides/deck.md` only. To build multiple decks, adjust the scripts in `package.json` or add new script entries. |

## License

See [LICENSE](LICENSE).