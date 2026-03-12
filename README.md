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

```bash
# Export to HTML
npx marp slides/deck.md --output output/deck.html

# Export to PDF
npx marp slides/deck.md --pdf --output output/deck.pdf
```

## License

See [LICENSE](LICENSE).