# claude-code-work

A slide-generation workflow powered by [Marp](https://marp.app/), Claude Code, Skills, and Git.

## Purpose

This repository provides a reproducible baseline for generating slide decks with Claude Code:

- **Write** slides in Markdown using [Marp](https://marp.app/)
- **Review** changes and history through Git
- **Export** to HTML, PDF, or PPTX via Marp CLI
- **Automate** generation and export with Claude Code skills and subagents

## Repository Structure

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

## Getting Started

### Prerequisites

- [Node.js](https://nodejs.org/) 18+
- [Marp CLI](https://github.com/marp-team/marp-cli)

### Install dependencies

```bash
npm install
```

### Preview slides

```bash
npm run preview
```

### Export slides

All outputs are written to the `dist/` directory.

```bash
# Export to HTML
npm run build:html

# Export to PDF
npm run build:pdf

# Export to PPTX
npm run build:pptx

# Export all formats at once
npm run build:all
```

> **Note:** PDF and PPTX export require a Chromium-based browser (e.g. Google Chrome or Chromium) to be installed on your system.
> On Linux you can install it with `sudo apt-get install -y chromium-browser` (Debian/Ubuntu) or the equivalent for your distribution.
> On macOS, install [Google Chrome](https://www.google.com/chrome/) or run `brew install --cask chromium`.

## License

See [LICENSE](LICENSE).