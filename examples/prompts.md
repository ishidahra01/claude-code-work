# Prompt Examples

Ready-to-use prompts for each stage of the slide-generation workflow.  
Copy, adapt, and paste into a Claude Code session.

---

## 1 — Outline Generation

Use these prompts to engage the planner subagent and get an approved outline before any Markdown is written.

### Minimal outline request

```
Create a slide outline for a 15-minute presentation.
Audience: software engineers who have not used Marp before.
Purpose: convince them to adopt the Marp + Claude Code workflow.
Target slide count: 10.
Key message: Marp + Claude Code makes slides faster to write, easier to review, and simpler to maintain than traditional tools.
```

### Outline request with extra constraints

```
Plan a 20-slide technical deep-dive on our CI/CD pipeline redesign.
Audience: senior engineers and tech leads.
Purpose: inform — explain what changed and why.
Duration: 30 minutes.
Key message: the new pipeline cuts build time by 60% while improving reliability.
Constraints:
- Include a "before vs. after" comparison slide.
- Add a slide for open questions and known risks.
- End with a "next steps" slide that lists three owner-assigned actions.
```

### Iterating on an outline

```
The outline looks good. Can you:
1. Merge slides 4 and 5 — they carry the same message.
2. Add a "Lessons Learned" slide between slide 8 and the summary.
3. Change the closing slide to a "Call to Action" rather than a Q&A prompt.
```

---

## 2 — Slide Draft Generation

Use these prompts after an outline is approved to generate or update `slides/deck.md`.

### Generate a full deck from an approved outline

```
The outline is approved. Generate slides/deck.md using the approved outline.
- Use the existing theme (theme: default) and front matter.
- Each slide should have a clear, descriptive title.
- Use short bullets (≤ 8 words each), ≤ 5 per slide.
- No dense paragraphs — elaboration goes in speaker notes.
- Apply <!-- _class: title --> to the opening and closing slides.
- Apply <!-- _class: cols --> to the "before vs. after" comparison slide.
```

### Add a single new slide

```
Add a new slide after slide 6 in slides/deck.md.
Title: "Pilot Results — 60% Faster Builds"
Content: a table comparing the old pipeline and new pipeline across three metrics: build time, failure rate, and deployment frequency.
Keep the existing slides unchanged.
```

### Replace the content of one slide

```
Update slide 4 ("The Problem") in slides/deck.md.
Replace the current content with three short bullets that describe:
1. Binary PPTX files are not diffable.
2. AI output requires manual copy-paste into the tool.
3. No shared quality bar across teams.
Do not touch any other slide.
```

### Add speaker notes to all slides

```
Add speaker notes to every slide in slides/deck.md.
Each note should be 2–3 sentences that elaborate on the slide message — not repeat the bullets.
Use the Marp comment syntax: a blank line followed by <!-- ... --> at the end of each slide block.
```

---

## 3 — Review and Density Reduction

Use these prompts to audit an existing deck and reduce visual clutter.

### Full deck review

```
Review slides/deck.md against the rules in docs/slide-rules.md.
For each slide that violates a rule, list:
- Slide number and title
- Which rule is violated
- A suggested fix (do not edit the file yet — show suggestions only)
```

### Reduce slide density

```
Slide 7 in slides/deck.md has too many bullets.
Reduce it to ≤ 5 bullets of ≤ 8 words each.
Move the removed detail into speaker notes.
Show a diff — do not regenerate the whole file.
```

### Shorten a verbose title

```
The title of slide 5 is too long.
Rewrite it as a concise active-voice phrase of ≤ 8 words that still communicates the slide's core message.
Show the old and new title side by side before making the change.
```

### Remove prose from slide body

```
Slide 9 contains a paragraph rather than bullets.
Convert it to a bullet list (≤ 5 items, ≤ 8 words each).
Move any removed detail to speaker notes.
Edit only slide 9; leave the rest of the deck intact.
```

---

## 4 — Export Preparation

Use these prompts to verify the deck is export-ready and to trigger the build.

### Pre-export checklist

```
Before I export, check slides/deck.md for:
1. Correct front matter (marp: true, theme: default, paginate: true).
2. At least one title-class slide for the opening.
3. No slide with more than 5 bullets.
4. No paragraph text in the slide body.
5. All image references point to files that exist under assets/.
Report any issues found. Do not edit the file.
```

### Trigger HTML export

```
Run the HTML export for slides/deck.md and confirm the output file was created.
Command: npm run build:html
Expected output: dist/deck.html
```

### Trigger full export

```
Export the deck to all three formats.
Command: npm run build:all
Confirm that dist/deck.html, dist/deck.pdf, and dist/deck.pptx were all created.
If any export fails, show the error output.
```

### Post-export summary

```
The export is complete. Summarise what was built:
- File paths and sizes for each output in dist/
- Which formats require Chromium and whether it was available
- Any warnings from the Marp CLI output
```
