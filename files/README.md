# Sparkboard ✨

> A soft little planner that turns half-formed ideas into step-by-step roadmaps you'll actually follow.

Sparkboard is a single-file web app that takes any idea — a business, a craft project, an app, a personal goal — and walks you through a cozy Q&A to bloom it into a phased, checkable roadmap. Everything lives in your browser; no accounts, no backend, no tracking.

🌸 **Try it:** open `index.html` in any modern browser.

---

## Features

- 🎯 **Auto-categorization** — keyword-weighted detection across 6 categories (Business, Tech, Creative, Personal Growth, Lifestyle, General).
- 💬 **Conversational refinement** — one question at a time, with chat-style history and questions that adapt to your earlier answers.
- 🗺️ **Tailored roadmaps** — 5 category-specific templates plus a general fallback, each with 4 phases and ~20 tasks personalized with your responses.
- 📌 **Pinterest-style idea board** — saved ideas render as gradient-tinted masonry cards with category badges.
- ✅ **Progress tracking** — tick off tasks inside any saved roadmap; progress persists across sessions.
- 💾 **localStorage persistence** — your board survives refreshes and browser restarts.
- 📱 **Mobile-responsive** — masonry collapses from 4 → 1 column, modal and typography scale gracefully.

## Aesthetic

Soft pastel palette (blush, lavender, cream, sage, peach) paired with *Playfair Display* for headings, *Nunito* for body, and *Caveat* for handwritten accents. Decorative touches include a floating sparkle layer, dotted phase-timeline, gradient card tints, and gentle hover micro-animations.

## Tech stack

- **HTML + CSS + vanilla JS** — single file, no build step, no dependencies.
- Google Fonts (loaded via CDN).
- `localStorage` for persistence.
- Categorization uses weighted keyword matching; questions and roadmaps are rule-based decision trees with template interpolation.

## Running locally

No build, no install:

```bash
# Just open it
open index.html         # macOS
xdg-open index.html     # Linux
start index.html        # Windows
```

Or serve it with any static server if you prefer:

```bash
python3 -m http.server 8000
# then visit http://localhost:8000
```

## Deploying to GitHub Pages

This repo ships with a workflow at `.github/workflows/deploy.yml` that auto-publishes to GitHub Pages on every push to `main`.

**One-time setup:**

1. Push the repo to GitHub.
2. Go to **Settings → Pages**.
3. Under **Build and deployment → Source**, choose **GitHub Actions**.
4. Push to `main` — your site will be live at `https://<username>.github.io/<repo-name>/` within a minute.

## Project structure

```
.
├── index.html                  # The entire app (HTML + CSS + JS inline)
├── README.md                   # You are here
├── LICENSE                     # MIT
├── .gitignore
└── .github/
    └── workflows/
        └── deploy.yml          # GitHub Pages auto-deploy
```

## How the logic works (for the curious)

**Categorization** (`detectCategory`) — scans the idea text for keywords in each category bank, weighting longer keywords more heavily. Falls back to the `general` category when no keywords match.

**Question selection** (`QUESTIONS`) — each of the 6 categories has a 6-question bank tuned for that domain (e.g., business asks about audience, pricing, unique angle; creative asks about medium, theme, skill level). Question text supports `{answers.id|fallback}` placeholders that splice in earlier answers — so the second question can naturally reference the first.

**Roadmap generation** (`ROADMAPS`) — each category has a builder function that returns 4 phases of tasks. Tasks use the same `{answers.id|fallback}` interpolation, so the final plan feels personalized rather than generic.

**Persistence** — saved ideas live under the key `sparkboard.ideas.v1` in `localStorage`. The versioned key leaves room for schema migrations later.

## Customizing

Most things are tweakable from the top of the `<script>` block in `index.html`:

- **Add a category** → add an entry to `CATEGORIES`, a matching question bank to `QUESTIONS`, and a roadmap builder to `ROADMAPS`. Also add a CSS color token (`--cat-yourcategory`) and a card tone class (`.card.tone-yourcategory`).
- **Change the color palette** → edit the CSS custom properties at the top of the `<style>` block.
- **Adjust question count** → change the length of any array inside `QUESTIONS`.

## License

[MIT](./LICENSE) — do whatever you'd like with it. 🌷
