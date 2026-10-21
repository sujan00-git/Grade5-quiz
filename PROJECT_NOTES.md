# Grade 5 Quiz Project — Notes

## HOW TO COME BACK TO THIS PROJECT

**Local working directory:** `/home/mrahman/claude/projects/math/rezabhai/`
**GitHub repo:** https://github.com/sujan00-git/Grade5-quiz (public, account `sujan00-git`)
**Live site:** https://sujan00-git.github.io/Grade5-quiz/grade5-quizes.html

To resume in a fresh Claude Code session:

1. `cd /home/mrahman/claude/projects/math/rezabhai/`
2. Open this file (`PROJECT_NOTES.md`) and tell Claude: *"Read PROJECT_NOTES.md and continue from where we left off."*
3. The three HTML practice pages and the landing page are already here and synced to GitHub.
4. The source workbook photos (`1.jpeg`, `2.jpeg`, `3.jpeg`) are kept locally only — they are **not** uploaded to GitHub (copyright: James An College).

### Making a change

1. Edit a `.html` file.
2. Commit and push:
   ```bash
   git add <file>
   git -c user.name="sujan00-git" -c user.email="sujan00-git@users.noreply.github.com" \
       commit -m "Short message"
   git push
   ```
   (We use per-command `-c user.name`/`user.email` because the global git config is not set.)
3. GitHub Pages rebuilds in 1–3 minutes.

---

## FILES IN THIS REPO

| File | Purpose |
|---|---|
| `grade5-quizes.html` | Landing page with links to the three quizzes. |
| `index.html` | Older landing page (same content, slightly different styling). Kept so `/` still works. |
| `page1_practice.html` | **Quiz 1** — Decimals: Expanded, Standard & Matching |
| `page2_practice.html` | **Quiz 2** — Represent Decimals (word form → standard) |
| `page3_practice.html` | **Quiz 3** — Problem Solving (seven sections of mixed review) |

Local-only (not in Git): `1.jpeg`, `2.jpeg`, `3.jpeg` — the original workbook photos used as source material.

---

## WHAT EACH PAGE DOES

### Page 1 — Decimals Practice
Mirrors sections III, IV, V of the workbook:

- **III. Write decimals in expanded form** — 5 random decimals like `12.63`; student types `1×10 + 2×1 + 6×0.1 + 3×0.01`. Checker accepts `x`, `X`, `*`, or `×` and ignores term order.
- **IV. Write standard decimal form** — 5 expanded expressions; student types the decimal.
- **V. Matching** — 5 pairs. Left column mixes word form and expanded form; right column has decimals. Click left then click the matching right item. Wrong picks flash red; correct picks lock green.

### Page 2 — Represent Decimals (Set 13)
- **I. Introduction** — teaching example showing standard / expanded (with fractions) / word form of 5.1711.
- **II. Write these decimals in standard form** — 5 word-form prompts (e.g. *"Two tenths"*, *"Six and nine thousand two hundred thirty-three ten-thousandths"*) → student types the decimal.

### Page 3 — Problem Solving (Set 13)
Seven sections, each with 5 randomized questions:

- **I. Multiplication and Divisions** — order-of-operations expressions using ×, ÷, +, −. All answers are integers. Templates include `a × b + c ÷ d`, `a × b − c ÷ d`, `c ÷ d + a × b`, `a × b × c`, `c ÷ d − a`, and `a × b ÷ c`.
- **II. Round to the Nearest Hundred** — mix of 3-, 4-, and 5-digit numbers. Answer accepts optional commas (e.g. `54,300` or `54300`).
- **III. Fill in the Blanks (Expanded Form)** — `538.274 = __ × 100 + __ × 10 + __ × 1 + __ × 0.1 + __ × 0.01 + __ × 0.001`. Each blank is marked green/red individually.
- **IV. Partition the Number** — same structure but with words (`__ hundreds + __ tens + __ units + __ tenths + __ hundredths + __ thousandths`).
- **V. Perimeter of a Rectangle** — SVG rectangle scaled to its dimensions with cm labels. Student types the perimeter; accepts `40` or `40 cm`.
- **VI. Subtract Fractions** — unlike denominators, drawn from a 20-pair pool. Any equivalent fraction is accepted (checker uses cross-multiplication, not string match).
- **VII. Math Trivia** — four miscellaneous questions: name-the-shape of an everyday object, multiple-choice measurement tool, budget word problem (division), shopkeeper word problem (multiplication).

---

## KEY DESIGN DECISIONS

- **Per-section New Questions button.** Each section has its own *New Questions* button next to *Check Answers* / *Show Answers*. Regenerating one section doesn't wipe in-progress work in another.
- **Roman-numeral section labels.** All pages use the same convention (I, II, III, …).
- **"Back to all quizzes" link** on every practice page, top-left of the header.
- **Answer checking is tolerant** where sensible: fraction equivalents, comma-separated numbers, optional units like `cm`, case-insensitive text, varied × operators, etc.
- **No external dependencies.** Every page is a single self-contained HTML file with inline CSS + vanilla JavaScript. No build step, no npm, no CDN. Open any `.html` in a browser and it works offline.
- **Light-mode-only design.** No dark mode currently (not usually a kid-friendly setting for math practice).

---

## IDEAS FOR FUTURE IMPROVEMENTS

Ordered roughly by effort — easy wins at the top.

1. **Score counter per section** — show "4/5 correct" after Check Answers.
2. **Overall quiz score / progress bar** across all sections on a page.
3. **Timer** — optional "beat the clock" mode per section.
4. **Printable version** — a `?print=1` query param that hides buttons so a kid can do it on paper.
5. **Difficulty toggle** — easy / medium / hard controls that change the number ranges in the generator functions.
6. **Save progress** to `localStorage` so a half-done quiz survives a reload.
7. **Streak tracker** across sessions ("you've practiced 3 days in a row").
8. **Audio feedback** — a soft chime on correct, buzzer on wrong (toggleable).
9. **New question types** — long division, mixed-number operations, decimal × / ÷, elapsed time, area + volume.
10. **A fourth page** — once you have more workbook photos, follow the same pattern: section headings → randomized generators → per-section buttons.
11. **Dark-mode theme toggle** — add `@media (prefers-color-scheme: dark)` with inverted palette.
12. **PWA / installable** — add a manifest + service worker so Reza can "install" the quiz app on a tablet and use it offline.

### If you want to add a new section to Page 3

Pattern already used repeatedly in `page3_practice.html`:

1. Add a `<section class="section">` block with `h2`, container div (`id="sectionX"`), and the three-button controls row.
2. In the script, add:
   - `let sectionXData = [];`
   - `function makeXQuestion()` — returns a randomized question object.
   - `function generateSectionX()` — fills `sectionXData` and calls `renderSectionX`.
   - `function renderSectionX()` — writes the HTML into `#sectionX`.
   - `function checkSectionX()` and `function revealSectionX()`.
3. Add `generateSectionX();` to `generateAll()`.

---

## GIT / REPO HOUSEKEEPING

- Repo is **public** so GitHub Pages works for free.
- Pages is served from **main branch, root path** (configured via REST API `POST /repos/{owner}/{repo}/pages`).
- Commit attribution: `Co-Authored-By: Claude Opus 4.7 <noreply@anthropic.com>` is appended to every commit (per session attribution rules).
- `.gitignore` is **not** set up yet — if you add other files you don't want pushed, create one (`1.jpeg\n2.jpeg\n3.jpeg\nPROJECT_NOTES.md\n` would be a reasonable start if you don't want notes synced either).

---

## COMMIT HISTORY (as of this writing)

Short list of what was done, newest at the top. Use `git log --oneline` for the live view.

- Page 3 Section VI: tighten spacing between fraction and answer box
- Page 3: relabel section headings A–G as Roman numerals I–VII
- Move New Questions button from page header to each section
- Page 3: label remaining questions as Section G – Math Trivia
- Page 3: add Section F – Subtract Fractions
- Page 3: add Section E – Perimeter of a Rectangle
- Page 3: add Section D – Partition the Number
- Page 3: add Section C – Fill in the Blanks (Expanded Form)
- Page 3: add Section B – Round to the Nearest Hundred
- Restructure page 3: Section A – Multiplication and Divisions
- Add back link to the quizzes landing page on each practice page
- Add grade5-quizes landing page linking to all three quizzes
- Add Grade 5 math practice pages (decimals + mixed review)
